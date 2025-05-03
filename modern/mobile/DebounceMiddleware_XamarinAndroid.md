# Debounce Middleware in Xamarin.Android

## Zweck
Diese Middleware filtert schnell aufeinanderfolgende Events und verhindert, dass sie mehrfach verarbeitet werden. Das ist besonders bei **UI-Klicks**, **Textänderungen** oder **asynchronen API-Aufrufen** nützlich.

---

## Version 1: "Letztes Event zählt" (klassisches Debounce-Verhalten)

```csharp
public class DebounceMiddleware
{
    private CancellationTokenSource _cts;
    private readonly TimeSpan _debounceDelay;

    public DebounceMiddleware(TimeSpan debounceDelay)
    {
        _debounceDelay = debounceDelay;
    }

    public async Task RunAsync(Func<Task> action)
    {
        _cts?.Cancel(); // vorigen Aufruf abbrechen
        _cts = new CancellationTokenSource();
        var token = _cts.Token;

        try
        {
            await Task.Delay(_debounceDelay, token);
            token.ThrowIfCancellationRequested();

            await action();
        }
        catch (OperationCanceledException)
        {
            // Ignorieren – neuer Aufruf kam früher
        }
    }
}
```

### Beispielnutzung:
```csharp
private readonly DebounceMiddleware _debounce = new(TimeSpan.FromMilliseconds(500));

public void OnSearchTextChanged(string newText)
{
    _debounce.RunAsync(async () =>
    {
        await SearchAsync(newText); // wird nur 500ms nach letzter Eingabe ausgelöst
    });
}
```

---

## Version 2: "Nur erstes Event zählt" (klassisches Throttle-Verhalten)

```csharp
public class ThrottleMiddleware
{
    private bool _isExecuting = false;
    private readonly TimeSpan _throttleDelay;

    public ThrottleMiddleware(TimeSpan throttleDelay)
    {
        _throttleDelay = throttleDelay;
    }

    public async Task RunAsync(Func<Task> action)
    {
        if (_isExecuting) return;

        _isExecuting = true;
        try
        {
            await action();
        }
        finally
        {
            await Task.Delay(_throttleDelay);
            _isExecuting = false;
        }
    }
}
```

### Beispielnutzung:
```csharp
private readonly ThrottleMiddleware _throttle = new(TimeSpan.FromMilliseconds(1000));

public void OnSubmitButtonClick()
{
    _throttle.RunAsync(async () =>
    {
        await SubmitDataAsync(); // nur erster Klick innerhalb 1 Sekunde wird verarbeitet
    });
}
```

---

## Fazit

| Verhalten             | Middleware       | Beschreibung                                  |
|----------------------|------------------|-----------------------------------------------|
| **Debounce** (letzter zählt) | `DebounceMiddleware` | Bricht alle alten Aufrufe ab, wartet 500ms    |
| **Throttle** (erster zählt)  | `ThrottleMiddleware` | Ignoriert weitere Aufrufe für X Millisekunden |

Beide Middleware-Varianten erhöhen die UI- und Netzwerk-Stabilität in mobilen Apps.

## Anwendung
- Buttons, die versehentlich mehrfach gedrückt werden
- Texteingaben mit Autocomplete
- Scroll-/Touch-Ereignisse, die stark frequentiert sind

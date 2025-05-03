# Concurrency Middleware in Xamarin.Android

## Zweck
Diese Middleware begrenzt gleichzeitige Zugriffe auf bestimmte Ressourcen oder kritische Abschnitte – ähnlich wie ein Semaphor oder eine Task-Queue. Sie kann z. B. verwendet werden, um Netzwerkzugriffe, Dateizugriffe oder Berechnungen zu serialisieren oder zu drosseln.

---

## Motivation
In mobilen Apps wie Xamarin.Android kann es wichtig sein:
- gleichzeitige Zugriffe auf SQLite oder SharedPreferences zu verhindern,
- API-Aufrufe sequenziell zu erzwingen (z. B. Rate Limiting),
- UI-sensible Operationen nacheinander ablaufen zu lassen.

---

## Beispiel: Einfache ConcurrencyMiddleware mit SemaphoreSlim

```csharp
public class ConcurrencyMiddleware
{
    private readonly SemaphoreSlim _semaphore;

    public ConcurrencyMiddleware(int maxConcurrency = 1)
    {
        _semaphore = new SemaphoreSlim(maxConcurrency, maxConcurrency);
    }

    public async Task<T> RunAsync<T>(Func<Task<T>> operation)
    {
        await _semaphore.WaitAsync();
        try
        {
            return await operation();
        }
        finally
        {
            _semaphore.Release();
        }
    }

    public async Task RunAsync(Func<Task> operation)
    {
        await _semaphore.WaitAsync();
        try
        {
            await operation();
        }
        finally
        {
            _semaphore.Release();
        }
    }
}
```

---

## Verwendung

```csharp
var middleware = new ConcurrencyMiddleware(1); // Single-threaded

await middleware.RunAsync(async () =>
{
    Console.WriteLine("Starte kritische Operation...");
    await Task.Delay(2000); // Simuliere Arbeit
    Console.WriteLine("Beende kritische Operation.");
});
```

---

## Praxisbezug in Xamarin.Android

- **Datenbankzugriffe (z. B. SQLite-net)**: Nur ein Schreibvorgang gleichzeitig erlaubt
- **Dateisystem-Zugriffe**: Konfliktfreies Schreiben/Lesen
- **Sensor-/Hardwarezugriffe**: Exklusive Steuerung
- **UI-nahe Dienste**: Verhindern, dass mehrere Navigationsaufrufe kollidieren

---

## Erweiterungsideen

- **Timeout-Support**: Abbrechen, wenn Zugriff zu lange dauert
- **Prioritätensystem**: Höher priorisierte Tasks bevorzugen
- **Warteschlangen-Logging**: Einsicht in blockierende Operationen

---

## Fazit

Concurrency Middleware ermöglicht die zentrale Steuerung paralleler Abläufe, wo Sicherheit, Konsistenz oder Ressourcenbegrenzung wichtig sind – ohne dass jeder Aufrufer sich darum kümmern muss.

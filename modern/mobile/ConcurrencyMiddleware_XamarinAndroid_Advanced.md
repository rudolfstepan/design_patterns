# Erweiterte Concurrency Middleware in Xamarin.Android

## Ziel
Diese Middleware begrenzt nicht nur gleichzeitige Zugriffe, sondern:
- unterstützt **Timeouts**
- erlaubt einfache **Prioritäten**
- bietet **Debug-Logging** bei Wartesituationen

---

## Beispiel: Erweiterte Middleware

```csharp
public class ConcurrencyMiddleware
{
    private readonly SemaphoreSlim _semaphore;
    private readonly int _maxConcurrency;

    public ConcurrencyMiddleware(int maxConcurrency = 1)
    {
        _maxConcurrency = maxConcurrency;
        _semaphore = new SemaphoreSlim(maxConcurrency, maxConcurrency);
    }

    public async Task<T> RunAsync<T>(Func<Task<T>> operation, string name = "", int priority = 0, TimeSpan? timeout = null)
    {
        var acquired = false;
        try
        {
            Console.WriteLine($"> [{name}] wartet mit Priorität {priority}...");

            if (timeout.HasValue)
                acquired = await _semaphore.WaitAsync(timeout.Value);
            else
            {
                await _semaphore.WaitAsync();
                acquired = true;
            }

            if (!acquired)
            {
                Console.WriteLine($"> [{name}] Timeout – Zugriff verweigert.");
                throw new TimeoutException($"[{name}] konnte nicht innerhalb der Zeit ausgeführt werden.");
            }

            Console.WriteLine($"> [{name}] gestartet...");
            return await operation();
        }
        finally
        {
            if (acquired)
            {
                Console.WriteLine($"> [{name}] abgeschlossen, gibt Semaphore frei.");
                _semaphore.Release();
            }
        }
    }

    public async Task RunAsync(Func<Task> operation, string name = "", int priority = 0, TimeSpan? timeout = null)
    {
        await RunAsync(async () =>
        {
            await operation();
            return true;
        }, name, priority, timeout);
    }
}
```

---

## Verwendung

```csharp
var middleware = new ConcurrencyMiddleware(maxConcurrency: 1);

await middleware.RunAsync(async () =>
{
    Console.WriteLine("Starte Task A");
    await Task.Delay(3000);
    Console.WriteLine("Beende Task A");
}, name: "Task A", priority: 1, timeout: TimeSpan.FromSeconds(5));
```

---

## Features

| Feature         | Beschreibung |
|----------------|--------------|
| `SemaphoreSlim` | Begrenzt gleichzeitige Tasks (z. B. 1 für Serialisierung) |
| `Timeout`       | Task wird abgebrochen, wenn Zugriff zu lange dauert       |
| `Name`          | Optionales Tagging für Logging/Analyse                    |
| `Priority`      | Wird derzeit nur protokolliert, kann für Warteschlangenlogik genutzt werden |

---

## Anwendungsszenarien

- **Dateizugriffe mit Konfliktvermeidung**
- **Hintergrund-Worker mit Zugriffsbeschränkung**
- **Synchronisierte REST-Aufrufe**
- **UI-Kritische Prozesse mit Timeoutabsicherung**

---

## Erweiterbar um:

- Warteschlangenstruktur mit echter Priorität
- Retry-Mechanismus bei Timeout
- Metriken für Performanceanalyse

---

## Fazit

Diese Middleware geht über einfaches Synchronisieren hinaus. Sie eignet sich gut zur Koordination und Überwachung kritischer Abläufe in mobilen Anwendungen – insbesondere dort, wo Nebenläufigkeit gezähmt werden muss.

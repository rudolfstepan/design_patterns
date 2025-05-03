# Hosted Services

## Zweck
Hintergrunddienste, die mit der Anwendung starten.

## Beispiel
```csharp
public class MyWorker : BackgroundService
{
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            Console.WriteLine("Running...");
            await Task.Delay(1000, stoppingToken);
        }
    }
}
```

## Praxisbezug
Für Scheduler, Queues, Hintergrundüberwachung in ASP.NET Core-Apps (z. B. E-Mail-Versand, Wartung).

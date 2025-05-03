# Hosted Service (Hintergrunddienste in ASP.NET Core)

## Zweck
Ermöglicht Hintergrundverarbeitung parallel zum Webserver-Betrieb, z. B. für Scheduler, Wartung, E-Mail-Versand oder Queues.

## Vorteile
- Leichtgewichtig und integriert in ASP.NET Core
- Lebenszyklussteuerung über Dependency Injection
- Parallele Verarbeitung außerhalb des HTTP-Kontexts

## Nachteile
- Kein automatisches Recovery bei Ausfall
- Muss explizit mit Logging und Fehlerbehandlung versehen werden

## Beispiel
```csharp
public class MyWorker : BackgroundService
{
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            Console.WriteLine("Service läuft...");
            await Task.Delay(5000, stoppingToken);
        }
    }
}

// Registrierung in Program.cs
builder.Services.AddHostedService<MyWorker>();
```

## Praxisbezug
Ideal für:
- wiederkehrende Aufgaben (CRON)
- Service-Bus-Verarbeitung (RabbitMQ, Kafka)
- Cleanup- oder Indexierungsjobs

# Dependency Injection

## Zweck
Dependency Injection (DI) ermöglicht die Trennung von Objektinstanziierung und Verwendung. Abhängigkeiten werden einem Objekt von außen übergeben statt innerhalb erzeugt zu werden.

## Vorteile
- Entkoppelte Komponenten
- Leichtere Testbarkeit (Mocks, Stubs)
- Klare Verantwortlichkeiten
- Ermöglicht Inversion of Control (IoC)

## Nachteile
- Kann zur Overhead-Komplexität führen
- Fehlkonfigurationen meist zur Laufzeit sichtbar
- Einstiegshürde bei komplexen DI-Containern

## Varianten
- Konstruktorinjektion
- Property-/Setter-Injektion
- Methoden-Injektion

## Beispiel in C#
```csharp
public interface ILogger
{
    void Log(string message);
}

public class ConsoleLogger : ILogger
{
    public void Log(string message) => Console.WriteLine(message);
}

public class OrderService
{
    private readonly ILogger _logger;
    public OrderService(ILogger logger) => _logger = logger;

    public void PlaceOrder(string product) => _logger.Log($"Order placed: {product}");
}

// Verwendung
ILogger logger = new ConsoleLogger();
OrderService service = new OrderService(logger);
service.PlaceOrder("Widget");
```

## Praxisbezug
- ASP.NET Core integriert ein leichtgewichtiges DI-System (`builder.Services.AddTransient<T>()`)
- Verwendet für Controller, Services, Repositories, BackgroundServices etc.

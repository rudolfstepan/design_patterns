# Proxy Pattern

## Zweck
Stellt einen Stellvertreter für ein anderes Objekt bereit, um dessen Zugriff zu kontrollieren.

## Motivation
Verwendbar für Zugriffssteuerung, Lazy Loading oder Logging.

## Beispiel in C#
```csharp
public interface IService { void Operation(); }

public class RealService : IService
{
    public void Operation() => Console.WriteLine("Echte Operation");
}

public class ProxyService : IService
{
    private RealService _real;
    public void Operation()
    {
        _real ??= new RealService();
        Console.WriteLine("Proxy davor");
        _real.Operation();
    }
}
```

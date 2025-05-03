# Service Locator

## Zweck
Zentralisiert die Bereitstellung von Abhängigkeiten über eine globale Zugriffsschnittstelle.

## Beispiel
```csharp
public static class ServiceLocator
{
    private static readonly Dictionary<Type, object> _services = new();

    public static void Register<T>(T service) => _services[typeof(T)] = service;
    public static T Get<T>() => (T)_services[typeof(T)];
}

// Verwendung
ServiceLocator.Register<IMessageService>(new EmailService());
var service = ServiceLocator.Get<IMessageService>();
```

## Praxisbezug
Veraltet im Vergleich zu Dependency Injection – erschwert Testbarkeit und klare Abhängigkeiten.

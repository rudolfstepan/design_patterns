# Service Locator

## Zweck
Bietet eine zentrale Möglichkeit, auf Abhängigkeiten zuzugreifen – ähnlich einem globalen Container.

## Vorteile
- Einfachheit für kleine Projekte
- Zentraler Zugriffspunkt

## Nachteile
- Versteckte Abhängigkeiten
- Schwer testbar (kein klarer Konstruktorvertrag)
- Wird oft als Anti-Pattern betrachtet

## Beispiel
```csharp
public static class ServiceLocator
{
    private static readonly Dictionary<Type, object> _services = new();

    public static void Register<T>(T service) => _services[typeof(T)] = service;
    public static T Get<T>() => (T)_services[typeof(T)];
}
```

## Praxisbezug
Nur in Ausnahmefällen empfehlenswert (z. B. bei Legacy-Code oder vorübergehender Migrationslösung).

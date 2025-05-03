# Null Object Pattern

## Zweck
Vermeidet `null` durch eine Standardimplementierung.

## Beispiel
```csharp
public class NullLogger : ILogger
{
    public void Log(string message) { /* nichts tun */ }
}
```

## Praxisbezug
Ersatz für Logging, Konfiguration oder Validierung, wenn keine Aktion erwünscht ist.

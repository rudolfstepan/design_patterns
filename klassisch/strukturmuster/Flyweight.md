# Flyweight Pattern

## Zweck
Reduziert Speicherverbrauch, indem viele ähnliche Objekte ihren gemeinsamen Zustand teilen.

## Motivation
Effizient bei vielen kleinen Objekten (z. B. Zeichen in einem Editor).

## Beispiel in C#
```csharp
public class Character
{
    private readonly char _symbol;
    public Character(char symbol) => _symbol = symbol;
    public void Display() => Console.Write(_symbol);
}
```

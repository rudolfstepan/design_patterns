# Prototype

Prototype

Beschreibung:
Ermöglicht das Kopieren von Objekten, ohne deren konkreten Klassen zu kennen.

C# Beispiel:
```csharp
public abstract class Prototype
{
    public abstract Prototype Clone();
}
```

```csharp
public class ConcretePrototype : Prototype
{
    public int Data;
    public override Prototype Clone()
    {
        return (Prototype)this.MemberwiseClone();
    }
}
```

## Praxisbeispiel

```csharp
// Beispiel: Klonen eines Dokuments
Document original = new Document { Title = "Report", Content = "..." };
Document copy = original.Clone();
```
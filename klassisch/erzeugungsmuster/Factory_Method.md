# Factory Method

Factory Method

Beschreibung:
Definiert eine Schnittstelle zur Erstellung eines Objekts, lässt aber die Unterklassen entscheiden, welche Klasse instanziiert wird.

C# Beispiel:
```csharp
public abstract class Creator
{
    public abstract IProduct FactoryMethod();
}
```

```csharp
public class ConcreteCreator : Creator
{
    public override IProduct FactoryMethod()
    {
        return new ConcreteProduct();
    }
}
```

```csharp
public interface IProduct { }
```

```csharp
public class ConcreteProduct : IProduct { }

```
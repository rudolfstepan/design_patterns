# Specification Pattern

## Zweck
Definiert wiederverwendbare, kombinierbare Geschäftsregeln als Objekte.

## Beispiel
```csharp
public interface ISpecification<T>
{
    Expression<Func<T, bool>> Criteria { get; }
}
```

## Praxisbezug
Wird eingesetzt, um LINQ-Filterkriterien testbar und wiederverwendbar zu machen.

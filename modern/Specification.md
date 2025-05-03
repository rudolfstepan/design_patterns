# Specification Pattern

## Zweck
Ermöglicht die Wiederverwendung und Kombination von Kriterien zur Filterung oder Entscheidungsfindung.

## Vorteile
- Kapselung von Geschäftsregeln
- Wiederverwendbarkeit
- Testbarkeit von Filterlogik

## Nachteile
- Kann für einfache Fälle unnötig erscheinen
- Kombination mehrerer Spezifikationen kann komplex werden

## Beispiel
```csharp
public interface ISpecification<T>
{
    Expression<Func<T, bool>> Criteria { get; }
}

public class ActiveCustomersSpec : ISpecification<Customer>
{
    public Expression<Func<Customer, bool>> Criteria => c => c.IsActive;
}
```

## Praxisbezug
Verwendet z. B. in LINQ-Queries, DDD, APIs mit Filterfunktionen.

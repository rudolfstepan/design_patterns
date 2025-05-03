# Unit of Work

## Zweck
Fasst mehrere Datenbankoperationen zu einer Transaktion zusammen.

## Beispiel
```csharp
public interface IUnitOfWork
{
    IProductRepository Products { get; }
    Task SaveChangesAsync();
}
```

## Praxisbezug
Wird oft mit Repository Pattern kombiniert – etwa bei `SaveChanges()` im Entity Framework DbContext.

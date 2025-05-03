# Unit of Work

## Zweck
Bündelt Operationen über mehrere Repositories in einer Transaktion.

## Vorteile
- Koordination von Änderungen
- Atomare Persistenz
- Trennung der Geschäftslogik von der Datenzugriffslogik

## Nachteile
- Zusätzlicher Abstraktionsaufwand
- Bei reinem EF-Core oft überflüssig (da DbContext bereits Unit of Work ist)

## Beispiel
```csharp
public interface IUnitOfWork
{
    ICustomerRepository Customers { get; }
    Task SaveAsync();
}

public class EfUnitOfWork : IUnitOfWork
{
    private readonly MyDbContext _ctx;
    public EfUnitOfWork(MyDbContext ctx) => _ctx = ctx;

    public ICustomerRepository Customers => new EfCustomerRepository(_ctx);
    public Task SaveAsync() => _ctx.SaveChangesAsync();
}
```

## Praxisbezug
Empfohlen in komplexeren Anwendungen mit mehreren Datenbankoperationen pro Geschäftsfall.

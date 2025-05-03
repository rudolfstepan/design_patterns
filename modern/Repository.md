# Repository Pattern

## Zweck
Abstrahiert den Datenzugriff, sodass die Geschäftslogik keine Kenntnis über die konkrete Datenquelle benötigt.

## Vorteile
- Trennung von Datenlogik und Businesslogik
- Austauschbarkeit der Persistenzschicht
- Besser testbar mit In-Memory-Repositories

## Nachteile
- Kann redundant zur ORM-Funktionalität sein (Over-Engineering)
- Extra-Komplexität bei kleinen Projekten

## Beispiel
```csharp
public interface ICustomerRepository
{
    Customer GetById(int id);
    void Add(Customer customer);
}

public class EfCustomerRepository : ICustomerRepository
{
    private readonly MyDbContext _ctx;
    public EfCustomerRepository(MyDbContext ctx) => _ctx = ctx;

    public Customer GetById(int id) => _ctx.Customers.Find(id);
    public void Add(Customer customer) => _ctx.Customers.Add(customer);
}
```

## Praxisbezug
Standard in Domain-Driven Design, weit verbreitet in Kombination mit Unit of Work.

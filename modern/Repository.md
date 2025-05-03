# Repository Pattern

## Zweck
Kapselt den Datenzugriff und stellt eine domänenspezifische Schnittstelle zur Verfügung.

## Beispiel
```csharp
public interface IProductRepository
{
    Product GetById(int id);
    IEnumerable<Product> GetAll();
    void Add(Product product);
}
```

## Praxisbezug
Wird in Kombination mit Entity Framework Core verwendet, um die Datenzugriffsschicht von der Geschäftslogik zu trennen.

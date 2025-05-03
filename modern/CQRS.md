# CQRS – Command Query Responsibility Segregation

## Zweck
CQRS trennt Leseoperationen (Query) von Schreiboperationen (Command), um bessere Skalierung, Performance und Sicherheit zu erreichen.

## Vorteile
- Trennung von Verantwortung
- Optimierung von Lese-/Schreibpfaden getrennt möglich
- Unterstützung für Event Sourcing
- Einfacheres Sicherheitsmodell (nur Commands schreiben)

## Nachteile
- Höhere Komplexität
- Synchronisation von Read-/Write-Modellen erforderlich
- Nicht für einfache CRUD-Apps notwendig

## Struktur
- **Command Handler**: führt Änderungen aus
- **Query Handler**: liest optimierte Datenmodelle
- **Read Model**: oft materialisierte Projektionen
- **Write Model**: Domain-Model mit Logik

## Beispiel
```csharp
public record CreateCustomerCommand(string Name) : IRequest<Guid>;

public class CreateCustomerHandler : IRequestHandler<CreateCustomerCommand, Guid>
{
    public async Task<Guid> Handle(CreateCustomerCommand request, CancellationToken ct)
    {
        // Persistiere neuen Kunden
        return Guid.NewGuid();
    }
}

public record GetCustomerQuery(Guid Id) : IRequest<Customer>;

public class GetCustomerHandler : IRequestHandler<GetCustomerQuery, Customer>
{
    public async Task<Customer> Handle(GetCustomerQuery request, CancellationToken ct)
    {
        // Hole Kunden aus Read DB
        return new Customer { Id = request.Id, Name = "Alice" };
    }
}
```

## Praxisbezug
Verwendet in Event-getriebenen Microservices, Reporting-Systemen oder bei Performance-kritischen Anwendungen.

# Mediator Pattern (modern)

## Zweck
Kapselt Kommunikation zwischen Komponenten zentral.

## Beispiel (MediatR in .NET)
```csharp
public record CreateOrderCommand(string ProductId) : IRequest<Guid>;

public class CreateOrderHandler : IRequestHandler<CreateOrderCommand, Guid>
{
    public Task<Guid> Handle(CreateOrderCommand request, CancellationToken ct)
    {
        // Logik hier
        return Task.FromResult(Guid.NewGuid());
    }
}
```

## Praxisbezug
Gängiges Pattern in ASP.NET Core mit MediatR zur Trennung von Business-Logik und Controller.

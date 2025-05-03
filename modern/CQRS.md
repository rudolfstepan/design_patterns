# CQRS – Command Query Responsibility Segregation

## Zweck
Trennt Lese- und Schreibmodelle zur besseren Skalierung und Wartbarkeit.

## Beispiel
```csharp
public class CreateOrderCommand { public string ProductId; }
public class GetOrdersQuery { public int CustomerId; }
```

## Praxisbezug
Verwendet in verteilten Systemen und bei Event Sourcing – z.B. in Event-getriebenen Microservices.

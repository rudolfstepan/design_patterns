# Event Sourcing

## Zweck
Beim Event Sourcing wird der Zustand einer Anwendung nicht direkt als Objektstruktur gespeichert, sondern aus einer Sequenz von Ereignissen (Events) wiederhergestellt. Jedes Event beschreibt eine Veränderung, die an einem Aggregat stattgefunden hat.

## Vorteile
- Komplette Nachvollziehbarkeit und Audit-Logik
- "Zeitreisen" im Systemzustand sind möglich
- Ideal für Systeme mit hoher Änderungsfrequenz oder regulatorischer Nachweispflicht
- Unterstützt Event-getriebene Architekturen und CQRS

## Nachteile
- Komplexere Persistenzlogik
- Erfordert Event-Design und Versionierung bei Änderungen
- Rehydrierung kann aufwändig sein, bei großen Event-Mengen

## Struktur

- **Event Store**: Persistiert alle Events chronologisch
- **Aggregate**: Domänenobjekte, die auf Basis der Events wiederhergestellt werden
- **Event Handler**: Reagieren auf gespeicherte Events, erzeugen ggf. Read-Modelle

## Beispiel in C#

```csharp
public abstract class Event
{
    public DateTime Timestamp { get; init; } = DateTime.UtcNow;
}

public class AccountCreated : Event
{
    public Guid AccountId { get; init; }
    public string Owner { get; init; }
}

public class MoneyDeposited : Event
{
    public Guid AccountId { get; init; }
    public decimal Amount { get; init; }
}

public class BankAccount
{
    public Guid Id { get; private set; }
    public decimal Balance { get; private set; }

    public void Apply(Event e)
    {
        switch (e)
        {
            case AccountCreated created:
                Id = created.AccountId;
                Balance = 0;
                break;
            case MoneyDeposited deposit:
                Balance += deposit.Amount;
                break;
        }
    }

    public void Rehydrate(IEnumerable<Event> history)
    {
        foreach (var e in history)
            Apply(e);
    }
}
```

## Praxisbezug

### Typische Einsatzbereiche
- **Finanzsysteme**: Buchungen, Transaktionen, Rechnungen
- **Audit-Anwendungen**: Jeder Zustand ist reproduzierbar
- **Microservices**: Zustandslose Services speichern nur Events

### Tools & Frameworks
- EventStoreDB (speziell für Event Sourcing)
- Marten (für PostgreSQL + .NET)
- Axon, Kafka (indirekt durch Event-Prozesse)

### Beispielhafte Anwendung
Ein Onlineshop speichert jede Warenkorb-Änderung als Event:
- `ItemAddedToCart`
- `ItemRemovedFromCart`
- `CartCheckedOut`

Der Zustand des Warenkorbs kann jederzeit aus diesen Events berechnet werden. Änderungen an der Interpretation der Events (z. B. neue Rabattregeln) wirken rückwirkend.

## Fazit
Event Sourcing ist ein mächtiges, aber auch komplexes Muster. Es lohnt sich vor allem bei Systemen, die von vollständiger Nachverfolgbarkeit, asynchroner Verarbeitung oder komplexer Historie profitieren.

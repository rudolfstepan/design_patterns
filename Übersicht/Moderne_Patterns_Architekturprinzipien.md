# Architekturprinzipien und moderne Patterns in C#

Diese Übersicht enthält moderne Architekturprinzipien und Design-Patterns, die nicht Teil der klassischen GoF-Muster sind, aber in modernen C#- und .NET-Projekten häufig Anwendung finden.

---

## Service Locator

### Zweck
Zentralisierte Bereitstellung von Abhängigkeiten, bei der Objekte ihre Abhängigkeiten nicht direkt übergeben bekommen, sondern selbst über einen Locator abrufen.

### Nachteile
- Versteckte Abhängigkeiten
- Schwer testbar
- Anti-Pattern, wenn überstrapaziert

### Beispiel
```csharp
var service = ServiceLocator.Get<IMessageService>();
```

---

## Repository Pattern

### Zweck
Abstraktion der Datenzugriffsschicht (z. B. EF Core), um Datenzugriffe zu kapseln und Geschäftslogik von Datenbankdetails zu trennen.

### Beispiel
```csharp
public interface ICustomerRepository
{
    Customer GetById(int id);
    void Add(Customer customer);
}
```

---

## Unit of Work

### Zweck
Koordiniert mehrere Repositorys und bündelt Datenbankoperationen in einer Transaktion.

### Beispiel
```csharp
public interface IUnitOfWork
{
    ICustomerRepository Customers { get; }
    Task SaveChangesAsync();
}
```

---

## Specification Pattern

### Zweck
Ermöglicht die Kapselung wiederverwendbarer Geschäftsregeln oder Filterlogik.

### Beispiel
```csharp
public interface ISpecification<T>
{
    Expression<Func<T, bool>> Criteria { get; }
}
```

---

## CQRS – Command Query Responsibility Segregation

### Zweck
Trennung von Lese- und Schreibmodellen für bessere Skalierbarkeit, Wartbarkeit und klare Verantwortlichkeiten.

### Beispiel
```csharp
public class CreateOrderCommand { ... }
public class GetOrdersQuery { ... }
```

---

## Event Sourcing

### Zweck
Speichert Systemzustände nicht direkt, sondern durch eine Ereigniskette. Der Zustand wird aus der Ereignisgeschichte rekonstruiert.

### Beispiel
```csharp
public class OrderCreatedEvent { ... }
public class ProductAddedEvent { ... }
```

---

## Mediator Pattern (modern)

### Zweck
Zentralisiert Kommunikation zwischen Komponenten und reduziert direkte Abhängigkeiten.

### Beispiel (MediatR in .NET)
```csharp
public record CreateOrderCommand(string ProductId) : IRequest<Guid>;
```

---

## Null Object Pattern

### Zweck
Vermeidung von `null`, indem eine funktionslose Standardimplementierung verwendet wird.

### Beispiel
```csharp
public class NullLogger : ILogger
{
    public void Log(string msg) { /* nichts tun */ }
}
```

---

## Strategy Pattern (modern via Delegate)

### Zweck
Austauschbare Verhaltensweisen über Delegates statt Klassen.

### Beispiel
```csharp
Func<int, int> strategy = x => x * 2;
```

---

## Options Pattern (ASP.NET Core)

### Zweck
Stark typisierte Konfiguration mit Bindung an POCO-Klassen.

### Beispiel
```csharp
public class MySettings
{
    public string ApiKey { get; set; }
}
```

---

## Middleware Pattern (ASP.NET Core)

### Zweck
Verkettete Verarbeitungsschritte für HTTP-Anfragen.

### Beispiel
```csharp
app.Use(async (context, next) =>
{
    // Vor dem nächsten Middleware
    await next.Invoke();
    // Danach
});
```

---

## Hosted Services

### Zweck
Langlaufende Hintergrunddienste im ASP.NET Core-Umfeld.

### Beispiel
```csharp
public class MyWorker : BackgroundService
{
    protected override Task ExecuteAsync(CancellationToken stoppingToken) { ... }
}
```

---

## HttpClientFactory / LoggerFactory

### Zweck
Zentrale Erstellung von `HttpClient` und `ILogger`-Instanzen mit zentraler Verwaltung.

### Beispiel
```csharp
var client = _httpClientFactory.CreateClient("MyApi");
```

---

## Fazit

Diese modernen Patterns sind essenziell für die heutige Softwarearchitektur in C#. Sie fördern Wartbarkeit, Testbarkeit und Flexibilität moderner Anwendungen.

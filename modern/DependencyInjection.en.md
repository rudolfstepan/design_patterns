# Dependency Injection

## Intent
Separate the creation of an object's dependencies from its behavior, allowing the system to be more modular, testable, and loosely coupled.

## Also Known As
DI, Inversion of Control (IoC)

## Motivation
In traditional object-oriented design, objects are responsible for obtaining their dependencies. This leads to tight coupling and difficulties in testing or reusing components.

Dependency Injection inverts this control: instead of the object creating its dependencies, they are provided externally.

## Applicability
Use the Dependency Injection pattern when:
- You want to decouple components from their dependencies
- You need to facilitate testing with mock objects
- You aim to increase maintainability and flexibility

## Structure
The pattern involves:
- A service or dependency that a client depends on
- An injector or container that knows how to construct services
- A client that receives its dependencies through constructor, setter, or method injection

## Participants
- **Client**: The class that depends on a service
- **Service**: The dependency to be injected
- **Injector**: Responsible for constructing and providing dependencies

## Consequences
### Pros
- Reduces coupling between components
- Increases code reusability and testability
- Promotes Single Responsibility Principle

### Cons
- Can introduce complexity if overused
- May make tracing dependencies harder in large systems

## Implementation

### Example in C#

```csharp
// The service interface
public interface IMessageService
{
    void Send(string message);
}

// A concrete implementation
public class EmailService : IMessageService
{
    public void Send(string message)
    {
        Console.WriteLine("Sending Email: " + message);
    }
}

// The client that uses the service
public class Notification
{
    private readonly IMessageService _messageService;

    // Constructor injection
    public Notification(IMessageService messageService)
    {
        _messageService = messageService;
    }

    public void SendAlert(string message)
    {
        _messageService.Send(message);
    }
}

// Example usage
public class Program
{
    public static void Main()
    {
        IMessageService service = new EmailService();
        Notification notification = new Notification(service);
        notification.SendAlert("Pattern implemented successfully.");
    }
}
```

## Variants
- Constructor Injection
- Setter Injection
- Interface Injection (less common)

## Known Uses
- ASP.NET Core built-in dependency injection
- Autofac, Unity Container, Ninject

## Related Patterns
- Service Locator
- Factory
- Strategy


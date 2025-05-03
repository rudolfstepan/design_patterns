# Chain of Responsibility

Chain of Responsibility

Beschreibung:
Vermeidet die Kopplung des Senders einer Anfrage an deren Empfänger, indem mehr als ein Objekt die Möglichkeit erhält, die Anfrage zu bearbeiten.

C# Beispiel:
```csharp
public abstract class Handler
{
    protected Handler successor;
    public void SetSuccessor(Handler successor)
    {
        this.successor = successor;
    }
    
	public abstract void HandleRequest(int request);
}
```

```csharp
public class ConcreteHandler1 : Handler
{
    public override void HandleRequest(int request)
    {
        if (request < 10)
            Console.WriteLine($"{GetType().Name} handled request {request}");
        else
            successor?.HandleRequest(request);
    }
}
```

```csharp
public class ConcreteHandler2 : Handler
{
    public override void HandleRequest(int request)
    {
        if (request < 20)
            Console.WriteLine($"{GetType().Name} handled request {request}");
        else
            successor?.HandleRequest(request);
    }
}

## Praxisbeispiel

```csharp
// Logging-Kette mit verschiedenen Ebenen
public class Logger
{
    private readonly LogLevel _level;
    private Logger _next;

    public Logger(LogLevel level) => _level = level;

    public Logger SetNext(Logger next)
    {
        _next = next;
        return next;
    }

    public void Log(string message, LogLevel level)
    {
        if (level >= _level)
            Console.WriteLine($"{_level}: {message}");
        _next?.Log(message, level);
    }
}
public enum LogLevel { Debug, Info, Warning, Error }
```
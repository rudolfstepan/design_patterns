# Command

Command

Beschreibung:
Kapselt eine Anfrage als Objekt, wodurch sich die Parameter der Clients unterschiedlich konfigurieren lassen.

C# Beispiel:
```csharp
public interface ICommand
{
    void Execute();
}
```

```csharp
public class Receiver
{
    public void Action() => Console.WriteLine("Ausführung durch Empfänger");
}
```

```csharp
public class ConcreteCommand : ICommand
{
    private Receiver _receiver;
    public ConcreteCommand(Receiver receiver) => _receiver = receiver;
    public void Execute() => _receiver.Action();
}
```

```csharp
public class Invoker
{
    private ICommand _command;
    public void SetCommand(ICommand command) => _command = command;
    public void ExecuteCommand() => _command.Execute();
}
```
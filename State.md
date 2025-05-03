# State

State

Beschreibung:
Ermöglicht einem Objekt, sein Verhalten zu ändern, wenn sich sein interner Zustand ändert.

C# Beispiel:
```csharp
public interface IState
{
    void Handle(Context context);
}
```

```csharp
public class ConcreteStateA : IState
{
    public void Handle(Context context)
    {
        Console.WriteLine("Zustand A verarbeitet.");
        context.State = new ConcreteStateB();
    }
}
```

```csharp
public class ConcreteStateB : IState
{
    public void Handle(Context context)
    {
        Console.WriteLine("Zustand B verarbeitet.");
        context.State = new ConcreteStateA();
    }
}
```

```csharp
public class Context
{
    public IState State { get; set; }
    public Context(IState state) => State = state;
    public void Request() => State.Handle(this);
}
```

## Praxisbeispiel

```csharp
// Beispiel: AudioPlayer mit Zuständen "Play", "Pause", "Stop"
player.SetState(new PlayState());
player.Request();
```
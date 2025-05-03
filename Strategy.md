# Strategy

Strategy

Beschreibung:
Definiert eine Familie von Algorithmen, kapselt jeden und macht sie untereinander austauschbar.

C# Beispiel:
```csharp
public interface IStrategy
{
    void Execute();
}
```

```csharp
public class ConcreteStrategyA : IStrategy
{
    public void Execute() => Console.WriteLine("Strategie A");
}
```

```csharp
public class ConcreteStrategyB : IStrategy
{
    public void Execute() => Console.WriteLine("Strategie B");
}
```

```csharp
public class Context
{
    private IStrategy _strategy;
    public Context(IStrategy strategy) => _strategy = strategy;
    public void ExecuteStrategy() => _strategy.Execute();
}
```

## Praxisbeispiel

```csharp
// Beispiel: Sortierstrategien
Context context = new Context(new QuickSort());
context.ExecuteStrategy(new[] { 5, 2, 8 });
```
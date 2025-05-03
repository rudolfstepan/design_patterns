# Interpreter

Interpreter

Beschreibung:
Gibt eine Grammatik für eine Sprache an und definiert einen Interpreten, der die Sätze der Sprache interpretiert.

C# Beispiel:
```csharp
public interface IExpression
{
    int Interpret();
}
```

```csharp
public class NumberExpression : IExpression
{
    private int _number;
    public NumberExpression(int number) => _number = number;
    public int Interpret() => _number;
}
```

```csharp
public class AddExpression : IExpression
{
    private IExpression _left, _right;
    public AddExpression(IExpression left, IExpression right)
    {
        _left = left; _right = right;
    }

    public int Interpret() => _left.Interpret() + _right.Interpret();
}
```

## Praxisbeispiel

```csharp
// Kontextuelle Interpretation einfacher Rechenausdrücke
IExpression expr = new AddExpression(
    new NumberExpression(5),
    new AddExpression(new NumberExpression(3), new NumberExpression(2)));

Console.WriteLine(expr.Interpret()); // 10
```
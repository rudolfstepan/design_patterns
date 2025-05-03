# Builder

Builder

Beschreibung:
Trennt die Konstruktion eines komplexen Objekts von seiner Repräsentation, sodass derselbe Konstruktionsprozess verschiedene Darstellungen erzeugen kann.

C# Beispiel:
```csharp
public class Product
{
    public List Parts = new List();
    public void Show() => Parts.ForEach(Console.WriteLine);
}
```

```csharp
public abstract class Builder
{
    public abstract void BuildPartA();
    public abstract void BuildPartB();
    public abstract Product GetResult();
}
```

```csharp
public class ConcreteBuilder : Builder
{
    private Product _product = new Product();
    public override void BuildPartA() => _product.Parts.Add("Teil A");
    public override void BuildPartB() => _product.Parts.Add("Teil B");
    public override Product GetResult() => _product;
}
```

## Praxisbeispiel

```csharp
// Beispiel: HTML-Dokument bauen
public class HtmlBuilder
{
    private StringBuilder _sb = new StringBuilder();

    public HtmlBuilder AddElement(string tag, string content)
    {
        _sb.AppendLine($"<{tag}>{content}</{tag}>");
        return this;
    }

    public string Build() => _sb.ToString();
}
```
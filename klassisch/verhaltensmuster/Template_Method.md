# Template Method

Template Method

Beschreibung:
Definiert das Skelett eines Algorithmus in einer Methode, wobei einige Schritte von Unterklassen implementiert werden.

C# Beispiel:
```csharp
public abstract class AbstractClass
{
    public void TemplateMethod()
    {
        Step1();
        Step2();
        Step3();
    }

    protected abstract void Step1();
    protected abstract void Step2();
    protected virtual void Step3() => Console.WriteLine("Standard Schritt 3");
}
```

```csharp
public class ConcreteClass : AbstractClass
{
    protected override void Step1() => Console.WriteLine("Schritt 1");
    protected override void Step2() => Console.WriteLine("Schritt 2");
}
```

## Praxisbeispiel

```csharp
// Beispiel: Berichtserstellung mit fixem Ablauf, aber variablem Inhalt
Report report = new SalesReport();
report.Generate();
```
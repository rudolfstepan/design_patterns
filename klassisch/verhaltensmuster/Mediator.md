# Mediator Pattern

## Zweck
Vermittelt Kommunikation zwischen Objekten, ohne dass diese direkt gekoppelt sind.

## Motivation
Reduziert die Komplexität bei stark vernetzten Komponenten.

## Beispiel in C#
```csharp
public interface IMediator
{
    void Notify(object sender, string ev);
}

public class ConcreteMediator : IMediator
{
    public ComponentA A { get; set; }
    public ComponentB B { get; set; }

    public void Notify(object sender, string ev)
    {
        if (ev == "A") B.DoSomething();
    }
}

public class ComponentA
{
    public IMediator Mediator { get; set; }
    public void Trigger() => Mediator.Notify(this, "A");
}

public class ComponentB
{
    public void DoSomething() => Console.WriteLine("B reagiert auf A");
}
```

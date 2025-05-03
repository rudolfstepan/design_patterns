# Bridge

Bridge

Beschreibung:
Das Bridge-Pattern dient dazu, eine Abstraktion (z. B. eine Oberklasse) von ihrer Implementierung zu entkoppeln, sodass beide unabhängig voneinander weiterentwickelt werden können. Dies ist besonders nützlich, wenn sich sowohl die Abstraktion als auch die Implementierung häufig ändern oder in mehreren Varianten existieren.

Lehrbuch-Beispiel in C#:
Hier wird eine einfache Implementierung gezeigt, bei der zwei Hierarchien voneinander getrennt sind.

```csharp
public interface IImplementor
{
    void OperationImpl();
}
```

```csharp
public class ConcreteImplementorA : IImplementor
{
    public void OperationImpl() => Console.WriteLine("Implementierung A");
}
```

```csharp
public abstract class Abstraction
{
    protected IImplementor implementor;
    protected Abstraction(IImplementor impl) => implementor = impl;

    public abstract void Operation();
}
```

```csharp
public class RefinedAbstraction : Abstraction
{
    public RefinedAbstraction(IImplementor impl) : base(impl) {}
    public override void Operation() => implementor.OperationImpl();
}
```

Praxisnahes Beispiel:
Stellen wir uns ein Darstellungsframework vor, in dem unterschiedliche Geräte (z. B. Drucker oder Bildschirme) unabhängig von der Form (z. B. Kreis oder Rechteck) arbeiten sollen.

```csharp
public interface IRenderer
{
    void Render(string shapeName);
}
```

```csharp
public class ScreenRenderer : IRenderer
{
    public void Render(string shapeName)
    {
        Console.WriteLine($"Rendering {shapeName} auf dem Bildschirm.");
    }
}
```

```csharp
public class PrinterRenderer : IRenderer
{
    public void Render(string shapeName)
    {
        Console.WriteLine($"Rendering {shapeName} auf dem Drucker.");
    }
}
```

```csharp
public abstract class Shape
{
    protected IRenderer renderer;
    protected Shape(IRenderer renderer) => this.renderer = renderer;
    public abstract void Draw();
}
```

```csharp
public class Circle : Shape
{
    public Circle(IRenderer renderer) : base(renderer) {}
    public override void Draw() => renderer.Render("Kreis");
}
```

```csharp
public class Rectangle : Shape
{
    public Rectangle(IRenderer renderer) : base(renderer) {}
    public override void Draw() => renderer.Render("Rechteck");
}
```

```csharp
// Anwendung:
public class App
{
    public static void Main()
    {
        Shape screenCircle = new Circle(new ScreenRenderer());
        Shape printRectangle = new Rectangle(new PrinterRenderer());

        screenCircle.Draw();     // Rendering Kreis auf dem Bildschirm.
        printRectangle.Draw();   // Rendering Rechteck auf dem Drucker.
    }
}
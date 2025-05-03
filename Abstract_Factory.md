# Abstract Factory

## Beschreibung

Ermöglicht die Erstellung von Familien verwandter oder abhängiger Objekte, ohne deren konkrete Klassen zu spezifizieren.

## C# Beispiel

```csharp
public interface IButton
{
    void Paint();
}
````

```csharp
public class WinButton : IButton
{
    public void Paint() => Console.WriteLine("Windows Button");
}
```

```csharp
public class MacButton : IButton
{
    public void Paint() => Console.WriteLine("Mac Button");
}
```

```csharp
public interface IGUIFactory
{
    IButton CreateButton();
}
```

```csharp
public class WinFactory : IGUIFactory
{
    public IButton CreateButton() => new WinButton();
}
```

```csharp
public class MacFactory : IGUIFactory
{
    public IButton CreateButton() => new MacButton();
}
```
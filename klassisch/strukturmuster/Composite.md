# Composite

Composite

Beschreibung:
Stellt Baumstrukturen dar, um Teil-Ganzes-Hierarchien darzustellen. Ermöglicht die gleiche Behandlung von Einzelobjekten und Objektgruppen.

C# Beispiel:
```csharp
public abstract class Component
{
    public string Name;
    public Component(string name) => Name = name;
    public abstract void Display(int depth);
}
```

```csharp
public class Leaf : Component
{
    public Leaf(string name) : base(name) { }
    public override void Display(int depth) => Console.WriteLine(new string('-', depth) + Name);
}
```

```csharp
public class Composite : Component
{
    private List_children = new List();
    public Composite(string name) : base(name) { }

    public void Add(Component component) => _children.Add(component);
    public override void Display(int depth)
    {
        Console.WriteLine(new string('-', depth) + Name);

        foreach (var component in _children)
        component.Display(depth + 2);
    }
}

## Praxisbeispiel

```csharp
// Beispiel: Menüstruktur
Component menu = new Composite("Hauptmenü");
menu.Add(new Leaf("Start"));
menu.Add(new Leaf("Einstellungen"));

Component sub = new Composite("Extras");
sub.Add(new Leaf("Tools"));
sub.Add(new Leaf("Hilfe"));

menu.Add(sub);
menu.Display(1);
```
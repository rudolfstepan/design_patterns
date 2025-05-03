# Iterator

Iterator

Beschreibung:
Stellt eine Möglichkeit bereit, die Elemente eines Aggregats ohne Offenlegung der zugrunde liegenden Repräsentation zu durchlaufen.

C# Beispiel:
```csharp
public interface IIterator
{
    bool HasNext();
    object Next();
}
```

```csharp
public class Aggregate
{
    private List_items = new List();
    public void Add(object item) => _items.Add(item);
    public IIterator GetIterator() => new ConcreteIterator(_items);
}
```

```csharp
public class ConcreteIterator : IIterator
{
    private List_items;
    private int _position = 0;

    public ConcreteIterator(List items) => _items = items;

    public bool HasNext() => _position < _items.Count;
    public object Next() => _items[_position++];
}
```
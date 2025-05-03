# Memento

Memento

Beschreibung:
Erfasst und externalisiert den internen Zustand eines Objekts, ohne dessen Kapselung zu verletzen, damit das Objekt später in diesen Zustand zurückversetzt werden kann.

C# Beispiel:
```csharp
public class Memento
{
    public string State { get; }
    public Memento(string state) => State = state;
}
```

```csharp
public class Originator
{
    public string State { get; set; }
    public Memento Save() => new Memento(State);
    public void Restore(Memento memento) => State = memento.State;
}
```

```csharp
public class Caretaker
{
    public Memento Memento { get; set; }
}
```

## Praxisbeispiel

```csharp
// Beispiel: Texteditor mit Undo-Funktion
Editor editor = new Editor();
History history = new History();

editor.Text = "Version 1";
history.Push(editor.Save());

editor.Text = "Version 2";
editor.Restore(history.Pop());

Console.WriteLine(editor.Text); // Version 1
```
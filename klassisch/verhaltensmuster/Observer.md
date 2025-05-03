# Observer

Observer

Beschreibung:
Das Observer-Pattern definiert ein Kommunikationsmodell, bei dem mehrere abhängige Objekte (Beobachter) automatisch benachrichtigt werden, sobald sich der Zustand eines beobachteten Objekts (Subjekt) ändert. Es ermöglicht die Entkopplung zwischen Sender und Empfänger von Nachrichten oder Zustandsänderungen.

Lehrbuch-Beispiel in C#:
Dieses einfache Beispiel zeigt eine klassische Implementierung, wie sie in vielen Lehrbüchern vorkommt.

```csharp
public interface IObserver
{
    void Update();
}
```

```csharp
public interface ISubject
{
    void Attach(IObserver observer);
    void Detach(IObserver observer);
    void Notify();
}
```

```csharp
public class ConcreteSubject : ISubject
{
    private List_observers = new List();

    public void Attach(IObserver observer) => _observers.Add(observer);
    public void Detach(IObserver observer) => _observers.Remove(observer);
    public void Notify() => _observers.ForEach(o => o.Update());

    public string State { get; set; }
}
```

```csharp
public class ConcreteObserver : IObserver
{
    private string _name;
    public ConcreteObserver(string name) => _name = name;

    public void Update()
    {
        Console.WriteLine($"{_name} wurde benachrichtigt.");
    }
}
```

Praxisnahes Low-Level-Beispiel (mit Windows-spezifischen Interop-Funktionen):
Dieses Beispiel zeigt, wie mit einem Observer-Konzept auf tiefer Ebene (z. B. Multithreading) gearbeitet werden kann.

```csharp
using System;
using System.Collections.Generic;
using System.Runtime.InteropServices;
using System.Threading;

public interface IObserver
{
    void OnNotified();
}

public interface INotifiable
{
    void Register(IObserver observer);
    void NotifyAll();
}

public class MemoryObserver : IObserver
{
    private volatile int _flag;
    public void Wait()
    {
        while (_flag == 0)
        {
            NativeMethods.WaitOnAddress(ref _flag, 0, IntPtr.Zero, -1);
        }
    }

    public void OnNotified()
    {
        _flag = 1;
        NativeMethods.WakeByAddressAll(ref _flag);
    }
}
```

Innere Klasse um die Dll-Aufrufe auszuführen

```csharp
internal static class NativeMethods
{
    [DllImport("kernel32.dll", SetLastError = true)]
    internal static extern bool WaitOnAddress(ref int address, int compareValue, IntPtr addressSize, int milliseconds);

    [DllImport("kernel32.dll", SetLastError = false)]
    internal static extern void WakeByAddressAll(ref int address);
}

public class Subject : INotifiable
{
    private List_observers = new List();
    public void Register(IObserver observer) => _observers.Add(observer);

    public void NotifyAll()
    {
        foreach (var o in _observers)
        o.OnNotified();
    }
}
```

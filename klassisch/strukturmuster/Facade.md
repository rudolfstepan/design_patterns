# Facade Pattern

## Zweck
Bietet eine einheitliche Schnittstelle für eine Gruppe von Schnittstellen in einem Subsystem.

## Motivation
Vereinfacht die Benutzung komplexer Systeme durch eine Fassade.

## Beispiel in C#
```csharp
public class SubsystemA { public void DoA() => Console.WriteLine("A"); }
public class SubsystemB { public void DoB() => Console.WriteLine("B"); }

public class Facade
{
    private SubsystemA _a = new();
    private SubsystemB _b = new();
    public void DoAll()
    {
        _a.DoA();
        _b.DoB();
    }
}
```

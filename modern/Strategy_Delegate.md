# Strategy Pattern (Delegate-basiert)

## Zweck
Austauschbare Algorithmen über Funktionen oder Delegates.

## Beispiel
```csharp
Func<int, int> strategy = x => x * 2;
Console.WriteLine(strategy(10)); // 20
```

## Praxisbezug
Ersetzt klassische Klassenstrategien durch flexible Lambdas – z.B. bei Filtern, Berechnungen, Vergleichen.

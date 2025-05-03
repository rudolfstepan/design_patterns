# Event Sourcing

## Zweck
Speichert Systemzustände als Folge von Ereignissen.

## Beispiel
```csharp
public class AccountCreated { public Guid Id; public string Owner; }
public class MoneyDeposited { public Guid Id; public decimal Amount; }
```

## Praxisbezug
Wird in Finanzsystemen, Buchhaltung und verteilten Systemen eingesetzt, um vollständige Historie zu sichern.

# Middleware Pattern

## Zweck
Verarbeitung von HTTP-Anfragen in einer verketteten Pipeline.

## Beispiel
```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine("Vorher");
    await next();
    Console.WriteLine("Nachher");
});
```

## Praxisbezug
Fundamentaler Bestandteil jeder ASP.NET Core-Anwendung (z. B. Authentifizierung, Logging, CORS).

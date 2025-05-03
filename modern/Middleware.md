# Middleware Pattern (ASP.NET Core)

## Zweck
Erlaubt die Verarbeitung von HTTP-Anfragen in einer Kette von zustandslosen Komponenten.

## Vorteile
- Modularer Aufbau von Webanfragen
- Trennung von Belangen wie Logging, Authentifizierung, CORS, Caching
- Einfache Erweiterbarkeit durch benutzerdefinierte Middleware

## Nachteile
- Reihenfolge ist wichtig und kann zu Fehlern führen
- Versteckte Nebeneffekte, wenn nicht richtig dokumentiert

## Beispiel
```csharp
public class LoggingMiddleware
{
    private readonly RequestDelegate _next;

    public LoggingMiddleware(RequestDelegate next) => _next = next;

    public async Task Invoke(HttpContext context)
    {
        Console.WriteLine($"Request: {context.Request.Path}");
        await _next(context);
        Console.WriteLine($"Response: {context.Response.StatusCode}");
    }
}

// Registrierung in Program.cs
app.UseMiddleware<LoggingMiddleware>();
```

## Praxisbezug
Standardpattern in ASP.NET Core. Alle Framework-Middleware (Authentication, StaticFiles, etc.) basiert darauf.

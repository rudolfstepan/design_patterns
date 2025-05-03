# Middleware Pattern in Xamarin.Android

## Konzept
Auch wenn Xamarin.Android kein eingebautes Middleware-System wie ASP.NET Core besitzt, lässt sich das Middleware-Prinzip gut anwenden – z. B. bei HTTP-Kommunikation, Navigation oder Events.

---

## 1. HTTP Middleware mit `DelegatingHandler`

### Zweck
Fügt Verhalten vor oder nach einem HTTP-Aufruf hinzu – z. B. Logging, Authentifizierung oder Caching.

### Beispiel
```csharp
public class LoggingHandler : DelegatingHandler
{
    public LoggingHandler(HttpMessageHandler innerHandler) : base(innerHandler) { }

    protected override async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        Console.WriteLine("Request: " + request.RequestUri);
        var response = await base.SendAsync(request, cancellationToken);
        Console.WriteLine("Response: " + response.StatusCode);
        return response;
    }
}

// Verwendung
var client = new HttpClient(new LoggingHandler(new HttpClientHandler()));
var response = await client.GetAsync("https://example.com/api/data");
```

---

## 2. Navigation Middleware

### Zweck
Wickelt Navigation in eine Middleware-Kette ein – z. B. für Logging, Berechtigungen, Telemetrie.

### Beispiel
```csharp
public class NavigationMiddleware
{
    public async Task NavigateAsync(Func<Task> next)
    {
        Console.WriteLine("Before navigation");
        await next();
        Console.WriteLine("After navigation");
    }
}

// Verwendung
await new NavigationMiddleware().NavigateAsync(() =>
    Navigation.PushAsync(new DetailPage())
);
```

---

## 3. Middleware für eigene Request- oder Command-Pipeline

### Zweck
Führt Logik in verketteter Reihenfolge aus – ähnlich MediatR oder CQRS.

### Beispiel
```csharp
public interface IRequestMiddleware
{
    Task<T> HandleAsync<T>(Func<Task<T>> next);
}

public class RetryMiddleware : IRequestMiddleware
{
    public async Task<T> HandleAsync<T>(Func<Task<T>> next)
    {
        try
        {
            return await next();
        }
        catch
        {
            Console.WriteLine("Retrying...");
            return await next(); // Nur Beispiel: Nicht unendlich retrien!
        }
    }
}
```

---

## Fazit

Middleware-Konzepte lassen sich in Xamarin.Android vielseitig nutzen:
- **HTTP**: über DelegatingHandler
- **Navigation**: durch umgebende Wrapper
- **ViewModel-Pipeline**: durch Middleware-Handler

Damit erhöhst du Testbarkeit, Wiederverwendbarkeit und Trennung von Belangen.

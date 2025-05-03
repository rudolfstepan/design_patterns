# Options Pattern (ASP.NET Core)

## Zweck
Bindung von Konfiguration an stark typisierte POCOs.

## Beispiel
```csharp
public class MySettings { public string ApiKey { get; set; } }

// In Program.cs
builder.Services.Configure<MySettings>(builder.Configuration.GetSection("MySettings"));
```

## Praxisbezug
Standardkonzept in ASP.NET Core zur Verwaltung von AppSettings, API-Schlüsseln, Verbindungen etc.

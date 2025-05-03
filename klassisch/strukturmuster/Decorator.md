# Decorator Pattern

## Zweck
Fügt einem Objekt zur Laufzeit zusätzliche Funktionalität hinzu, ohne dessen Klasse zu verändern.

## Motivation
Das Pattern bietet eine flexible Alternative zur Unterklassenbildung, um Funktionalität zu erweitern.

## Struktur
- Komponente: Gemeinsame Schnittstelle
- Konkrete Komponente: Basisklasse
- Dekorator: Hält Referenz zur Komponente
- Konkreter Dekorator: Fügt Verhalten hinzu

## Beispiel in C#
```csharp
public interface IMessage
{
    string GetContent();
}

public class SimpleMessage : IMessage
{
    public string GetContent() => "Hello";
}

public class HtmlDecorator : IMessage
{
    private readonly IMessage _message;
    public HtmlDecorator(IMessage message) => _message = message;
    public string GetContent() => $"<html>{_message.GetContent()}</html>";
}
```

# Adapter

Adapter

Beschreibung:
Das Adapter-Pattern dient dazu, die Schnittstelle einer vorhandenen Klasse so anzupassen, dass sie mit einer anderen erwarteten Schnittstelle kompatibel wird. Es wird oft verwendet, wenn man bestehende Klassen wiederverwenden will, deren Schnittstellen nicht mit dem aktuellen System übereinstimmen.

Lehrbuch-Beispiel in C#:
Dieses Beispiel zeigt eine typische Implementierung, bei der eine inkompatible Methode angepasst wird.

```csharp
public interface ITarget
{
    void Request();
}
```

```csharp
public class Adaptee
{
    public void SpecificRequest() => Console.WriteLine("Spezifische Anfrage");
}
```

```csharp
public class Adapter : ITarget
{
    private Adaptee _adaptee = new Adaptee();
    public void Request() => _adaptee.SpecificRequest();
}
```

Praxisnahes Beispiel:
Stellen wir uns vor, wir haben eine alte XML-basierte Logger-Klasse, aber unser neues System arbeitet mit einer modernen JSON-Logger-Schnittstelle. Der Adapter verbindet beide Welten.

```csharp
public interface IJsonLogger
{
    void LogJson(string message);
}
```

```csharp
// Alte Klasse mit inkompatibler XML-basierten Schnittstelle
public class XmlLogger
{
    public void LogXml(string xmlMessage)
    {
        Console.WriteLine($"XML-Log: {xmlMessage}");
    }
}
```

```csharp
// Adapter, der IJsonLogger verwendet und intern XML verwendet
public class JsonToXmlLoggerAdapter : IJsonLogger
{
    private readonly XmlLogger _xmlLogger;
    public JsonToXmlLoggerAdapter(XmlLogger xmlLogger)
    {
	_xmlLogger = xmlLogger;
    }

    public void LogJson(string message)
    {
        // Simuliere JSON -> XML Konvertierung
        string xml = $"{message}";
        _xmlLogger.LogXml(xml);
    }
}
```

```csharp
// Anwendung:
public class App
{
    public static void Main()
    {
	IJsonLogger logger = new JsonToXmlLoggerAdapter(new XmlLogger());
	logger.LogJson("System gestartet");
    }
}
```

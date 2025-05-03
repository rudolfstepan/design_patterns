# Visitor

Visitor

Beschreibung:
Das Visitor-Pattern erlaubt es, neue Operationen auf Objekten durch eine zusätzliche Visitor-Klasse einzuführen, ohne die Klassen der besuchten Objekte selbst zu ändern.
Es trennt also die Datenstruktur von der auf ihr arbeitenden Logik. Dies ist besonders hilfreich, wenn sich häufig die Logik, aber selten die Struktur ändert.

Lehrbuch-Beispiel in C#:
Dieses Beispiel zeigt zwei konkrete Elemente und einen Besucher, der jeweils anders darauf reagiert.

```csharp
public interface IVisitor
{
    void Visit(ElementA element);
    void Visit(ElementB element);
}
```

```csharp
public interface IElement
{
    void Accept(IVisitor visitor);
}
```

```csharp
public class ElementA : IElement
{
    public void Accept(IVisitor visitor) => visitor.Visit(this);
}
```

```csharp
public class ElementB : IElement
{
    public void Accept(IVisitor visitor) => visitor.Visit(this);
}
```

```csharp
public class ConcreteVisitor : IVisitor
{
    public void Visit(ElementA element) => Console.WriteLine("Besuch in Element A");
    public void Visit(ElementB element) => Console.WriteLine("Besuch in Element B");
}
```

Praxisnahes Beispiel:
Ein Dokument besteht aus mehreren verschiedenen Elementen – z. B. Text, Bilder und Tabellen. Der Visitor kann zur Laufzeit unterschiedliche Operationen auf diesen anwenden, z. B. Drucken, Speichern oder Validieren.

```csharp
public interface IDocumentElement
{
    void Accept(IDocumentVisitor visitor);
}
```

```csharp
public interface IDocumentVisitor
{
    void VisitText(TextElement text);
    void VisitImage(ImageElement image);
    void VisitTable(TableElement table);
}
```

```csharp
public class TextElement : IDocumentElement
{
    public string Content { get; set; } = "Textinhalt";
    public void Accept(IDocumentVisitor visitor) => visitor.VisitText(this);
}
```

```csharp
public class ImageElement : IDocumentElement
{
    public string Path { get; set; } = "bild.jpg";
    public void Accept(IDocumentVisitor visitor) => visitor.VisitImage(this);
}
```

```csharp
public class TableElement : IDocumentElement
{
    public int Rows { get; set; } = 5;
    public void Accept(IDocumentVisitor visitor) => visitor.VisitTable(this);
}
```

```csharp
public class PrintVisitor : IDocumentVisitor
{
    public void VisitText(TextElement text) => Console.WriteLine($"Drucke Text: {text.Content}");
    public void VisitImage(ImageElement image) => Console.WriteLine($"Drucke Bild: {image.Path}");
    public void VisitTable(TableElement table) => Console.WriteLine($"Drucke Tabelle mit {table.Rows} Zeilen");
}
```

```csharp
// Anwendung:
public class App
{
    public static void Main()
    {
        var elements = new List
        {
            new TextElement(),
            new ImageElement(),
            new TableElement()
        };

        var printer = new PrintVisitor();
        elements.ForEach(e => e.Accept(printer));
    }
}
```
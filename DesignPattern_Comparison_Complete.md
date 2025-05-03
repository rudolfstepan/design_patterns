# 🧩 Vergleich von Design Patterns

Dieses Dokument bietet einen strukturierten Überblick über ähnliche Entwurfsmuster (Design Patterns) und hilft, die feinen Unterschiede zwischen ihnen zu erkennen. Anwendungsbeispiele und Entscheidungshilfen runden jeden Abschnitt ab.

## Inhaltsverzeichnis

1. [Erzeugungsmuster](#-erzeugungsmuster-im-vergleich)
2. [Beobachtungsmuster](#-beobachtungsmuster-im-vergleich)
3. [Verhaltensmuster](#-verhaltensmuster-im-vergleich)
4. [Strukturmuster](#-strukturmuster-im-vergleich)
5. [Instanzverwaltung & Zugriff](#-instanzverwaltung--zugriffsmuster-im-vergleich)

---

# Design Pattern Vergleich – Feine Unterschiede und Einsatzempfehlungen

## 🔧 Erzeugungsmuster im Vergleich

### Factory Method vs. Abstract Factory vs. Builder vs. Prototype

| Aspekt                     | Factory Method                          | Abstract Factory                                  | Builder                                           | Prototype                                      |
|---------------------------|-----------------------------------------|--------------------------------------------------|--------------------------------------------------|------------------------------------------------|
| Ziel                      | Objekterzeugung delegieren              | Familien verwandter Objekte erzeugen             | Komplexe Objekte schrittweise zusammensetzen     | Objekte durch Klonen erzeugen                 |
| Konfiguration             | Eine Klasse entscheidet, welches Objekt erzeugt wird | Sammlung von Factory-Methoden                    | Trennung von Aufbau-Logik und Objektstruktur     | Bestehendes Objekt wird dupliziert            |
| Verwendung                | Wenn Unterklassen entscheiden sollen, was instanziiert wird | Wenn verschiedene Varianten benötigt werden     | Wenn Objektaufbau komplex ist oder viele Schritte erfordert | Wenn Objekte ähnlich sind und kopiert werden sollen |
| Beispiel                  | GUI-Buttons für verschiedene OS         | UI-Factory für Windows und Mac                   | HTML-Builder, SQL-Query-Builder                  | Klonen von Konfigurationen oder Gegnern in Games |
| Vorteile                  | Einfache Erweiterung                    | Konsistenz von Produktfamilien                   | Flexibilität beim Objektaufbau                   | Schnelle Duplizierung                          |
| Nachteile                 | Viele Subklassen möglich                | Viele Klassen für jede Produktfamilie            | Mehr Code und Overhead                           | Tiefes Kopieren kann komplex sein              |

**Wann welches Muster?**
- Nutze **Factory Method**, wenn die Entscheidung über das zu erstellende Objekt in Unterklassen verlagert werden soll.
- Nutze **Abstract Factory**, wenn du mehrere Varianten von Objektfamilien brauchst, die konsistent erzeugt werden müssen.
- Nutze **Builder**, wenn das Objekt selbst komplex aufgebaut ist und unterschiedliche Darstellungen benötigt.
- Nutze **Prototype**, wenn du viele ähnliche Objekte brauchst oder Kopierprozesse optimieren willst.


## 👁️ Beobachtungsmuster im Vergleich

### Observer vs. Events vs. Publisher/Subscriber

| Aspekt                    | Observer                               | Events (z. B. .NET/C#)                           | Publisher/Subscriber                            |
|--------------------------|----------------------------------------|-------------------------------------------------|------------------------------------------------|
| Kopplung                 | Enge Kopplung an konkrete Subjekte     | Losere Kopplung via Sprache/Middleware           | Geringe Kopplung, oft über Bus oder Broker     |
| Registrierungsart        | Manuell beim Subjekt anmelden          | Sprachunterstützung durch `+=` oder Event-Handler | Zentrale Registratur oder Message-Broker       |
| Sichtbarkeit der Quelle  | Direkter Bezug zum Observable          | Meist bekannt, aber nicht zwingend               | Quelle kann komplett unbekannt sein            |
| Synchron vs. Asynchron   | Meist synchron                          | Meist synchron, aber async möglich               | Oft asynchron (z. B. RabbitMQ, Kafka)           |
| Rückkopplung             | Subjekt kennt seine Beobachter         | Eventquelle kennt ihre Listener                  | Publisher kennt Subscriber nicht direkt         |
| Beispiel                 | GUI-Komponenten reagieren auf Änderungen | Button-Click in C#                               | Microservices mit Event-Bus                     |

**Wann welches Muster?**
- Nutze **Observer**, wenn du eine enge Kopplung brauchst oder willst, z. B. in GUI-Systemen oder bei internen Modelländerungen.
- Nutze **Events**, wenn du innerhalb derselben Applikation lose gekoppelte Event-Reaktion willst – z. B. C# oder JavaScript.
- Nutze **Publisher/Subscriber**, wenn du mehrere Systeme lose über eine Middleware entkoppeln willst – etwa in verteilten Architekturen.



## 🧠 Verhaltensmuster im Vergleich

### Strategy vs. State vs. Command vs. Template Method

| Aspekt                    | Strategy                              | State                                        | Command                                     | Template Method                           |
|--------------------------|----------------------------------------|---------------------------------------------|---------------------------------------------|--------------------------------------------|
| Ziel                     | Austauschbare Algorithmen              | Zustandsabhängiges Verhalten                 | Kapselt eine Aktion als Objekt              | Struktur eines Algorithmus festlegen       |
| Fokus                    | Wie etwas getan wird                  | In welchem Zustand etwas getan wird         | Was getan werden soll                       | Reihenfolge der Schritte fest vorgeben     |
| Kontextverhalten         | Kontext kennt Strategie                | Kontext ändert seinen Zustand               | Kontext ruft Command aus                    | Subklassen überschreiben bestimmte Schritte |
| Entkopplung              | Strategie trennt Algorithmen von Kontext | Zustände isolieren Zustandslogik           | Aufrufer kennt nicht die Ausführung         | Subklassen überschreiben Teile der Methode |
| Erweiterbarkeit          | Hoch – neue Strategien möglich         | Hoch – neue Zustände                         | Hoch – neue Befehle                         | Eingeschränkt auf definierte Hook-Methoden |
| Beispiel                 | Sortier-Algorithmen                    | TCP-Verbindung (Connected, Closed)          | Undo/Redo, Menüaktionen                     | Game-Loop mit festen Hooks                 |

**Wann welches Muster?**
- Nutze **Strategy**, wenn du viele Varianten eines Algorithmus brauchst, die austauschbar sein sollen.
- Nutze **State**, wenn sich das Verhalten eines Objekts je nach Zustand ändern soll.
- Nutze **Command**, wenn du Aktionen als Objekte behandeln möchtest – z. B. für Undo, Queues oder Makros.
- Nutze **Template Method**, wenn du eine feste Struktur mit überladbaren Schritten brauchst (z. B. bei Parsing, Lebenszyklen etc.).



## 🧱 Strukturmuster im Vergleich

### Adapter vs. Bridge vs. Decorator vs. Composite

| Aspekt                    | Adapter                                | Bridge                                       | Decorator                                   | Composite                                   |
|--------------------------|----------------------------------------|----------------------------------------------|----------------------------------------------|----------------------------------------------|
| Ziel                     | Schnittstellen-Kompatibilität          | Entkopplung von Abstraktion und Implementierung | Dynamische Erweiterung von Verhalten        | Struktur für Teil-Ganzes-Hierarchien        |
| Fokus                    | Schnittstellenanpassung                | Trennung von Konzept und Umsetzung           | Verhalten erweitern ohne Unterklassen       | Gruppenbehandlung wie Einzelelemente        |
| Veränderung              | Bestehende Klassen nutzbar machen      | Änderung zur Laufzeit möglich                | Laufzeitkomposition statt Vererbung         | Einheitliche Behandlung von Objekten        |
| Beziehung                | "Wrapper" für inkompatible Klassen     | "Bridge" zwischen zwei Hierarchien           | Umhüllung bestehender Objekte                | Baumstruktur mit rekursivem Verhalten       |
| Beispiel                 | USB-zu-Seriell-Adapter                  | Zeichnen auf unterschiedlichen Geräten       | Logging um Komponenten herum                | GUI-Komponenten oder Dateisysteme           |

**Wann welches Muster?**
- Nutze **Adapter**, wenn du eine vorhandene Klasse mit inkompatibler Schnittstelle integrieren musst.
- Nutze **Bridge**, wenn du zwei Hierarchien unabhängig voneinander entwickeln möchtest – z. B. UI und Renderer.
- Nutze **Decorator**, wenn du Verhalten dynamisch erweitern möchtest, ohne Vererbung zu verwenden.
- Nutze **Composite**, wenn du Teil-Ganzes-Strukturen abbilden willst – z. B. Bäume oder rekursive Elemente.



## 🔂 Instanzverwaltung & Zugriffsmuster im Vergleich

### Singleton vs. Static Class vs. Dependency Injection

| Aspekt                    | Singleton                              | Static Class                                | Dependency Injection                         |
|--------------------------|----------------------------------------|---------------------------------------------|----------------------------------------------|
| Ziel                     | Nur eine Instanz im gesamten System    | Globale Funktionen ohne Instanz             | Übergabe von Abhängigkeiten statt Zugriff     |
| Instanzierung            | Lazily oder eager über private Konstruktor | Keine Instanz – rein statisch              | Instanz vom außen gesteuert                  |
| Erweiterbarkeit          | Eingeschränkt                          | Sehr eingeschränkt (nicht erweiterbar)       | Sehr hoch                                     |
| Testbarkeit              | Eingeschränkt – schwer zu mocken       | Sehr schlecht testbar                       | Sehr gut testbar (Mocks/Interfaces)          |
| Kopplung                 | Globaler Zustand – hohe Kopplung       | Sehr hohe Kopplung                          | Niedrige Kopplung                            |
| Beispiel                 | Logger, Configuration, Cache           | Math-Klasse, Helper-Methoden                | Services in modernen Frameworks              |

**Wann welches Muster?**
- Nutze **Singleton**, wenn genau eine Instanz notwendig ist und globaler Zugriff erforderlich, aber kontrollierbar sein soll.
- Nutze **Static Class**, wenn du rein funktionale Methoden hast, die keinen Zustand brauchen.
- Nutze **Dependency Injection**, wenn du maximale Flexibilität, Testbarkeit und lose Kopplung willst – besonders in großen Projekten.


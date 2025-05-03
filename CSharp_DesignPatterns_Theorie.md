# CSharp DesignPatterns Theorie

C# Design Patterns – Verständlich erklärt

Singleton
---------
Zweck:
Stellt sicher, dass es von einer Klasse nur genau eine Instanz gibt. Diese Instanz wird meist global über eine statische Eigenschaft zugänglich gemacht.

Typische Anwendung:
Beispielsweise für eine zentrale Protokollierung (Logger) oder eine globale Konfiguration.

Vorteile:
Einfacher Zugriff auf zentrale Instanzen, die systemweit verwendet werden.

Nachteile:
Kann bei unsachgemäßer Verwendung zu unkontrollierten globalen Abhängigkeiten führen. Testbarkeit leidet, wenn die Instanz schwer zu ersetzen ist.

Alternativen:
Injektionsbasierte Lösungen (z. B. Dependency Injection) für bessere Austauschbarkeit und Testbarkeit.

Factory Method
--------------
Zweck:
Stellt eine Methode bereit, die Objekte erzeugt, ohne die genaue Klasse des erzeugten Objekts zu kennen.

Typische Anwendung:
Wenn ein Framework Objekte erstellt, aber dem Anwender die Kontrolle über die genaue Ausprägung geben möchte.

Vorteile:
Flexibilität, da Unterklassen bestimmen können, welches konkrete Produkt erzeugt wird.

Nachteile:
Erfordert viele Klassen und kann unnötig kompliziert wirken, wenn nur wenige Varianten benötigt werden.

Alternativen:
Direktes Instanziieren (`new`) oder Abstract Factory für Produktfamilien.

Abstract Factory
----------------
Zweck:
Ermöglicht die Erzeugung zusammengehöriger Objekte (Produktfamilien), ohne deren konkrete Klassen zu kennen.

Typische Anwendung:
Benutzeroberflächen, bei denen Widgets für verschiedene Plattformen unterschiedlich aussehen sollen.

Vorteile:
Sorgt für Konsistenz zwischen zusammengehörigen Objekten (z. B. Mac-Button + Mac-Dialog).

Nachteile:
Viele Schnittstellen und Klassen, geringere Flexibilität bei gemischten Kombinationen.

Alternativen:
Factory Method für einzelne Objekte, Builder bei komplexen Konstruktionen.

Builder
-------
Zweck:
Erlaubt es, komplexe Objekte Schritt für Schritt zu konstruieren, wobei die Konstruktion vom Aufbau getrennt ist.

Typische Anwendung:
Dokumentgeneratoren, Konfigurationsobjekte, bei denen Teile optional sind.

Vorteile:
Bessere Lesbarkeit und Wartbarkeit durch schrittweise Konstruktion.

Nachteile:
Overhead bei einfachen Objekten, da zusätzliche Builder-Klassen notwendig sind.

Alternativen:
Initialisierer oder Fluent APIs, wenn keine vollständige Trennung nötig ist.

Prototype
---------
Zweck:
Erzeugt Objekte durch Kopieren (Clonen) eines vorhandenen Objekts anstatt durch Instanziierung.

Typische Anwendung:
Wenn `new` teuer ist oder die Objektkonfiguration kompliziert.

Vorteile:
Ermöglicht das einfache Kopieren komplex konfigurierter Objekte.

Nachteile:
Schwierig bei tief verschachtelten Objekten oder solchen mit Referenzabhängigkeiten.

Alternativen:
Factory Method, wenn genaue Kontrolle über Instanziierung gewünscht ist.

Observer
--------
Zweck:
Erlaubt es einem Objekt (Subjekt), mehrere Beobachter über Zustandsänderungen zu informieren.

Typische Anwendung:
In Benutzerschnittstellen (z. B. MVC), Eventsystemen oder Multithreading-Kommunikation.

Vorteile:
Entkopplung von Erzeuger und Reaktion; Beobachter können zur Laufzeit hinzugefügt werden.

Nachteile:
Komplexität durch viele Beobachter; schwierige Fehlernachverfolgung bei zyklischen Abhängigkeiten.

Alternativen:
Events, Reactive Extensions oder Messaging-Systeme als Alternativen mit anderer Abstraktion.

Strategy
--------
Zweck:
Kapselt eine Familie von Algorithmen und macht diese austauschbar.

Typische Anwendung:
Wenn verschiedene Varianten eines Verhaltens zur Auswahl stehen sollen (z. B. Sortierstrategien).

Vorteile:
Klare Trennung von Algorithmus und Verwendung, ermöglicht einfache Erweiterung.

Nachteile:
Kann bei vielen Strategien unübersichtlich werden.

Alternativen:
Template Method, wenn feste Abläufe mit austauschbaren Schritten gewünscht sind.

State
-----
Zweck:
Ermöglicht einem Objekt, sein Verhalten zu ändern, wenn sich sein interner Zustand ändert.

Typische Anwendung:
Zustandsautomaten wie bei Verbindungen (Offen, Verbunden, Fehlerhaft).

Vorteile:
Verkapselt Zustandslogik und macht sie modular.

Nachteile:
Viele Klassen bei vielen Zuständen; Zustandswechsel müssen klar definiert sein.

Alternativen:
Strategy, wenn Verhalten unabhängig vom Objektzustand ist.

Command
-------
Zweck:
Verpackt eine Anweisung in ein Objekt, um sie später auszuführen, zu speichern oder rückgängig zu machen.

Typische Anwendung:
Menübefehle, Makros, Undo-Operationen.

Vorteile:
Entkopplung von Sender und Empfänger, Befehle können gespeichert oder rückgängig gemacht werden.

Nachteile:
Kann bei vielen Befehlen viele kleine Klassen erzeugen.

Alternativen:
Delegate oder Events bei einfacher Interaktion ohne Undo-Anforderung.

Interpreter
-----------
Zweck:
Implementiert eine Sprache und einen Parser für einfache Ausdrücke oder Skripte.

Typische Anwendung:
Mathematische Parser, einfache Query-Sprachen, DSLs.

Vorteile:
Sehr geeignet für einfache Sprachen mit kleiner Grammatik.

Nachteile:
Unübersichtlich bei komplexeren Sprachen.

Alternativen:
Parsergeneratoren oder externe Bibliotheken für größere Sprachen.

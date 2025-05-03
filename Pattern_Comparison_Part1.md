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

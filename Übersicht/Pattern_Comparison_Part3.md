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


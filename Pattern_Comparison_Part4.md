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


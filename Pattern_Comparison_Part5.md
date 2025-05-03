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


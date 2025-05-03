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


# Moderne Design- und Architektur-Patterns (C#)

Dieser Ordner enthält moderne Patterns und Architekturprinzipien, die in der heutigen .NET/C#-Welt weit verbreitet sind. Jedes Pattern ist in einer eigenen Datei im Markdown-Format beschrieben – inklusive Beispielcode und Praxisbezug.

## Inhaltsverzeichnis

| Pattern                        | Beschreibung |
|-------------------------------|--------------|
| [DependencyInjection.md](../DependencyInjection.md) | Entkopplung durch externe Bereitstellung von Abhängigkeiten |
| [ServiceLocator.md](ServiceLocator.md)              | Globale Zugriffsmethode auf Abhängigkeiten (veraltet)        |
| [Repository.md](Repository.md)                      | Abstraktion der Datenzugriffsschicht                         |
| [UnitOfWork.md](UnitOfWork.md)                      | Koordination mehrerer Repositories in einer Transaktion      |
| [Specification.md](Specification.md)                | Kapselung von Geschäftslogik oder Filterkriterien            |
| [CQRS.md](CQRS.md)                                  | Trennung von Lese- und Schreibmodellen                       |
| [EventSourcing.md](EventSourcing.md)                | Zustandsrekonstruktion durch Ereignishistorie                |
| [MediatorModern.md](MediatorModern.md)              | Zentrale Vermittlung von Kommunikation (z. B. MediatR)       |
| [NullObject.md](NullObject.md)                      | Standardobjekt zur Vermeidung von `null`                     |
| [Strategy_Delegate.md](Strategy_Delegate.md)        | Delegates als moderne Strategie-Implementierung              |
| [OptionsPattern.md](OptionsPattern.md)              | Konfigurationsbindung über POCOs in ASP.NET Core             |
| [Middleware.md](Middleware.md)                      | Verarbeitung von HTTP-Requests in Pipelines                  |
| [HostedService.md](HostedService.md)                | Hintergrunddienste z. B. für Timer, Wartung, Worker-Threads  |

## Verwendung

Diese Patterns finden sich häufig in modernen C#-Anwendungen, insbesondere in ASP.NET Core, Microservices und Enterprise-Systemen. Sie ergänzen die klassischen GoF-Muster um flexible und praxisnahe Architekturlösungen.

# Spring Service (Layered Structure)
## Introduction

In der Softwareentwicklung ist eine klare und strukturierte Aufteilung der Verantwortlichkeiten von großer Bedeutung.
Das Spring Framework bietet eine bewährte Schichtenarchitektur, die uns dabei hilft, den Code sauber zu organisieren und zu pflegen.
In diesem Modul werden wir uns auf die Spring-Service-Struktur konzentrieren, die aus den Schichten Controller, Service und Repository besteht.
Außerdem werden wir uns mit Data Transfer Objects (DTOs) beschäftigen, die eine effiziente Kommunikation zwischen den Schichten und externen Modulen ermöglichen.
## Annotationen

`@Component` ist die allgemeine Annotation für alle Spring-Beans. Die folgenden Annotationen sind spezifischere Versionen von `@Component`, tun jedoch dasselbe.
* `@Service`
* `@Repository`
* ...

## DTOs (Data Transfer Objects)
DTOs sind einfache Java-Klassen, die verwendet werden, um Daten zwischen Schichten zu übertragen, ohne unnötige Details
preiszugeben. Sie helfen dabei, die Kommunikation effizient und klar zu gestalten. Ein typisches Beispiel wäre ein DTO,
das Benutzerinformationen zwischen Controller und Service überträgt.
```java
public class NeueBestellung {
private List<Produkt> produkte;

    // Getter und Setter
}

public class Bestellung {
private String id;
private List<Produkt> produkte;
private Bestellstatus status;
private Instant erstelltAm;
}
```
> Beachten Sie, dass DTOs auch für die Datenvalidierung verwendet werden können, bevor sie in der Datenbank 
> gespeichert werden.

## Controller

Der Controller ist die Schnittstelle zwischen der Benutzeroberfläche (oder externen Anfragen) und dem zugrunde liegenden System.
Er empfängt Anfragen, verarbeitet sie und gibt die entsprechenden Antworten zurück. Ein einfaches Beispiel könnte ein Controller sein, der Anfragen zur Benutzerregistrierung verarbeitet.

```java
@RestController
@RequestMapping("/api/bestellungen")
public class BestellController {

    private final BestellService bestellService;

    ...

    @PostMapping
    public Bestellung bestellungErstellen(@RequestBody NeueBestellung neueBestellung) {
        return bestellService.bestellungErstellen(neueBestellung);
    }
}
```
## Service

Der Service ist die Geschäftslogikschicht. Hier werden die tatsächlichen Aktionen und Operationen durchgeführt. Der Controller ruft Methoden im Service auf, um die Anfragen zu verarbeiten. Ein Beispiel für einen Service könnte die Validierung und Speicherung eines neuen Benutzers sein.

```java
@Service
public class BestellService {

    private private BestellRepository bestellRepository;

    ...

    public Benutzer bestellungErstellen(NeueBestellung neueBestellung) {
        // Validierung und Speicherung der Bestellung
        Bestellung bestellung = new Bestellung("123", neueBestellung.produkte, Bestellstatus.IN_BEARBEITUNG, Instant.now());
        return bestellRepository.save(bestellung);
    }
}
```
## Repository

Das Repository ist dafür verantwortlich, auf die Datenbank oder eine andere Datenquelle zuzugreifen. Hier werden die Datenbankabfragen und -operationen durchgeführt. In unserem Beispiel könnte das Repository die Aufgabe haben, Benutzerdaten in der Datenbank zu speichern und abzurufen.

```java
@Repository
public interface BestellRepository extends MongoRepository<Bestellung, String> {
// Datenbankabfragen und -operationen
}
```



# Java Spring Data
Siehe als Beispiel: [Challenge_2024_02_15](https://github.com/MaHambach/Challenge_2024_02_15.git)

## Einbinden einer MongoDB Datenbank mit Java Spring Boot

Um eine MongoDB Datenbank in ein Java Spring Boot Projekt einzubinden, müssen folgende Schritte durchgeführt werden:

### 1. Dependency hinzufügen
Füge die folgende Dependency in die `pom.xml` Datei hinzu:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

### 2. Konfiguration hinzufügen
Füge die folgende Konfiguration in die `application.properties` Datei hinzu:
```properties
spring.data.mongodb.uri=${MONGODB_CONNECTION_STRING}
```

### 3. Umgebungsvariable hinzufügen
Benutzt du MongoDB Atlas, findest du den Connection-String in deinem Cluster unter "Connect" -> "Compass".

Der Connection-String sollte in etwa so aussehen:
```properties
mongodb+srv://<username>:<password>@<cluster-url>/<database-name>
```

Füge ihn dann in deine Umgebungsvariablen in IntelliJ ein.

* Gehe zu "Run" -> "Edit Configurations..."
* Wähle deine Spring Boot Konfiguration aus
* Füge unter "Environment" eine neue Umgebungsvariable hinzu
  * Name: `MONGODB_CONNECTION_STRING`
  * Value: `<dein-connection-string>`

__! Wichtig:__ Ersetze `<username>`, `<password>`, `<cluster-url>` und `<database-name>` durch deine eigenen Daten.

__! Wichtig:__ Die Datenbank muss bereits existieren. Spring Boot erstellt keine Datenbanken.

### 4. Repository erstellen
Du musst ein Repository erstellt haben, auf das du zugreifen kannst, wie schon in Schritt 3 gesehen. Mache dir auch 
klar, wie die Datenbankstruktur aussieht, damit du die Datenbankabfragen korrekt erstellen kannst.

### 5. Datenbankabfragen erstellen
Erstelle hierfür zunächst Java-Klassen, welche die verschiedenen Elemente deiner Datenbank repräsentieren. Am besten 
als `Records`.

Erstelle dann ein Interface, welches von `MongoRepository` erbt und die Datenbankabfragen definiert.

```java
import org.springframework.data.mongodb.repository.MongoRepository;

public interface RecordRepository extends MongoRepository<Record, String> {
    List<Record> findByTitle(String title);
}
```

### 6. Datenbankabfragen verwenden
Nun kannst du die Datenbankabfragen in deinem Code verwenden. Hier ein Beispiel, wie du die Datenbankabfrage aus 
Schritt 5 verwenden kannst:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
public class RecordController {
    @Autowired
    private RecordRepository recordRepository;

    @GetMapping("/records")
    public List<Record> getRecordsByTitle(@RequestParam String title) {
        return recordRepository.findByTitle(title);
    }
}
```

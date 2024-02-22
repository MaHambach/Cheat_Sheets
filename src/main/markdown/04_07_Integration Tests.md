# Integrationstests mit Spring Boot Cheat-Sheet
## Schnelle Übersicht
| Befehl                                             | Auswirkung                                                                                       |
|----------------------------------------------------|--------------------------------------------------------------------------------------------------|
| `@SpringBootTest`                                  | Erstellt einen Spring-Kontext für den Integrationstest.                                         |
| `@AutoConfigureMockMvc`                            | Konfiguriert den MockMvc für den Integrationstest.                                               |
| `@Autowired MockMvc mockMvc`                       | Injiziert den MockMvc-Instanz für die Verwendung in Integrationstests.                           |
| `MockMvcRequestBuilders.get("/api/resource")`      | Simuliert eine HTTP-GET-Anfrage an den angegebenen Endpunkt.                                     |
| `MockMvcResultMatchers.status().isOk()`            | Überprüft, ob der HTTP-Statuscode der Antwort 200 (OK) ist.                                      |
| `@Sql({"/data.sql"})`                              | Führt SQL-Skripte vor dem Test aus, um Testdaten vorzubereiten.                                   |
| `@ActiveProfiles("test")`                          | Aktiviert bestimmte Profile für Integrationstests.                                               |
| `@Transactional`                                   | Rollback von Transaktionen nach jedem Test, um die Datenbank in einen konsistenten Zustand zu bringen. |
| `@TestConfiguration`                               | Definiert eine benutzerdefinierte Konfiguration nur für Integrationstests.                        |


## 1. Abhängigkeiten hinzufügen:
Maven Abhängigkeiten für Integrationstests hinzufügen:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

Für einen Fake-Server:
```xml
<dependency>
    <groupId>de.flapdoodle.embed</groupId>
    <artifactId>de.flapdoodle.embed.mongo.spring3x</artifactId>
    <version>4.12.0</version>
    <scope>test</scope>
</dependency>
```
Im Testordner muss dann ein Verbindungsstring für den Fake-Server in die `application.properties` eingefügt werden:
```
de.flapdoodle.mongodb.embedded.version=7.0.4
```
## 2. Integrationstests erstellen:

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.servlet.MockMvc;

@SpringBootTest
@AutoConfigureMockMvc
@DirtiesContext(classMode = DirtiesContext.ClassMode.BEFORE_EACH_TEST_METHOD) //Notwendig, damit mögliche erzeugte Datensätze in der
                                                                              //simulierten Datenbank restlos nach jedem Test gelöscht
                                                                              //werden
public class MyIntegrationTests {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void testSomething() throws Exception {
        // Integrationstest-Code hier
    }
}
```
## 3. Test mit MockMvc durchführen:

Mit MockMvc können Sie HTTP-Anfragen simulieren und die Antwort überprüfen.

```java
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.result.MockMvcResultMatchers;

@Test
public void testSomething() throws Exception {
mockMvc.perform(MockMvcRequestBuilders.get("/api/resource"))
.andExpect(MockMvcResultMatchers.status().isOk());
}
```
## 4. Testdaten vorbereiten:

Verwenden Sie @Sql oder @SqlGroup zum Vorbereiten von Testdaten mit SQL-Skripts.
```java
import org.springframework.test.context.jdbc.Sql;

@Test
@Sql({"/data.sql"})
public void testWithSqlScript() {
// Test-Code hier
}
```
## 5. Profile in Integrationstests verwenden:

Aktivieren Sie bestimmte Profile für Integrationstests.
```java
@SpringBootTest
@ActiveProfiles("test")
public class MyIntegrationTests {
// Integrationstest-Code hier
}
```
## 6. Transaktionsverhalten steuern:

Verwenden Sie @Transactional zum Rollback von Transaktionen nach jedem Test.
```java
import org.springframework.transaction.annotation.Transactional;

@SpringBootTest
@Transactional
public class MyIntegrationTests {
// Integrationstest-Code hier
}
```
## 7. Benutzerdefinierte Konfiguration für Integrationstests:

Verwenden Sie @TestConfiguration für benutzerdefinierte Konfigurationen nur für Integrationstests.
```java
import org.springframework.boot.test.context.TestConfiguration;

@TestConfiguration
public class TestConfig {
// Benutzerdefinierte Konfiguration hier
}
```
Dies sind grundlegende Schritte und Best Practices für Integrationstests mit Spring Boot. Je nach Anwendungsfall können weitere Anpassungen und Optimierungen erforderlich sein.
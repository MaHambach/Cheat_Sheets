# Java Spring
## Annotationen
| Annotation        | Beschreibung                                                                          |
|-------------------|---------------------------------------------------------------------------------------|
| `@Controller`     | Markiert eine Klasse als Controller in einer MVC-Anwendung.                           |
| `@RestController` | Kombination von `@Controller` und `@ResponseBody`. Verwendet für RESTful-Webservices. |
| `@RequestMapping` | Mappt HTTP-Anforderungen auf Handler-Methoden in einem Controller.                    |
| `@GetMapping`     | Spezifische Anfragemethodenannotation für `@RequestMapping` - HTTP GET-Anfragen.      |
| `@PostMapping`    | Spezifische Anfragemethodenannotation für `@RequestMapping` - HTTP POST-Anfragen.     |
| `@PutMapping`     | Spezifische Anfragemethodenannotation für `@RequestMapping` - HTTP PUT-Anfragen.      |
| `@DeleteMapping`  | Spezifische Anfragemethodenannotation für `@RequestMapping` - HTTP DELETE-Anfragen.   |
| `@RequestParam`   | Bindet den Wert eines HTTP-Anforderungsparameters an einen Methodenparameter.         |
| `@PathVariable`   | Extrahiert Variable aus der URI und bindet sie an Methodenparameter.                  |
| `@RequestBody`    | Bindet den Wert des HTTP-Anforderungsbodies an einen Methodenparameter.               |

### Konfiguration
| Annotation       | Beschreibung                                                              |
|------------------|---------------------------------------------------------------------------|
| `@Configuration` | Markiert eine Klasse als Konfigurationsklasse für die Spring-Anwendung.   |
| `@Bean`          | Definiert eine Methode als Bean, die von Spring verwaltet wird.           |

### Datenbankzugriff
| Annotation      | Beschreibung                                                 |
|-----------------|--------------------------------------------------------------|
| `@Repository`   | Markiert eine Klasse als Repository für Datenbankzugriff.    |
| `@Autowired`    | Automatische Verdrahtung von Beans durch den Spring-Kontext. |

### Tests
| Annotation                        | Beschreibung                                          |
|-----------------------------------|-------------------------------------------------------|
| `@RunWith(SpringRunner.class)`    | Konfiguriert den JUnit-Test, um mit Spring zu laufen. |
| `@SpringBootTest`                 | Erstellt den Spring-Kontext für den Test.             |
| `@MockBean`                       | Erstellt eine Mock-Instanz eines Beans für den Test.  |

### Security
| Annotation                  | Beschreibung                                                  |
|-----------------------------|---------------------------------------------------------------|
| `@EnableWebSecurity`        | Aktiviert die Websecurity-Konfiguration.                      |
| `@PreAuthorize`             | Definiert Vorauthentifizierungsausdrücke für Methodenaufrufe. |

### RESTful Web Services
| Annotation                  | Beschreibung                                                               |
|-----------------------------|----------------------------------------------------------------------------|
| `@RestController`           | Markiert eine Klasse als REST-Controller.                                  |
| `@GetMapping`               | Definiert einen Endpunkt für HTTP-GET-Anfragen.                            |
| `@PostMapping`              | Definiert einen Endpunkt für HTTP-POST-Anfragen.                           |
| `@PutMapping`               | Definiert einen Endpunkt für HTTP-PUT-Anfragen.                            |
| `@DeleteMapping`            | Definiert einen Endpunkt für HTTP-DELETE-Anfragen.                         |
| `@PathVariable`             | Extrahiert Variable aus der URI und bindet sie an Methodenparameter.       |

### Dependency Injection
| Annotation   | Beschreibung                               |
|--------------|--------------------------------------------|
| `@Autowired` | Führt eine automatische Verdrahtung durch. |

### Logging
| Annotation      | Beschreibung                                          |
|-----------------|-------------------------------------------------------|
| `@Slf4j`        | Lombok-Annotation zum Hinzufügen eines SLF4J-Loggers. |

### Transaktionen
| Annotation       | Beschreibung                                     |
|------------------|--------------------------------------------------|
| `@Transactional` | Markiert eine Methode für Transaktionen.         |

### Scheduler
| Annotation       | Beschreibung                                        |
|------------------|-----------------------------------------------------|
| `@Scheduled`     | Definiert eine geplante Methode für die Ausführung. |

### Testing
| Annotation   | Beschreibung                                           |
|--------------|--------------------------------------------------------|
| `@Test`      | Markiert eine Methode als Testmethode für JUnit-Tests. |

## Arbeiten mit dem API-Pfad in Spring

In Spring können Sie den Pfad (Path) einer API mithilfe verschiedener Annotationen definieren:

### @RequestMapping

Die Annotation `@RequestMapping` wird verwendet, um den Basispfad für einen Controller festzulegen. Sie kann auf Klassen- und Methodenebene angewendet werden.

#### Beispiel:
```java
@RestController
@RequestMapping("/api")
public class MyController {
    // API-Endpunkt unter /api/hello
    @GetMapping("/hello")
    public String hello() {
        return "Hello from API!";
    }
}
```
Die obige Klasse definiert einen REST-Controller, der unter dem Basispfad `/api` verfügbar ist. Die Methode `hello` ist unter `/api/hello` verfügbar.
### Pfadvariablen (Path Variables)

Sie können auch dynamische Teile des Pfades definieren, die als Pfadvariablen bezeichnet werden. Diese werden in der URL definiert und können in Ihren Controller-Methoden verwendet werden.

#### Beispiel:
```java
@GetMapping("/users/{id}")
public User getUserById(@PathVariable Long id) {
// Hier wird die ID aus dem Pfad extrahiert
// und zur Datenbankabfrage verwendet
}
```
### Anfrageparameter (Query Parameters)

Anfrageparameter sind Teil der URL, die dem "?"-Zeichen folgen. Sie können verwendet werden, um zusätzliche Informationen an Ihre API-Endpunkte zu übergeben.

#### Beispiel:

```java
@GetMapping("/search")
public List<Product> searchProducts(@RequestParam String keyword) {
// Hier wird der Anfrageparameter "keyword" verwendet,
// um Produkte zu suchen
}
```
Diese Mechanismen ermöglichen es Ihnen, die Struktur Ihrer API-Pfade in Spring zu definieren und dynamisch auf Benutzeranfragen zu reagieren.

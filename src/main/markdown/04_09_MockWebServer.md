# MockWebServer - Testen von HTTP Interaktionen in Spring
## Maven dependency
Um MockWebServer in unserem Spring-Projekt zu verwenden, müssen wir es zunächst als Abhängigkeit in unserem Maven-
Projekt einbinden. Fügen Sie dazu die folgende Abhängigkeit in Ihre pom.xml-Datei ein:
```xml
<dependency>
    <groupId>com.squareup.okhttp3</groupId>
    <artifactId>mockwebserver</artifactId>
    <version>4.9.1</version>
    <scope>test</scope>
</dependency>
```
## Beispiel Code - Initialisierung des MockWebServers:
```java
import okhttp3.mockwebserver.MockWebServer;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class MyApiTest {

    private static MockWebServer mockWebServer;

    @BeforeAll
    static void beforeAll() throws IOException {
        mockWebServer = new MockWebServer();
        mockWebServer.start();
    }

    @AfterAll
    static void tearDown() throws IOException {
        mockWebServer.shutdown();
    }

    @DynamicPropertySource
    static void backendProperties(DynamicPropertyRegistry registry) {
        registry.add("rickandmorty.url", () -> mockWebServer.url("/").toString());
    }


    // Weitere Testmethoden...
}
```

## Beispiel Code - Testen von HTTP-Anfragen und -Antworten:
```java
@Test
public void testApiCall() throws IOException {
    
    mockWebServer.enqueue(new MockResponse()
            .setBody("""
                        [{
                            "name": "Mayo",
                            "id": "1"
                        }]
                    """)
            .addHeader("Content-Type", "application/json"));

    mockMvc.perform(MockMvcRequestBuilders.get("/api/items/"))
            .andExpect(status().isOk())
            .andExpect(content().json("""
                    [{
                        "name": "Mayo",
                        "id": "1"
                    }]
                    """));
}
```

## Was ist MockWebServer?: 
MockWebServer ist eine Testbibliothek von OkHttp, mit der Sie einen simulierten Webserver in Ihren Tests starten können.

## Warum ist es wichtig?:
MockWebServer ermöglicht es Ihnen, HTTP-Anfragen und -Antworten in Ihren Tests zu simulieren, ohne dass Sie tatsächlich eine echte externe API aufrufen müssen. Dadurch können Sie Ihre Tests isolieren und unabhängig von externen Ressourcen machen, was sie zuverlässiger und schneller macht.


## Was sind @BeforeEach und @AfterEach?: 
Diese Annotationen werden in JUnit-Tests verwendet, um Methoden zu kennzeichnen, die vor bzw. nach jedem Testlauf ausgeführt werden sollen.

## Warum sind sie wichtig?: 
Mit `@BeforeEach` können Sie Setup-Arbeiten durchführen, z.B. das Initialisieren von Variablen, die für alle Tests benötigt werden. @AfterEach wird verwendet, um Cleanup-Arbeiten durchzuführen, wie das Schließen von Ressourcen oder das Zurücksetzen von Änderungen.

## Was sind Setup- und Teardown-Methoden?: 
Setup-Methoden werden verwendet, um die Umgebung vor den Tests einzurichten, während Teardown-Methoden verwendet werden, um die Umgebung nach den Tests aufzuräumen.

## Warum sind sie wichtig?: 
Diese Methoden ermöglichen es Ihnen, Tests in einer definierten Umgebung auszuführen und sicherzustellen, dass keine unerwünschten Seiteneffekte auftreten.

## Wie integriere ich MockWebServer mit Maven?:
Fügen Sie die entsprechende Abhängigkeit zu Ihrem pom.xml hinzu, um MockWebServer in Ihr Projekt einzubinden.

## Warum ist die Konfiguration wichtig?: 
Je nach den Anforderungen Ihrer Tests müssen Sie möglicherweise verschiedene Einstellungen für Ihren MockWebServer vornehmen, z.B. die Portnummer, die zu simulierenden Antworten usw.

## Wie schreibe ich einen Test mit MockWebServer?:
Erstellen Sie eine Instanz von MockWebServer, konfigurieren Sie sie entsprechend Ihren Anforderungen, starten Sie sie, führen Sie Ihre Tests durch und überprüfen Sie die erwarteten HTTP-Anfragen und -Antworten.

## Warum sind sie wichtig?: 
MockResponse ermöglicht es Ihnen, präzise vordefinierte Antworten für Ihre Testfälle zu erstellen, während `MockWebServer.enqueue()` Ihnen die Möglichkeit gibt, mehrere Antworten in einer bestimmten Reihenfolge zu planen, um verschiedene Szenarien zu testen.
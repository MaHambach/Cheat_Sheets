# RestClient
## Warum RestClient?
In den vorherigen Sitzungen haben wir gelernt, wie man eine REST-API mit Spring Boot erstellt. In dieser Sitzung lernen 
wir, wie man den RestClient verwendet, um auf ___externe___ APIs zuzugreifen und Daten abzurufen.

## Verwendung des RestClient
Der RestClient ist Teil des Spring-Webpakets und kann verwendet werden, um auf externe APIs zuzugreifen. Der RestClient 
basiert auf dem reaktiven Programmiermodell und ist daher asynchron. Das bedeutet, dass wir die Daten nicht direkt 
erhalten, sondern nur ein Versprechen, dass die Daten zu einem späteren Zeitpunkt geliefert werden.

## Codebeispiele
### Grundlegender Aufruf
Der folgende Code zeigt den grundlegenden Aufruf des RestClient zum Abrufen von Daten aus einer API:

```java
@Service
public class MyService {

    private final RestClient restClient;

    public MyService(RestClient.Builder restClientBuilder) {
        this.restClient = restClientBuilder.baseUrl("https://example.org").build();
    }

    public Details someRestCall(String name) {
        return this.restClient.get().uri("/{name}/details", name).retrieve().body(Details.class);
    }
}
```

### Erstellung von Modellklassen
Um die Daten aus der API darzustellen, müssen wir Modellklassen erstellen, die die Felder enthalten, die wir aus der API-Antwort extrahieren möchten.
Die Felder in den Modellklassen müssen genau denselben Namen und denselben Datentyp haben wie sie in der API-Antwort erscheinen.

> Hinweis: Es werden nur die Daten aus den Feldern extrahiert, die in unserer Modellklasse vorhanden sind. Wenn das API-Objekt mehr Felder als das von uns definierte Modell hat, werden die "ungenutzten" Felder ignoriert.

### Beispiel einer API-Antwort
```java
public record ApiResponse(
        List<Character> results
) {
}
```

Die API-Antwort enthält eine Liste von Character-Objekten.
```java
public record Character(
        int id,
        String name
) {
}
```

Jedes Character-Objekt enthält eine id und einen name.
```java
public ApiResponse fetchApiResponse(){
    RestClient restClient = RestClient.builder().baseUrl("https://rickandmortyapi.com/api").build();
    ApiResponse response = restClient.get().uri("/character").retrieve().body(ApiResponse.class);
    assert response != null;
    return response;
}

public List<Character> getAllCharacters() {
    return fetchApiResponse().results();
}
```
In diesem Beispiel holen wir die API-Antwort und extrahieren die Liste der Character-Objekte daraus.

> Das Verständnis der Verwendung von RestClient und der Modellklassen ist eine wichtige Grundlage für die Arbeit mit Full-Stack-Anwendungen und die erfolgreiche Nutzung externer APIs.

### Beispiel Daten abrufen
Hier ist ein weiteres Beispiel für die Verwendung des RestClient, um Daten von einer externen API abzurufen:

```java
@Service
public class WeatherService {

    private final RestClient restClient;

    public WeatherService(RestClient.Builder restClientBuilder) {
        this.restClient = restClientBuilder.baseUrl("https://api.weather.com").build();
    }

    public WeatherData getWeatherData(String city) {
        return this.restClient.get()
                .uri("/weather-data/{city}", city)
                .retrieve()
                .bodyToMono(WeatherData.class)
                .block(); // Block until the response is received
    }
}
```

In diesem Beispiel erstellen wir einen WeatherService, der den RestClient verwendet, um Wetterdaten für eine bestimmte Stadt von einer externen API abzurufen. Die Methode getWeatherData nimmt den Namen der Stadt als Parameter entgegen und ruft dann die entsprechenden Wetterdaten von der API ab.

Die WeatherData-Klasse repräsentiert die Struktur der Wetterdaten, die wir von der API erhalten. Sie sollte entsprechend der Struktur der API-Antwort definiert sein.

## API, die eine Liste zurückgibt
Wenn die API anstelle eines Objekts eine Liste zurückgibt, können Sie den Array-Typ verwenden, um das JSON in Java-Objekte zu konvertieren.

```json
[
  {    
    "id": "1",    
    "name": "Rick"
  },  
  {    
    "id": "2",    
    "name": "Morty"
  },   
  ...
]
```

```java
public List<Character> fetchApiResponse(){
    RestClient restClient = RestClient.builder().baseUrl("https://rickandmortyapi.com/api").build();
    Character[] response = restClient.get()
        .uri("/character")
        .retrieve()
        .body(Character[].class);
  
    return Arrays.asList(response);
}
```

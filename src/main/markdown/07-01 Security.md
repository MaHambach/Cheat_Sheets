# Security
## OAuth2 über GitHub
### Dependency für OAuth2 hinzufügen
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-oauth2-client</artifactId>
 </dependency>
```

### Konfiguration hinzufügen
```properties
spring.security.oauth2.client.registration.github.client-id=${GITHUB_ID}
spring.security.oauth2.client.registration.github.client-secret=${GITHUB_SECRET}
spring.security.oauth2.client.registration.github.scope=none
app.url=${APP_URL}
```

* `client-id` und `client-secret` erhältst du von GitHub, wenn du eine neue OAuth-App erstellst.
* `scope` gibt an, welche Berechtigungen die App haben soll. `none` bedeutet, dass keine Berechtigungen benötigt werden.
* `app.url` ist die URL deiner App.
* Die Werte für `client-id` und `client-secret` müssen in den Umgebungsvariablen hinterlegt werden.
* Alternativ zu GitHub können auch andere Anbieter verwendet werden, wie z.B. Google, Facebook oder Okta.

### OAuth2-App auf GitHub erstellen
1. Gehe zu [GitHub Developer Settings](
2. Klicke auf "New OAuth App"
3. Fülle die Felder aus:
   * Application name: Name deiner App
   * Homepage URL: URL deiner App
   * Authorization callback URL: URL deiner App + "/login/oauth2/code/github"
     * Eventuell zwei Apps erstellen: eine für lokale Entwicklung eine für die Produktionsumgebung
   * Application description: Beschreibung deiner App
   * Application logo: Logo deiner App
4. Klicke auf "Register application"
5. Kopiere `Client ID` und `Client Secret` in deine Umgebungsvariablen
6. Klicke auf "Save"

__! Wichtig:__ Die URL deiner App muss mit der URL übereinstimmen, die du in der OAuth-App eingetragen hast.

__! Wichtig:__ Hier kriegen wir auch den `GITHUB_ID` und den `GITHUB_SECRET` her.

## Backend Aufbau
### Controller
### SecurityConfig
Zwei wichtige Annotationen:
* `@Configuration` gibt an, dass es sich um eine Konfigurationsklasse handelt
* `@EnableWebSecurity` aktiviert die Web-Security
* `@Bean` gibt an, dass es sich um eine Bean handelt, die von Spring verwaltet wird


#### Beispiel
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf(AbstractHttpConfigurer::disable)
            .sessionManagement(sessionManagement -> sessionManagement.sessionCreationPolicy(SessionCreationPolicy.
                    ALWAYS)) //Hiermit wird die Session immer erstellt, auch wenn sie nicht benötigt wird.
            .exceptionHandling(e -> e.authenticationEntryPoint(new HttpStatusEntryPoint(HttpStatus.UNAUTHORIZED)))
                .oauth2Login(o -> o.defaultSuccessorUrl(appUrl + "/login/success"))
                .authorizeHttpRequest(a -> a
                        .requestMatchers(HttpMethod.GET, "/api/**").authenticated()
                        .requestMatchers(HttpMethod.POST, "/api/**").permitAll()
                        .anyRequest().permitAll() //Sollte im fertigen Produkt nicht so sein.
                );
        
        return http.build();
    }
}
```
#### Erklärung 
* Die Reihenfolge bei `http` ist wichtig, da die Methoden in der Reihenfolge aufgerufen werden, in der sie definiert sind.
  * Besonders wichtig bei `authorizeHttpRequest`, da die Reihenfolge der Methoden die Reihenfolge der Anfragen bestimmt.
* `csrf(AbstractHttpConfigurer::disable)` deaktiviert den CSRF-Schutz. Das ist in der Regel nicht empfehlenswert, aber für die lokale Entwicklung ist es einfacher.
  * Hiermit hohlen wir uns absichtlich eine Sicherheitslücke ins Backend denn... ansonsten mehr Aufwand.
* `permitAll()` beim `requestMatchers` erlaubt den Zugriff auf die angegebene URL für alle.
* `authenticated()` beim `requestMatchers` erfordert eine Authentifizierung für die angegebene URL.

### OAuth2-Login
### UserController

```java
@GetMapping("/me")
public String getCurrentUser(@AuthenticationPrincipal OAuth2User principal) {
    return principal.getName();
}
```
* Bei GitHub ist der `name` die Benutzer-ID des Benutzers.
  * Diese ist eindeutig und kann für die Identifikation des Benutzers verwendet werden.


## Sonstiges
Öffnen eines neuen Fensters in JavaScript:
```javascript
window.open('http://localhost:8080/login/oauth2/code/github', '_self');
```
* `window.open` öffnet ein neues Fenster
* `'_self'` gibt an, dass das Fenster im aktuellen Tab geöffnet wird
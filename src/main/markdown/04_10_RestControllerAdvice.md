# RestControllerAdvice
## Einführung
Der RestControllerAdvice ist ein leistungsfähiges Werkzeug im Spring-Framework, das uns dabei hilft, die 
Fehlerbehandlung und Kommunikation in unserer RESTful-Anwendung zu verbessern. Es ermöglicht uns, elegant und zentral 
auf Fehler zu reagieren und Feedback an die Client-Anwendung zu geben. Ein RestControllerAdvice kann global auf alle 
Controller oder speziell auf einen bestimmten Controller angewendet werden.

## ErrorMessage-Entität (Record)
Um die Kommunikation von Fehlermeldungen zu vereinfachen, erstellen wir eine einfache ErrorMessage-Entität (Record) mit 
einem Nachrichtenfeld.

```java
public record ErrorMessage(String message) {
}
```

Diese Entität enthält nur ein Feld `message`, das den Text der Fehlermeldung enthält. Dadurch können wir Fehlermeldungen 
in strukturierter Form zurückgeben.

> Um die ErrorMessage-Entität noch leistungsfähiger zu machen, könnten wir zusätzliche Felder wie Fehlercode, 
> Zeitstempel usw. hinzufügen. Festlegen von HTTP-Statuscodes für Fehlerantworten

Um die Fehlerkommunikation zu verbessern, ist es wichtig, die richtigen HTTP-Statuscodes für die Antworten festzulegen. 
Dies hilft dem Client, den Typ des Fehlers zu verstehen und entsprechend zu reagieren. Hierfür bietet Spring die 
`@ResponseStatus`-Annotation, die wir auf unsere ExceptionHandler-Methoden anwenden können.

```java
@ResponseStatus(HttpStatus.BAD_REQUEST)
```

> Die `@ResponseStatus`-Annotation kann auch auf die Methoden unserer Controller angewendet werden, um den Statuscode 
> der Antwort festzulegen.

## Globale Fehlerbehandlung mit @RestControllerAdvice
Die Annotation `@RestControllerAdvice` ermöglicht es uns, eine Klasse zu erstellen, die sich global auf alle Controller 
in unserer Anwendung auswirkt. Dies ist besonders nützlich, um gemeinsame Fehlerbehandlungslogik an einem zentralen Ort 
zu definieren.

```java
@RestControllerAdvice
@ResponseStatus(HttpStatus.BAD_REQUEST)
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ErrorMessage handleGlobalException(Exception ex) {
        ErrorMessage errorMessage = new ErrorMessage("Ein Fehler ist aufgetreten: " + ex.getMessage());
        return errorMessage;
    }
}
```

In diesem Beispiel verwenden wir die `@ExceptionHandler`-Annotation, um die Methode handleGlobalException zu definieren. 
Diese Methode wird aufgerufen, wenn eine Ausnahme nicht innerhalb eines Controllers behandelt wird. Sie erstellt eine 
Instanz unserer ErrorMessage-Entität (Record) und sendet eine HTTP-Antwort mit dem entsprechenden Statuscode.

## Integration in Spring-Projekte
Um RestControllerAdvice in Ihr bestehendes Spring-Projekt zu integrieren, befolgen Sie diese Schritte:

1. Erstellen Sie eine neue Klasse (z. B. GlobalExceptionHandler) mit der `@RestControllerAdvice`-Annotation.
2. Definieren Sie Methoden, die mit `@ExceptionHandler` annotiert sind, um verschiedene Arten von Fehlern zu behandeln.
3. Verwenden Sie die erstellte ErrorMessage-Klasse, um strukturierte Fehlermeldungen zurückzugeben.


# Lombok
## Befehle
### 1. @Getter und @Setter:
Annotationen, um automatisch Getter- und Setter-Methoden für Felder zu generieren.
#### Beispiel 1:
Für individuelle Felder.
```java
import lombok.Getter;
import lombok.Setter;

public class MyClass {
    @Getter @Setter private int id;
    @Getter @Setter private String name;
}
```
#### Beispiel 2:
Für alle Felder der Klasse.
```java
import lombok.Getter;
import lombok.Setter;

@Getter
@Override
public class MyClass {
    private int id;
    private String name;
}
```
### 2. @ToString:
Generiert eine toString()-Methode, die den Klassennamen und die Werte der Felder enthält.
#### Beispiel:
```java
import lombok.ToString;

@ToString
public class MyClass {
    private int id;
    private String name;
}
```
### 3. @EqualsAndHashCode:
Generiert equals()- und hashCode()-Methoden auf Basis der Felder der Klasse.
#### Beispiel:
```java
import lombok.EqualsAndHashCode;

@EqualsAndHashCode
public class MyClass {
private int id;
private String name;
}
```
### 4. @NoArgsConstructor, @RequiredArgsConstructor und @AllArgsConstructor:
Generiert Konstruktoren ohne Argumente (@NoArgsConstructor), Konstruktoren für erforderliche Felder (@RequiredArgsConstructor) und Konstruktoren für alle Felder (@AllArgsConstructor).
#### Beispiel:
```java
import lombok.AllArgsConstructor;
import lombok.NoArgsConstructor;
import lombok.RequiredArgsConstructor;

@NoArgsConstructor
@RequiredArgsConstructor
@AllArgsConstructor
public class MyClass {
    private int id;
    private final String name;
}
```
### 5. @Data:
Kombiniert @Getter, @Setter, @EqualsAndHashCode, @ToString und @RequiredArgsConstructor.
#### Beispiel:
```java
import lombok.Data;

@Data
public class MyClass {
    private int id;
    private String name;
}
```
### 6. @Builder:
Generiert einen Builder für die Klasse, der das Erstellen von Instanzen mit einer Fluent-Schnittstelle ermöglicht.
#### Beispiel:
```java
import lombok.Builder;

@Builder
public class MyClass {
    private int id;
    private String name;
}
```
### 7. @Value:
Erzeugt eine unveränderliche Klasse, die final für alle Felder und private für die Sichtbarkeit verwendet.
#### Beispiel:
```java
import lombok.Value;

@Value
public class MyClass {
    private int id;
    private String name;
}
```
### 8. @SneakyThrows:
Verwendet Lombok, um eine Methode zu erstellen, die eine Ausnahme wirft, ohne dass die Methode sie deklariert.
#### Beispiel:
```java
import lombok.SneakyThrows;

public class MyClass {
    @SneakyThrows
    public void myMethod() {
        throw new Exception();
    }
}
```
Das obige Beispiel zeigt, wie @SneakyThrows verwendet wird, um eine Methode zu definieren, die eine Exception wirft, ohne dass die Methode die Exception deklariert. Der Compiler erzwingt normalerweise, dass Methoden, die überprüfbare Ausnahmen werfen könnten, die entsprechenden Ausnahmen deklarieren oder behandeln. Durch die Verwendung von @SneakyThrows umgehst du diese Überprüfung und kannst Ausnahmen werfen, ohne dass die Methode sie deklariert.
## Anmerkungen
### @Value und @Builder: 
Die @Value-Annotation erzeugt eine unveränderliche Klasse, während die @Builder-Annotation einen Builder für die Klasse generiert. In einigen Fällen können diese beiden Annotationen konkurrierende Anforderungen darstellen, da der Builder möglicherweise mutierbare Instanzen erfordert, während @Value unveränderliche Instanzen erzeugt. Stelle sicher, dass die Verwendung beider Annotationen sinnvoll ist und nicht zu inkonsistentem Verhalten führt.

### Konstruktorverhalten: 
Lombok bietet verschiedene Möglichkeiten zur Generierung von Konstruktoren mit @NoArgsConstructor, @RequiredArgsConstructor und @AllArgsConstructor. Wenn du mehrere dieser Annotationen auf derselben Klasse verwendest, achte darauf, wie sich ihre generierten Konstruktoren gegenseitig beeinflussen und ob sie zu Inkonsistenzen führen können.

### @Data und @Value:
Wenn du beide Annotationen auf derselben Klasse verwendest oder versehentlich beide verwendet werden, können die generierten Methoden und das Verhalten der Klasse inkonsistent sein.

Einige Probleme, auf die du achten solltest:

* Setter-Methodenkonflikte: Wenn du sowohl @Data als auch @Value verwendest, können Konflikte entstehen, da @Data Setter-Methoden generiert, die die Unveränderlichkeit beeinträchtigen würden, die durch @Value erzeugt wird.
* Konflikte bei der Equals- und HashCode-Generierung: @Data und @Value generieren unterschiedliche equals()- und hashCode()-Methoden. Die @Data-Annotation generiert standardmäßig equals() und hashCode() basierend auf allen Feldern, während @Value die Objektidentität berücksichtigt. Die Verwendung beider Annotationen kann zu inkonsistenten Verhalten führen.

Um Konflikte zu vermeiden, solltest du nur eine der Annotationen verwenden, je nachdem, welche Funktionalität du benötigst. Wenn du unveränderliche Klassen mit finalen Feldern benötigst, verwende @Value. Wenn du Standardgetter und Setter benötigst, verwende @Data. Wenn du eine Kombination von beiden benötigst, solltest du die gewünschten Methoden explizit definieren oder eine der Annotationen nicht verwenden.
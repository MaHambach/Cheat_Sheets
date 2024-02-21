
# Lombok
## Befehle
| Annotation                 | 	Effekt                                                                                                                                                   |
        |---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `@Data`                    | Generiert Getter, Setter, toString, equals und hashCode Methoden für alle Felder der Klasse.                                                              |
| `@Getter`                  | Generiert Getter-Methoden für alle Felder der Klasse.                                                                                                     |
| `@Setter`                  | Generiert Setter-Methoden für alle Felder der Klasse.                                                                                                     |
| `@ToString`                | Generiert eine toString-Methode, die den Namen der Klasse und alle Felder mit ihren Werten enthält.                                                       |
| `@EqualsAndHashCode`       | Generiert equals und hashCode Methoden, basierend auf den Feldern der Klasse.                                                                             |
| `@AllArgsConstructor`      | Generiert einen Konstruktor mit allen Feldern der Klasse als Argumente.                                                                                   |
| `@NoArgsConstructor`       | Generiert einen Standardkonstruktor ohne Argumente.                                                                                                       |
| `@RequiredArgsConstructor` | Generiert einen Konstruktor mit allen finalen Feldern als Argumente.                                                                                      |
| `@Builder`                 | Generiert einen Builder, der es ermöglicht, Objekte der Klasse mit einer Fluent-Builder-Syntax zu erstellen.                                              |
| `@Value`                   | Generiert eine unveränderliche Klasse mit finalen Feldern, Getter-Methoden für diese Felder, einer `toString()`-Methode und equals und hashCode Methoden. |
| `@Slf4j`                   | Stellt Logger-Unterstützung bereit, indem ein statisches final-Feld log mit dem Logger für die Klasse                                                     |
generiert wird.
## Anmerkungen
### @Value und @Builder:
Die @Value-Annotation erzeugt eine unveränderliche Klasse, während die @Builder-Annotation einen Builder für die
Klasse generiert. In einigen Fällen können diese beiden Annotationen konkurrierende Anforderungen darstellen, da
der Builder möglicherweise mutierbare Instanzen erfordert, während @Value unveränderliche Instanzen erzeugt.
Stelle sicher, dass die Verwendung beider Annotationen sinnvoll ist und nicht zu inkonsistentem Verhalten führt.

        ### Konstruktorverhalten:
Lombok bietet verschiedene Möglichkeiten zur Generierung von Konstruktoren mit `@NoArgsConstructor`,
`@RequiredArgsConstructor` und `@AllArgsConstructor`. Wenn du mehrere dieser Annotationen auf derselben Klasse
verwendest, achte darauf, wie sich ihre generierten Konstruktoren gegenseitig beeinflussen und ob sie zu
Inkonsistenzen führen können.

### @Data und @Value:
Wenn du beide Annotationen auf derselben Klasse verwendest oder versehentlich beide verwendet werden, können die
generierten Methoden und das Verhalten der Klasse inkonsistent sein.

        Einige Probleme, auf die du achten solltest:

        * Setter-Methodenkonflikte: Wenn du sowohl `@Data` als auch @Value verwendest, können Konflikte entstehen, da `@Data`
        * Setter-Methoden generiert, die die Unveränderlichkeit beeinträchtigen würden, die durch `@Value` erzeugt wird.
Konflikte bei der Equals- und HashCode-Generierung: @Data und @Value generieren unterschiedliche `equals()`- und
`hashCode()`-Methoden. Die @Data-Annotation generiert standardmäßig `equals()` und `hashCode()` basierend auf
allen Feldern, während @Value die Objektidentität berücksichtigt. Die Verwendung beider Annotationen kann zu
inkonsistenten Verhalten führen.

Um Konflikte zu vermeiden, solltest du nur eine der Annotationen verwenden, je nachdem, welche Funktionalität du
benötigst. Wenn du unveränderliche Klassen mit finalen Feldern benötigst, verwende `@Value`. Wenn du Standard-Getter
und Setter benötigst, verwende `@Data`. Wenn du eine Kombination von beiden benötigst, solltest du die gewünschten
Methoden explizit definieren oder eine der Annotationen nicht verwenden.


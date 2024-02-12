# Date

In Java können wir das `Date`-Objekt verwenden, um das aktuelle Datum und die aktuelle Uhrzeit zu erhalten. Das `Date`-Objekt ist in der `java.util`-Paket enthalten.

Allerdings sollte man lieber `LocalDate`, `LocalTime`, `LocalDateTime`, `ZoneDateTime` und `Ìnstant` aus dem `java.
time`-Paket verwenden, da das `Date`-Objekt veraltet ist und einige Probleme hat.

* `LocalDate`: Ein Datum ohne Zeitangabe (z. B. 2022-01-31)
* `LocalTime`: Eine Uhrzeit ohne Datum (z. B. 15:30:45)
* `LocalDateTime`: Ein Datum und eine Uhrzeit (z. B. 2022-01-31T15:30:45)
* `ZoneDateTime`: Ein Datum und eine Uhrzeit mit Zeitzoneninformationen (z. B. 2022-01-31T15:30:45+01:00)
* `Instant`: Ein Zeitstempel, der die Anzahl der Sekunden seit dem 1. Januar 1970 UTC darstellt


## 1. Aktuelles Datum und Uhrzeit erhalten
```java
import java.time.*;

public class Main {
    public static void main(String[] args) {
        LocalDate localDate = LocalDate().now();
        LocalTime localTime = LocalTime.now();
        LocalDateTime localDateTime = LocalDateTime.now();
        ZoneDateTime zoneDateTime = ZoneDateTime.now();
        Instant instant = Instant.now();
        
        System.out.println("LocalDate:     " + localDate);
        System.out.println("LocalTime:     " + localTime);
        System.out.println("LocalDateTime: " + localDateTime);
        System.out.println("ZoneDateTime:  " + zoneDateTime);
        System.out.println("Instant:       " + instant);
    }
}
```
## 2. Datum und Uhrzeit formatieren
Verwende das entsprechende Formatierungsmuster, um das Datum und die Uhrzeit nach deinen Anforderungen zu formatieren.

### Formatierungsmuster:
* yyyy: Jahr (z. B. 2022)
* MM: Monat (01-12)
* dd: Tag im Monat (01-31)
* HH: Stunde im 24-Stunden-Format (00-23)
* mm: Minute (00-59)
* ss: Sekunde (00-59)
* E: Tag der Woche (z. B. Mo, Di, Mi)
* EEE: Kurzer Tag der Woche (z. B. Mon, Tue, Wed)
* EEEE: Vollständiger Name des Wochentags (z. B. Montag, Dienstag)
* MMMM: Monat als Name (z. B. January, February)
* MMMMM: Kurzer Monatsname (z. B. Jan, Feb)

#### Beispiele:
* String pattern = "yyyy-MM-dd HH:mm:ss";
  * Ausgabe: 2022-01-31 15:30:45
* String pattern = "yyyy-MM-dd HH:mm:ss EEE"; 
  * Ausgabe: 2022-01-31 15:30:45 Mon 
* String pattern = "yyyy-MM-dd HH:mm:ss EEEE"; 
  * Ausgabe: 2022-01-31 15:30:45 Montag 


### Beispiel: LocalDateTime zu String formatieren
```java
import java.time.format.DateTimeFormatter;
import java.time.*;

public class Main {
    public static void main(String[] args) {
        LocalDateTime localDateTime = LocalDateTime.now();
        
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("EEEE dd-MM-yyyy");
        String formattedDateTime = localDateTime.format(formatter);
        
        System.out.println("Formatted DateTime: " + formattedDateTime);
        // Ausgabe: Formatted DateTime: Montag 12-02-2024
    }
}
```
### Beispiel: String zu LocalDateTime parsen
```java
import java.time.format.DateTimeFormatter;
import java.time.*;

public class Main {
    public static void main(String[] args) {
        String dateTimeString = "31-01-2023 15:30:45";
        
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        LocalDateTime parsedDateTime = LocalDateTime.parse(dateTimeString, formatter);
        
        System.out.println("Parsed DateTime: " + parsedDateTime);
        // Ausgabe: Parsed DateTime: 2023-01-31T15:30:45
    }
}
```

## 3. Datum und Uhrzeit manipulieren
Hier sind einige nützliche Methoden, um `LocalDateTime`-Objekte in Java zu manipulieren:

| Methode                           | Beschreibung                                                                        |
|-----------------------------------|-------------------------------------------------------------------------------------|
| `plusYears(int years)`            | Fügt eine bestimmte Anzahl von Jahren hinzu.                                        |
| `plusMonths(int months)`          | Fügt eine bestimmte Anzahl von Monaten hinzu.                                       |
| `plusDays(int days)`              | Fügt eine bestimmte Anzahl von Tagen hinzu.                                         |
| `plusHours(int hours)`            | Fügt eine bestimmte Anzahl von Stunden hinzu.                                       |
| `plusMinutes(int minutes)`        | Fügt eine bestimmte Anzahl von Minuten hinzu.                                       |
| `plusSeconds(int seconds)`        | Fügt eine bestimmte Anzahl von Sekunden hinzu.                                      |
| `minusYears(int years)`           | Subtrahiert eine bestimmte Anzahl von Jahren.                                       |
| `minusMonths(int months)`         | Subtrahiert eine bestimmte Anzahl von Monaten.                                      |
| `minusDays(int days)`             | Subtrahiert eine bestimmte Anzahl von Tagen.                                        |
| `minusHours(int hours)`           | Subtrahiert eine bestimmte Anzahl von Stunden.                                      |
| `minusMinutes(int minutes)`       | Subtrahiert eine bestimmte Anzahl von Minuten.                                      |
| `minusSeconds(int seconds)`       | Subtrahiert eine bestimmte Anzahl von Sekunden.                                     |
| `withYear(int year)`              | Ändert das Jahr.                                                                    |
| `withMonth(int month)`            | Ändert den Monat.                                                                   |
| `withDayOfMonth(int dayOfMonth)`  | Ändert den Tag des Monats.                                                          |
| `withHour(int hour)`              | Ändert die Stunde.                                                                  |
| `withMinute(int minute)`          | Ändert die Minute.                                                                  |
| `withSecond(int second)`          | Ändert die Sekunde.                                                                 |
| `with(TemporalAdjuster adjuster)` | Verwendet einen TemporalAdjuster, um das Datum/Zeit-Objekt zu ändern.               |
| `truncatedTo(ChronoUnit unit)`    | Rundet das Datum/Zeit-Objekt auf die angegebene Einheit (z.B. Stunden, Minuten) ab. |

## 4. Datum und Uhrzeit vergleichen
In Java kann man `LocalDate`-Objekte miteinander vergleichen, indem man die Methoden compareTo oder 
die Methoden `isBefore()`, `isAfter()` und `isEqual()` verwendet.


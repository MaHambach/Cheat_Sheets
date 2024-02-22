# Unit-Tests mit JUnit und Mockito
## Schnellübersicht
| Befehl                                                   | Beschreibung                                                                                                     |
|----------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `Mockito.mock(Class<T> classToMock)`                     | Erzeugt ein Mock-Objekt für die angegebene Klasse.                                                               |
| `Mockito.when(mockedObject.method()).thenReturn(value)`  | Definiert das Verhalten des Mock-Objekts, wenn die angegebene Methode aufgerufen wird.                           |
| `Mockito.verify(mockedObject).method()`                  | Überprüft, ob eine bestimmte Methode auf dem Mock-Objekt aufgerufen wurde.                                       |
| `Mockito.verify(mockedObject, times(n)).method()`        | Überprüft, ob eine Methode auf dem Mock-Objekt genau n-mal aufgerufen wurde.                                     |
| `Mockito.verifyNoInteractions(mockedObject)`             | Überprüft, ob keine Interaktionen mit dem Mock-Objekt stattgefunden haben.                                       |
| `Mockito.verifyNoMoreInteractions(mockedObject)`         | Überprüft, ob nach der letzten Überprüfung keine weiteren Interaktionen mit dem Mock-Objekt stattgefunden haben. |
| `Mockito.doThrow(exception).when(mockedObject).method()` | Definiert, dass das Mock-Objekt eine Ausnahme auslöst, wenn die angegebene Methode aufgerufen wird.              |
| `Mockito.doNothing().when(mockedObject).method()`        | Definiert, dass das Mock-Objekt nichts tun soll, wenn die angegebene Methode aufgerufen wird.                    |
| `Mockito.spy(objectToSpyOn)`                             | Erzeugt ein Spy-Objekt, das ein echtes Objekt überwacht und bestimmte Methoden überschreibt.                     |
| `Mockito.doReturn(value).when(spyObject).method()`       | Definiert das Verhalten des Spy-Objekts, wenn die angegebene Methode aufgerufen wird.                            |


## 1. Maven Abhängigkeiten hinzufügen:
```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>5.10.0</version> <!-- Aktuelle Version hier einfügen -->
    <scope>test</scope>
</dependency>
```
## Beispiele
Hier sind zwei Beispiele für Unit-Tests mit Mockito:

### Beispiel: Überprüfung, ob eine Methode aufgerufen wurde:
```java
import static org.mockito.Mockito.*;

public class ExampleTest {

    @Test
    public void testExampleMethod() {
        // Mock erstellen
        SomeClass mockObject = mock(SomeClass.class);

        // Methode aufrufen, die den Mock verwenden sollte
        ClassUnderTest classUnderTest = new ClassUnderTest(mockObject);
        classUnderTest.doSomething();

        // Überprüfen, ob eine bestimmte Methode aufgerufen wurde
        verify(mockObject).someMethod();
    }
}
```
### Beispiel: Mocken eines Methodenaufrufs mit Rückgabewert:
```java
import static org.mockito.Mockito.*;

public class CalculatorTest {

    @Test
    public void testAddition() {
        // Mock erstellen
        Calculator calculator = mock(Calculator.class);

        // Verhalten des Mocks definieren: Wenn die Methode add(2, 3) aufgerufen wird, 
        // soll 5 zurückgegeben werden
        when(calculator.add(2, 3)).thenReturn(5);

        // Methode aufrufen, die den Mock verwenden sollte
        int result = calculator.add(2, 3);

        // Ergebnis überprüfen
        assertEquals(5, result);
    }
}
```

### Beispiel: Überprüfung, dass nach einer bestimmten Methode keine weiteren Interaktionen mit dem Mock-Objekt erfolgt sind:
```java
import static org.mockito.Mockito.*;

public class ExampleTest {

    @Test
    public void testNoMoreInteractions() {
        // Mock erstellen
        SomeClass mockObject = mock(SomeClass.class);

        // Methode aufrufen, die den Mock verwenden sollte
        ClassUnderTest classUnderTest = new ClassUnderTest(mockObject);
        classUnderTest.doSomething();

        // Überprüfen, ob die Methode aufgerufen wurde
        verify(mockObject).someMethod();

        // Weitere Interaktionen mit dem Mock-Objekt simulieren
        mockObject.someOtherMethod();

        // Überprüfen, dass nach 'someMethod' keine weiteren Interaktionen stattgefunden haben
        verifyNoMoreInteractions(mockObject);
    }
}
```
### Beispiel: Überprüfung, dass keine Interaktionen mit dem Mock-Objekt stattgefunden haben:
```java
import static org.mockito.Mockito.*;

public class ExampleTest {

    @Test
    public void testNoInteractions() {
        // Mock erstellen
        SomeClass mockObject = mock(SomeClass.class);

        // Keine Methodenaufrufe auf dem Mock-Objekt

        // Überprüfen, dass keine Interaktionen mit dem Mock-Objekt stattgefunden haben
        verifyNoInteractions(mockObject);
    }
}
```

## Spy-Objekte
Die spy-Methode in Mockito wird verwendet, um einen echten Objektinstanz zu erstellen, die das Verhalten eines echten Objekts nachahmt, aber gleichzeitig alle Aufrufe und Interaktionen mit diesem Objekt verfolgt werden können. Im Wesentlichen wird ein Spion erstellt, der alle Methodenaufrufe und Interaktionen des echten Objekts verfolgt, während das echte Objekt unverändert bleibt.

Hier ist ein Beispiel, das zeigt, wie die spy-Methode verwendet wird:

```java
import static org.mockito.Mockito.*;

public class ExampleTest {

    @Test
    public void testSpy() {
        // Echtes Objekt erstellen
        SomeClass realObject = new SomeClass();

        // Spion erstellen
        SomeClass spyObject = spy(realObject);

        // Methodenaufruf auf dem echten Objekt
        realObject.doSomething();

        // Methodenaufruf auf dem Spion
        spyObject.doSomething();

        // Überprüfen, ob die Methode aufgerufen wurde
        verify(realObject).doSomething();
        verify(spyObject).doSomething();
    }
}
```
In diesem Beispiel wird ein echtes Objekt realObject erstellt und dann ein Spion spyObject erstellt, der das Verhalten von realObject nachahmt. Beide Objekte werden verwendet, um die Methode doSomething() aufzurufen. Anschließend wird überprüft, ob die Methode sowohl auf dem echten Objekt als auch auf dem Spion aufgerufen wurde.

Die spy-Methode ist nützlich, wenn Sie das Verhalten eines echten Objekts beibehalten müssen, aber dennoch überprüfen möchten, welche Methoden aufgerufen wurden und welche Interaktionen mit dem Objekt stattgefunden haben.
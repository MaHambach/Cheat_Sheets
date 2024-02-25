# Allgemeines zu Tests

* Wird auf eine Umgebungsvariable verwiesen, muss diese für den Test selber noch gesetzt werden. (Nicht unbedingt mit dem "richtigen" Wert.)
  * Aufgepasst: Umgebungsvariablen können auch für einzelne Tests erstellt werden, nicht für die ganze Test-Datei.
* Für weitere Variablen der Form `${some.vlaue}` kann auch eine application.properties im Testordner erstellt werden.
* `@SpringBootTest` lädt den gesamten Anwendungskontext, was zu langsamen Tests führen kann. 
  * Alternativ kann `@WebMvcTest` verwendet werden, um nur den Webkontext zu laden.

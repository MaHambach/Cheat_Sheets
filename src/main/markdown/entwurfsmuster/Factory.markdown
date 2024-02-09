Das Factory Method Entwurfsmuster ist ein Erzeugungsmuster (Creational Pattern), das die Erstellung von Objekten kapselt und den Subklassen die Verantwortung überlässt, die konkrete Implementierung der Objekte zu wählen. Es ermöglicht die Definition einer Schnittstelle zur Erstellung von Objekten, wobei die konkrete Klasse zur Erstellung dieser Objekte zur Laufzeit entschieden wird.

Hier ist eine Übersicht über die Hauptkomponenten dieses Musters:

Product (Produkt): Dies ist das abstrakte Basisklasse oder das Schnittstellen-Interface für das zu erstellende Objekt.
ConcreteProduct (Konkrete Produkte): Dies sind die tatsächlichen Implementierungen des Produkts, die von der Factory erstellt werden.
Creator (Schöpfer): Dies ist die abstrakte Klasse oder das Interface, das die Factory Method definiert. Diese Methode wird verwendet, um ein neues Produkt zu erstellen. Es kann auch eine Standardimplementierung dieser Methode bereitstellen, die ein Standardprodukt erstellt.
ConcreteCreator (Konkreter Schöpfer): Dies sind die konkreten Implementierungen des Schöpfers, die die Factory Method implementieren, um die konkreten Produkte zu erstellen.
Ein einfaches Beispiel für das Factory Method Entwurfsmuster könnte eine Anwendung sein, die verschiedene Arten von Dokumenten (z.B. PDF, Word, Text) erstellt:

java
Copy code
// Product
interface Document {
void open();
void save();
}

// Concrete Products
class PdfDocument implements Document {
public void open() {
System.out.println("Opening PDF document.");
}
public void save() {
System.out.println("Saving PDF document.");
}
}

class WordDocument implements Document {
public void open() {
System.out.println("Opening Word document.");
}
public void save() {
System.out.println("Saving Word document.");
}
}

// Creator
abstract class DocumentCreator {
public abstract Document createDocument();
}

// Concrete Creators
class PdfDocumentCreator extends DocumentCreator {
public Document createDocument() {
return new PdfDocument();
}
}

class WordDocumentCreator extends DocumentCreator {
public Document createDocument() {
return new WordDocument();
}
}

// Client
public class Client {
public static void main(String[] args) {
DocumentCreator creator = new PdfDocumentCreator();
Document document = creator.createDocument();
document.open();
document.save();
}
}
In diesem Beispiel ist Document das abstrakte Produkt, PdfDocument und WordDocument sind konkrete Produkte. DocumentCreator ist der Schöpfer und PdfDocumentCreator und WordDocumentCreator sind konkrete Schöpfer. Der Client entscheidet, welchen Typ von Dokument er erstellen möchte, indem er den entsprechenden konkreten Schöpfer verwendet. Die Factory Method (createDocument()) wird aufgerufen, um das gewünschte Produkt zu erstellen.
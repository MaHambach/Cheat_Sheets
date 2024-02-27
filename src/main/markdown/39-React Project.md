# React Project
## 1.  Projekt erstellen
Wähle in IntelliJ:
```
File -> New -> Project...
```

Wähle ein `vite`-Projekt aus, wähle bei `Template` React, setze den Haken bei `Use TypeScript template` und klicke 
auf `create`.

__! Wichtig:__ Im Namen eines `vite`-Projekts dürfen keine Großbuchstaben vorkommen. Kommen Großbuchstaben vor, wird IntelliJ schlicht das Projekt nicht erstellen, aber keine Fehlermeldung geben.

__! Wichtig:__ Bei jedem neuen `vite`-Projekt sollte es ein Pop-up geben, welches dich auffordert `Run 'npm 
install'` auszuführen. Dies ist zwingen notwendig, da sonst das Projekt nicht funktioniert.

---
## 2.  Projektstruktur
Das von `vite` erstellte Projekt hat folgende Struktur:

Projektordner \
│\
├─ [public](#21-public)\
│   └─ [vite.svg](#22-vitesvg)\
├─ [src](#23-src)\
│  ├─ [assets](#24-assets)\
│  │   \
│  ├─ [App.css](#25-appcss)\
│  ├─ [App.tsx](#26-apptsx)\
│  ├─ [index.css](#27-indexcss)\
│  └─ [main.tsx](#28-maintsx)\
├─ [.gitignore](#29-gitignore)\
├─ [index.html](#210-indexhtml)\
└─ [package.json](#211-packagejson)\
---
### 2.1. public
Auszug aus der [Dokumentation](https://vitejs.dev/guide/assets.html#the-public-directory):

Wenn Sie Assets haben, die:
* Niemals im Quellcode referenziert werden (z. B. `robots.txt`)
* Den genauen Dateinamen beibehalten müssen (ohne Hashing)
* ... oder Sie einfach nicht möchten, dass Sie zuerst ein Asset importieren müssen, um seine URL zu erhalten

Dann können Sie das Asset in einem speziellen `public` Verzeichnis unter Ihrem Projektstamm platzieren. Assets in 
diesem Verzeichnis werden während der Entwicklung im Wurzelpfad `/` bereitgestellt und unverändert in das Stammverzeichnis 
des dist-Verzeichnisses kopiert.

Das Verzeichnis ist standardmäßig `<root>/public`, kann jedoch über die Option `publicDir` konfiguriert werden.

Beachten Sie, dass:
* Sie immer `public` Assets mit absolutem Pfad ab der Wurzel referenzieren sollten - zum Beispiel sollte 
`public/icon.png` im Quellcode als `/icon.png` referenziert werden.
* Assets in public können nicht aus JavaScript importiert werden.

#### 2.1.1. Beispiel
Im neu erstellen `vite`-Projekt wird die Datei `vite.svg` im `public`-Ordner abgelegt. In der `App.tsx` wird die 
Grafik dann wie folgt eingebunden: 
```tsx
import viteLogo from '/vite.svg';
```
```html
<img src={viteLogo} className="logo" alt="Vite logo" />
```

---
### 2.2. vite.svg
Das ist das Logo von `vite`. Es wird standardmäßig in der `index.html` eingebunden.

**Hinweis:** Das Logo kann gelöscht werden.

**Hinweis:** `.svg` ist ein Vektorgrafikformat. Es kann mit einem Texteditor geöffnet und bearbeitet werden.

---
### 2.3. src
In diesem Ordner befinden sich, wie auch bei `java`, die Dateien, die für das Projekt relevant sind.

---
### 2.4. assets
In diesem Ordner können statische Assets abgelegt werden, die im Projekt verwendet werden. Der Hauptunterschied zum 
`public`-Ordner ist, dass dieser Ordner aus dem `react`-Framework kommt und nicht von `vite`. Dadurch ist der 
`import` anders.

#### 2.4.1. Beispiel
Im neu erstellen `vite`-Projekt wird die Datei `react.svg` im `assets`-Ordner abgelegt. In der `App.tsx` wird die 
Grafik dann wie folgt eingebunden:
```tsx
import reactLogo from './assets/react.svg';
```
```html
<img src={reactLogo} className="logo react" alt="React logo" />
```
Im Vergleich mit dem `public`-Ordner wird hier der Pfad relativ zum aktuellen Verzeichnis angegeben.

---
### 2.5. App.css
Dies ist die CSS-Datei, die für die `App.tsx` verwendet wird. Hier sollen Styles für die `App.tsx` definiert werden. 

__! Hinweis:__ In `react`-Projekten sollte jede Komponente ihre eigene CSS-Datei erhalten.

__! Wichtig:__ Hierbei muss auf die CSS-Style-Klassen aufgepasst werden, dass diese für die Komponente eindeutig sind, da alle CSS-Dateien in einem 
Projekt überall zählen und es sonst zu Überschreibung der Styles kommen kann.

---
### 2.6. App.tsx
Dies ist standardmäßig die Hauptdatei des Projekts. Hier wird die `App`-Komponente definiert, über welche dann das 
Projekt aufgebaut wird.

---
### 2.7. index.css
Dies ist die CSS-Datei, die für die `main.tsx`-Komponente verwendet wird.

---
### 2.8. main.tsx
Dies ist der Einstiegspunkt für ein `react`-Projekt. Hier wird standardmäßig die Wurzel für unsere `react`-Anwendung 
erstellt:
```tsx
ReactDOM.createRoot(document.getElementById('root')!).render(
    <React.StrictMode>
        <App />
    </React.StrictMode>,
)
```

---
### 2.9. .gitignore
In dieser Datei werden Dateien und Ordner definiert, die nicht in das Git-Repository aufgenommen werden sollen.

---
### 2.10. index.html
Dies ist die Datei, auf welche der mit `npm run dev` gestartete Server zugreift.

---
### 2.11. package.json
In dieser Datei werden alle Abhängigkeiten und Skripte definiert, die für das Projekt relevant sind. Sie ist quasi 
das Äquivalent zur `pom.xml` in `java` mit `Maven`.

---
## 3. React Grundlagen
### 3.1. JSX
`JSX` ist eine Syntaxerweiterung für `JavaScript` und `TypeScript`. Es wird verwendet, um `react`-Elemente zu erstellen.

#### 3.1.1. Beispiel
```tsx
const element = <h1>Hello, world!</h1>;
```
---


## Links
- [Handout](https://github.com/neuefische/hh-java-24-1-handouts/blob/main/5-Frontend/06-React-Project/README.md)
- [Challenge](https://github.com/neuefische/hh-java-24-1-handouts/blob/main/5-Frontend/06-React-Project/challenges.md)
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
├─ [public](#21-public)\
│   └─ [vite.svg](#22-vitesvg)\
├─ [src](#23-src)\
│  ├─ [assets](#24-assets)\
│  │   \
│  ├─ [App.css](#25-appcss)\
│  ├─ [App.tsx](#26-apptsx)\
│  ├─ [index.css](#27-indexcss)\
│  └─ [main.tsx](#28-maintsx)\
├─ [.gitignore](#29-gitignore)\
├─ [index.html](#210-indexhtml)\
└─ [package.json](#211-packagejson)

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
Dies ist die CSS-Datei, die für die `main.tsx`-Komponente verwendet wird. Hier sollten `body`- und `html`-Styles
gesetzt werden, bzw. im allgemeinen Styles, die für das gesamte Projekt gelten und nicht mehr verändert werden sollten.

---
### 2.11. package.json
In dieser Datei werden alle Abhängigkeiten und Skripte definiert, die für das Projekt relevant sind. Sie ist quasi
das Äquivalent zur `pom.xml` in `java` mit `Maven`.

---
## 3. React Grundlagen
### 3.1. JSX
`JSX` ist eine Syntaxerweiterung für `JavaScript` und `TypeScript`. Es wird verwendet, um `react`-Elemente zu erstellen. Der Rückgabewert einer Komponente muss immer ein `JSX`-Element sein.

#### 3.1.1. Beispiel
```tsx
const element = <h1>Hello, world!</h1>;
```
---

#### 3.1.2. Beispiel
```jsx
function App() {
  return (
          <div>
            <h1>Hello, world!</h1>
          </div>
  );
}
```
---

### 3.2. React-Code Aufbau
Die `App.tsx`-Datei hat im `vite`-Projekt erstmal die folgende Form:
```jsx
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'

function App() {
  const [count, setCount] = useState(0)

  return (
          <>
            <div>
              <a href="https://vitejs.dev" target="_blank">
                <img src={viteLogo} className="logo" alt="Vite logo" />
              </a>
              <a href="https://react.dev" target="_blank">
                <img src={reactLogo} className="logo react" alt="React logo" />
              </a>
            </div>
            <h1>Vite + React</h1>
            <div className="card">
              <button onClick={() => setCount((count) => count + 1)}>
                count is {count}
              </button>
              <p>
                Edit <code>src/App.tsx</code> and save to test HMR
              </p>
            </div>
            <p className="read-the-docs">
              Click on the Vite and React logos to learn more
            </p>
          </>
  )
}

export default App
```

Wie auch in Java werden hier erstmal alle benötigten Imports gemacht. Danach wird die `App`-Komponente definiert und
am Ende exportiert. Letzteres kann man auch zusammen in einer Zeile machen:
```jsx
export default function App() {
  // ...
}
```
---
### 3.3. Import
In `react`-Projekten haben wir erstmal 3 Möglichkeiten Dinge zu importieren. Wollen wir nur eine Funktion aus einer
anderen Datei importieren, können wir das wie folgt machen:
```tsx
import { funktionsName } from './Datei';
```

Wollen wir mehrere Funktionen importieren, können wir das wie folgt machen:
```tsx
import { funktionsName1, funktionsName2 } from './Datei';
```

Alternativ können wir auch die als 'default' exportierte Funktion importieren:
```tsx
import funktionsName from './Datei';
```

Zu guter Letzt arbeiten wir auch mit `hmtl`-Code, weshalb wir auch CSS-Dateien importieren sollten. Das machen wir
wie folgt:
```tsx
import './Datei.css';
```

---
### 3.4. Export
In `react`-Projekten haben wir erstmal 2 Möglichkeiten Dinge zu exportieren. Wollen wir nur eine Funktion exportieren,
können wir das wie folgt machen:
```tsx
export function funktionsName() {
  // ...
}
```

Alternativ können wir auch die Funktion als 'default' exportieren:
```tsx
export default function funktionsName() {
  // ...
}
```

---
### 3.5. Komponenten
In `react`-Projekten arbeiten wir mit Komponenten. Eine Komponente ist eine Funktion, die `JSX`-Elemente zurückgibt.
Man sollte für jede Komponente eine eigene `tsx`-Datei erstellen, sowie eine CSS-Datei gleichen namens.

In einer Komponente können wir auch andere Komponenten verwenden. Das machen wir wie folgt:
```tsx
import './Komponente.css';

export default function Komponente() {
  return (
          <div>
            <h1>Ich bin eine Komponente</h1>
          </div>
  );
}
```
---

### 3.6. Komponenten dynamisch erstellen
Der große Vorteil von `react` gegenüber `html` ist, dass wir Komponenten dynamisch erstellen können. Das können wir
wie folgt machen:
```tsx
import './Komponente.css';

export default function Komponente(): JSX.Element {
  const anzahl:number = 5;
  const komponenten:JSX.Element[] = [];

  for (let i = 0; i < anzahl; i++) {
    komponenten.push(<Komponente key={i} />);
  }

  return (
          <div>
            {komponenten}
          </div>
  );
}
```
Hier wird ein Array `komponenten` erstellt, welches mit `JSX`-Elementen gefüllt wird. Diese werden dann in der
`return`-Methode ausgegeben.

__! Hinweis:__ Was das `key`-Attribut macht, wird später (nicht hier, bestimmt) erklärt.

#### 3.6.1. Komponente dynamisch mit eigenen Datentypen erstellen
Wir müssen aber nicht mit vorgefertigten Datentypen arbeiten, wir können auch mit TypeScript eigene Datentypen:
```tsx
type Cat = {
  name: string;
  age: number;
  color: string;
}
```

Diese können wir dann in einer Komponente verwenden:
```tsx
import './Komponente.css';

export default function Komponente({ name, age, color }: Cat): JSX.Element {
  return (
          <div>
            <h1>{name}</h1>
            <p>{age}</p>
            <p>{color}</p>
          </div>
  );
}
```

Hätten wir eine Liste von `Cat`-Objekten, könnten wir diese wie folgt in einer Komponente verwenden:
```tsx
import './Komponente.css';

export default function Komponente({ cats }: { cats: Cat[] }): JSX.Element {
  return (
          <div>
            {cats.map((cat, index) => (
                    <Komponente key={index} {...cat} />
            ))}
          </div>
  );
}
```
## Links
- [Handout](https://github.com/neuefische/hh-java-24-1-handouts/blob/main/5-Frontend/06-React-Project/README.md)
- [Challenge](https://github.com/neuefische/hh-java-24-1-handouts/blob/main/5-Frontend/06-React-Project/challenges.md)
- [React-Tutorial](https://react.dev/learn/tutorial-tic-tac-toe)
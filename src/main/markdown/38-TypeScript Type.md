# TypeScript - Type
Im Unterschied zu `JavaScript` ist `TypeScript` eine typisierte Sprache. Das bedeutet, dass Variablen, Parameter und Rückgabewerte von Funktionen einen Typ haben können. Dies ermöglicht es, Fehler frühzeitig zu erkennen und die Codequalität zu verbessern.

### TypeScript - Types Cheat Sheet

#### 1. Grundlegende Datentypen
| Typ                  | Beschreibung                                       |
|----------------------|----------------------------------------------------|
| `number`             | Numerische Werte, z.B. `5`, `3.14`, `-10`.         |
| `string`             | Zeichenketten, z.B. `'Hello'`, `"World"`, `'123'`. |
| `boolean`            | Wahrheitswerte, `true` oder `false`.               |
| `null`               | Der Typ mit nur dem Wert `null`.                   |
| `undefined`          | Der Typ mit nur dem Wert `undefined`.              |
| `any`                | Ein dynamischer Typ, der für alles verwendet wird. |

#### 2. Zusätzliche Datentypen
| Typ                     | Beschreibung                                                                                    |
|-------------------------|-------------------------------------------------------------------------------------------------|
| `void`                  | Der Rückgabetyp für Funktionen, die keinen Wert zurückgeben.                                    |
| [`never`](#21-Beispiel) | Ein Typ, der niemals einen Wert hat. Wird primär als nicht erreichbarer Rückgabewert verwendet. |
| `unknown`               | Ähnlich wie `any`, muss vor einer Verwendung aber auf einen Typ überprüft/ typisiert werden.    |
| `object`                | Ein nicht-primitiver Datentyp, der nicht `null` ist.                                            |
| `Array<ElementType>`    | Ein Array mit Elementen vom Typ `ElementType`.                                                  |
| `Tuple`                 | Ein Array mit einer festen Anzahl von Elementen und festen Typen.                               |
| `BigInt`                | Ein numerischer Datentyp, der beliebig große Zahlen speichern kann.                             |



##### 2.1. Beispiel
Beispiel für den Typ `never`:
```typescript
function throwError(message: string): never {
    throw new Error(message);
}
```

#### 3. Typ-Modifikatoren
| Symbol                     | Beschreibung                                      |
|----------------------------|---------------------------------------------------|
| [`readonly`](#31-Beispiel) | Eine schreibgeschützte Variable oder Eigenschaft. |
| `?`                        | Optionales Attribut in einem Typ.                 |
| `\|`                       | Union-Typ, erlaubt Werte aus verschiedenen Typen. |
| `&`                        | Intersection-Typ, kombiniert verschiedene Typen.  |

##### 3.1. Beispiel
Beispiel für den Typ-Modifikator `readonly`:
```typescript
class Person {
    readonly name: string;
    readonly age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}
```

##### 3.2. Beispiel
Beispiel für den Intersection-Typ:
```typescript
interface Animal {
    name: string;
    age: number;
}

interface Bird {
    fly: () => void;
}

// Intersection-Typ
type BirdAnimal = Animal & Bird;

// Objekt erstellen, das sowohl Animal- als auch Bird-Eigenschaften hat
const birdAnimal: BirdAnimal = {
    name: "Sparrow",
    age: 2,
    fly: () => {
        console.log("The sparrow is flying.");
    }
};
```


#### 4. Typisierung
Man definiert einen Datentyp in TypeScript mit dem `type`-Schlüsselwort:
```typescript
type MyType = {
    name: string;
    age?: number;
};
```

#### 5. Funktionstypen
    
```typescript
type MyFunc = (param1: number, param2: string) => boolean;
```

#### 6. Typüberprüfung

```typescript
const myVar: number = 5;
```

#### 7. Generische Typen

```typescript
function myFunction<T>(arg: T): T {
    return arg;
}
```

#### 8. Zusammengesetzte Typen

```ts
type User = {
    name: string;
    age: number;
};

type Admin = {
    name: string;
    role: string;
};

type UserOrAdmin = User | Admin;
```

#### 9. Spread-Operator
Der Spread-Operator (`...`) in TypeScript wird verwendet, um Elemente aus einem Array oder Eigenschaften aus einem Objekt zu "verbreiten" oder auszubreiten. Es ermöglicht, die Elemente eines Arrays oder die Eigenschaften eines Objekts an anderer Stelle einzufügen oder zu kombinieren.
```ts
type Cat = {
    id: string;
    name: string;
    color: string;
}

const cat: Cat = {
    id: "1",
    name: "Whiskers",
    color: "black"
}

const updatedCat: Cat = {
    ...cat,
    breed: "Britisch Shorthair"
}
```
Man kann den Spread-Operator auch verwenden um Objekte zu kombinieren:
```ts
const array1 = [1, 2, 3];
const array2 = [4, 5, 6];

// Kombinieren von Arrays
const combinedArray = [...array1, ...array2]; // Ergebnis: [1, 2, 3, 4, 5, 6]

// Kopieren eines Arrays
const copiedArray = [...array1]; // Ergebnis: [1, 2, 3]
```

Oder auch um Objekte zu kopieren und teilweise zu verändern:
```ts
type Cat = {
    id: string;
    name: string;
    color: string;
}

const cat: Cat = {
    id: "1",
    name: "Whiskers",
    color: "black"
}

const updatedCat: Cat = {
    ...cat,
    color: "orange"
}
```
Letzteres ist aber "mit Vorsicht zu genießen".


## Links
- [Handout](https://github.com/neuefische/hh-java-24-1-handouts/blob/main/5-Frontend/05-TypeScript-Type/README.md)
- [Challenge](https://github.com/neuefische/hh-java-24-1-handouts/blob/main/5-Frontend/05-TypeScript-Type/challenges.md)
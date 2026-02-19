---
layout: two-cols-header
hideInToc: true
---

# Warum Frameworks?
### Ohne Frameworks

::right::

```html [vanilla-example.html] {all|5|7,10|9}{lines:true}
<button id="button">Klicks: 0</button>

<script>
let count = 0
const button = document.querySelector("#button")

button.addEventListener("click", () => {
  count++
  button.textContent = "Klicks: " + count
})
</script>
```

::left::

<v-clicks at="1">

- Element finden
- `click` event handler
- Text manuell ändern

</v-clicks>

<!--
- HTML Element finden
- Event handler definieren
- Text manuell ändern
- Umständlich und schnell komplex
-->

---
layout: two-cols-header
---

# Warum Frameworks?
### Mit Vue

::right::

```vue [vue-example.vue] {all|4|9|8|all}{lines:true}
<script setup>
const count = ref(0)
</script>

<template>
  <button @click="count++">
    Klicks: {{ count }}
  </button>
</template>
```

::left::

<v-clicks at="1">

- Reaktive Variable definieren
- Variable im Markup-Template binden
- Handler im Markup-Template binden

</v-clicks>


<v-click at="4">

## Vorteile

</v-click>

<v-clicks at="5">

- Schnellere Entwicklung
- Weniger Komplexität
- Automatische UI-Updates
- Wiederverwendbarkeit

</v-clicks>

<!--
- Schnellere Entwicklung: viele Funktionen sind bereits fertig vorhanden
- Weniger Komplexität: klare Struktur statt chaotischem Code
- Automatische UI-Updates: Änderungen an Daten spiegeln sich sofort in der Oberfläche wider
- Komponentensystem für Wiederverwendung
-->

---
layout: center
---
# Warum vue?
<v-clicks>

- Vue ist auf Platz 2 der most desired Frontend Frameworks (StackOverflow Survey)
- Einsteigerfreundliche Lernkurve
- Geringe Menge an Boilerplate

</v-clicks>

<!--
- 23k Befragte https://survey.stackoverflow.co/2025/technology#2-web-frameworks-and-technologies
- Vue ist sehr bekannt und hat sich als zuverlässiges Framework etabliert
- Nr1 React
- Nr3 Angular
- Einfach zu lernen aufgrund der HTML ähnlichen Templates
- Komponenten trennen klar Logik, UI und Styles voneinander

 -->

---
layout: two-cols-header
---

# Template Syntax

::left::
### HTML-basierte Templates
Vue nutzt eine deklarative, leicht verständliche Template-Syntax

### Klare Struktur
Code wird in Logik, Markup und Style klar unterteilt

 ### Direkte Datenbindung
DOM ist automatisch mit den Komponentendaten verknüpft

### Effiziente Updates
Reaktivität sorgt für minimale DOM-Änderungen bei State-Updates


::right::
<v-click>

### Text Interpolation
```vue
<span>Message: {{ msg }}</span>
```
</v-click>

<v-click>

### Attribute Bindings
````md magic-move
```vue
<div v-bind:id="dynamicId"></div>
```

```vue
<div :id="dynamicId"></div>
```
````
</v-click>

<v-click>

### Binding Multiple Attributes

```ts
const objectOfAttrs = {
  id: 'container',
  class: 'wrapper',
  style: 'background-color:green'
}
````

```vue
<div v-bind="objectOfAttrs"></div>
```

</v-click>

<!--
- Templates sind HTML-nah und damit fuer viele sofort lesbar.
- Interpolation `{{ }}` rendert Daten im Text, Attribute laufen ueber `v-bind` bzw. `:`.
- Directives sind Vue-spezifische Attribute und kapseln Logik im Markup.
- Datenfluss ist deklarativ: Template beschreibt das Ergebnis, nicht die DOM-Schritte.
- Reaktivitaet sorgt dafuer, dass sich die Anzeige automatisch anpasst.
-->

---
layout: center
---

# Reaktivität

````md magic-move [reactivity.vue]
```vue
<script setup>
let count = 0
count // 0
</script>
```
```vue
<script setup>
const count = ref(0)
count.value // 0
</script>
```
```vue
<script setup>
const count = ref(0)
count.value // 0
</script>

<template>
  <p>Count: {{ count }}</p>
</template>
```
```vue
<script setup>
const state = reactive({ count: 0 })
state.count // 0
</script>

<template>
  <p>Count: {{ state.count }}</p>
</template>
```
````

<!--
* **Reaktivität = automatische UI-Updates**
  * Wenn sich Daten ändern, aktualisiert Vue die Oberfläche selbst
* **`ref()` → für einzelne Werte**
  * macht primitive Werte reaktiv (Zahl, String, Boolean)
  * Zugriff in JS mit `.value`
* **Warum `.value`?**
  * `ref` ist ein Wrapper-Objekt um den echten Wert
  * `.value` greift auf den inneren Wert zu
* **`reactive()` → für Objekte**
  * macht komplette Objekte reaktiv
  * kein `.value` nötig
* **Im Template wichtig:**
  * `.value` wird dort automatisch „entpackt“
  * man kann direkt `{{ count }}` schreiben
-->

---
layout: two-cols-header
---
# Computed Properties

::left::

- Erzeugen neue Werte aus vorhandenen Daten

<br>

- Aktualisieren sich bei Änderung abhängiger Daten

<br>

- Werden nur neu berechnet, wenn sich Abhängigkeiten ändern

<br>

- Halten Berechnungslogik außerhalb des Templates


::right::
````md magic-move [computed.vue]
```vue {all|14|all}
<script setup>
const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})
</script>

<template>
  <p>Has published books:</p>
  <span>{{ author.books.length > 0 ? 'Yes' : 'No' }}</span>
</template>
```

```vue {all|11-13|18|all}
<script setup>
const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})
</script>

<template>
  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>
</template>
```
````
<!--
 - Computed Properties berechnen Werte aus vorhandenem State
- Im ersten Beispiel steht die Logik direkt im Template
- Solche Ausdrücke werden schnell unübersichtlich und schwer wartbar

- Im zweiten Beispiel wird die Berechnung in eine Computed Property ausgelagert
- Die Logik liegt im Script statt im Template
- Das Template bleibt dadurch sauber und leichter lesbar

- Computed Properties sind reaktiv und aktualisieren sich automatisch bei Datenänderungen
- Sie werden nur neu berechnet, wenn sich ihre Abhängigkeiten ändern

- Hauptvorteil: bessere Lesbarkeit und klare Trennung von Logik und Darstellung
 -->

---
layout: center
---

# Options vs Composition API

````md magic-move
```ts
const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})
```
```ts
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  },
  computed: {
    // a computed getter
    publishedBooksMessage() {
      // `this` points to the component instance
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  }
}
```
````

<v-click>
<img src="/composition-api.png" alt="Options vs Composition API" class="absolute top-1/2 left-1/2 -translate-1/2 max-h-[90%] mx-auto invert rounded-xl" />
</v-click>

<!--
* **Options API = nach Kategorien organisiert**
  * Code in Blöcken wie `data`, `methods`, `computed`
  * leichter zu lesen für Anfänger
* **Composition API = nach Logik organisiert**
  * zusammengehörige Funktionalität steht an einem Ort
  * besser für große und komplexe Apps
* **Wiederverwendbarkeit**
  * Options: schwierig Logik sauber zu teilen
  * Composition: einfach über Composables
* **Code-Struktur**
  * Options: „was ist es?“ (Methoden, Daten, etc.)
  * Composition: „wofür ist es?“ (Feature-basiert)
* **TypeScript-Support**
  * Composition API deutlich besser geeignet
  * Paul stinkt!!
* **Kurz:**
  * Options API → einfacher Einstieg
  * Composition API → mehr Flexibilität & Skalierbarkeit

- bild zeigt wie code, der sich mit selben logischen aufgabe auseinanderfasst
-->

---
layout: two-cols-header
---

# Conditional Rendering & Iteration

::left::

<v-clicks at="1">

- `v-if` / `v-else`: rendert Inhalte nur bei erfüllter Bedingung
- `v-show`: bleibt im DOM, schaltet nur `display` um
- `v-for`: rendert Listen aus Arrays

</v-clicks>

::right::

```vue {all|16,19|16,19|17|all}{lines:true}
<script setup>
import { computed, ref } from "vue"

const showTodos = ref(true)
const todos = ref([
  { id: 1, text: "Slides vorbereiten", done: false },
  { id: 2, text: "Demo prüfen", done: true },
  { id: 3, text: "Fragen sammeln", done: false },
])

const openTodos = computed(() => todos.value.filter((todo) => !todo.done))
</script>

<template>
  <button @click="showTodos = !showTodos">Liste umschalten</button>
  <ul v-if="showTodos && openTodos.length">
    <li v-for="todo in openTodos" :key="todo.id">{{ todo.text }}</li>
  </ul>
  <p v-else>Keine offenen Aufgaben</p>
</template>
```

<!--
- kurzes beispiel für konditionales und iteratives rendering
- genauere erklärung bei live example nachher
- `v-if` / `v-else`: rendert Inhalte nur bei erfüllter Bedingung
- `v-show`: bleibt im DOM, schaltet nur `display` um
- `v-for`: rendert Listen aus Arrays
-->

---
layout: two-cols-header
---

# Event Handling

::left::

<v-clicks at="1">

- `v-on` bindet DOM-Events (`@click` als Kurzform)
- Inline-Handler für kleine, direkte Aktionen
- Komplexere Logik in Funktionen aus `<script setup>`
- Event Modifier wie `.once`, `.prevent`, `.stop`
- Weniger Boilerplate als mit `addEventListener`

</v-clicks>

::right::

````md magic-move [event-handling.vue]
```vue
<script setup>
const count = ref(0)
</script>

<template>
  <button>Klicks: {{ count }}</button>
</template>
```

```vue
<script setup>
const count = ref(0)
</script>

<template>
  <button>Klicks: {{ count }}</button>
</template>
```

```vue
<script setup>
const count = ref(0)
</script>

<template>
  <button @click="count++">Klicks: {{ count }}</button>
</template>
```

```vue
<script setup>
const count = ref(0)

function increment(step = 1) {
  count.value += step
}
</script>

<template>
  <button @click="increment()">Klicks: {{ count }}</button>
</template>
```

```vue
<script setup>
const count = ref(0)

function increment(step = 1) {
  count.value += step
}
</script>

<template>
  <button @click="increment()">Klicks: {{ count }}</button>
  <button @click.once="increment(5)">Bonus +5</button>
</template>
```
````

<!--
- Schritt 1: Noch kein Event gebunden
- Schritt 2: Inline Event Binding mit @click
- Schritt 3: Logik sauber in eine Funktion auslagern
- Schritt 4: Modifier (.once) als declaratives Verhalten
-->

---
layout: two-cols-header
---

# Input Bindings (`v-model`)

::left::

<v-clicks at="1">

- Input-Wert an reaktiven State binden
- Manuell mit `:value` + `@input` möglich
- `v-model` kombiniert beides in einer Direktive
- Funktioniert für `input`, `textarea`, `select`, Checkbox
- Modifier wie `.trim`, `.number`, `.lazy`

</v-clicks>

::right::

````md magic-move [input-bindings.vue]
```vue
<script setup>
const name = ref("")
</script>

<template>
  <input placeholder="Dein Name" />
  <p>Hallo {{ name }}</p>
</template>
```

```vue
<script setup>
const name = ref("")
</script>

<template>
  <input
    :value="name"
    @input="name = $event.target.value"
    placeholder="Dein Name"
  />
  <p>Hallo {{ name }}</p>
</template>
```

```vue
<script setup>
const name = ref("")
</script>

<template>
  <input v-model="name" placeholder="Dein Name" />
  <p>Hallo {{ name }}</p>
</template>
```

```vue
<script setup>
const name = ref("")
</script>

<template>
  <input v-model.trim="name" placeholder="Dein Name" />
  <p>Hallo {{ name || "Unbekannt" }}</p>
</template>
```
````

<!--
- Schritt 1: UI ohne echte Bindung
- Schritt 2: Zwei-Wege-Bindung manuell aufbauen
- Schritt 3: Gleiche Logik mit v-model kompakt ausdrücken
- Schritt 4: Modifier für robuste Input-Daten
-->

---
# try also 'default' to start simple
theme: apple-basic
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
info: |
  ## Getting started with Vue für Mobil-apps!!!
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# duration of the presentation
duration: 35min
fonts:
  sans: TeleNeo Office
  mono: Fira Code
layout: center
---

<img src="/Vue.js_Logo_2.svg.png" alt="Vue.js" class="h-18 w-auto mx-auto my-6" />

<h1>
Vue
</h1>

<span class="opacity-50 text-xl">/vjuː/</span>

---
layout: two-cols-header
---

# Warum Frameworks?
### Ohne Frameworks

::right::

```html [vanilla-example.html] {all|5|7,10|9}{lines:true}
<button id="btn">Klicks: 0</button>

<script>
let count = 0;
const btn = document.getElementById("btn");

btn.addEventListener("click", () => {
  count++;
  btn.textContent = "Klicks: " + count;
});
</script>
```

::left::

<v-clicks at="1">

- element finden
- `click` event handler
- text manuell ändern

</v-clicks>

<!--
- Schnellere Entwicklung: viele Funktionen sind bereits fertig vorhanden
- Weniger Komplexität: klare Struktur statt chaotischem Code
- Automatische UI-Updates: Änderungen an Daten spiegeln sich sofort in der Oberfläche wider
- Komponentensystem für Wiederverwendung
-->

---
layout: two-cols-header
---

# Warum Frameworks?
### Mit Vue

::right::

```vue [vue-example.vue] {all|4|9|8|all}{lines:true}
<script setup>
import { ref } from "vue";

const count = ref(0);
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

- Schnellere Entwicklung
- Weniger Komplexität
- Automatische UI-Updates
- Wiederverwendbarkeit

</v-click>

<!--
- Button klick handler → Element suchen → Text manuell ändern
- Schnellere Entwicklung: viele Funktionen sind bereits fertig vorhanden
- Weniger Komplexität: klare Struktur statt chaotischem Code
- Automatische UI-Updates: Änderungen an Daten spiegeln sich sofort in der Oberfläche wider
- Komponentensystem für Wiederverwendung
-->

---
layout: center
---
# Warum vue?
<v-click>
- Vue ist auf Platz 3 der most desired Web Frameworks
- Einsteigerfreundliche Lernkurve
- Geringe Menge an Boilerplate

</v-click>

<!--
- 23k Befragte https://survey.stackoverflow.co/2025/technology#2-web-frameworks-and-technologies
- Einfach zu lernen aufgrund der HTML ähnlichen Templates
- Komponenten trennen klar Logik, UI und Styles voneinander

 -->




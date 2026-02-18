---
layout: center
hideInToc: true
---

# Angular vs Vue

Minimal Template
````md magic-move
```ts
// angular
import { Component } from "@angular/core";

@Component({
  selector: "app-hello-world",
  template: `<h1>Hello world</h1>`,
})
export class HelloWorldComponent {}
```

```vue
<!-- vue -->
<template>
  <h1>Hello world</h1>
</template>
```
````


<!--
**Angular**
- Component = Klasse mit `@Component`.
- Template im Decorator definiert.
- Viel Struktur und Boilerplate.

**Nachteile der Syntax**
- Sehr verbose für einfache UI.
- Viel „Framework-Code“ für wenig Ergebnis.
- Für Einsteiger schwerer zu lesen.

**Vue**
- Template direkt im `<template>`.
- Keine Klassen oder Decorators nötig.
- Sehr kompakt.
 -->
---
layout: center
hideInToc: true
---
# Angular vs Vue

Direkter Zugriff auf HTML Element

````md magic-move
```ts
import {
  afterNextRender,
  Component,
  ElementRef,
  viewChild,
} from "@angular/core";

@Component({
  selector: "app-input-focused",
  template: `<input type="text" #inputRef />`,
})
export class InputFocusedComponent {
  inputRef = viewChild.required<ElementRef<HTMLInputElement>>("inputRef");

  constructor() {
    afterNextRender({ write: () => this.inputRef().nativeElement.focus() });
  }
}
```
```vue
<script setup>
import { useTemplateRef, onMounted } from "vue";

const inputElement = useTemplateRef("inputElement");

onMounted(() => {
  inputElement.value.focus();
});
</script>

<template>
  <input ref="inputElement" />
</template>
```
````

<!-- **Angular**
- `viewChild` + `ElementRef`.
- Lifecycle nötig für Zugriff.
- Stark typisiert.

**Nachteile der Syntax**
- Viele Imports für einfache Aufgabe.
- Sehr technisch für etwas Simples wie `focus()`.
- Lifecycle-Abhängigkeit macht Code unübersichtlicher.

**Vue**
- `ref` im Template.
- Zugriff mit `onMounted`.
- Sehr kurze Syntax.
 -->
---
layout: center
hideInToc: true
---

# Angular vs Vue

Component Importieren

````md magic-move
```ts
import { Component } from "@angular/core";
import { UserprofileComponent } from "./userprofile.component";

@Component({
  selector: "app-root",
  imports: [UserprofileComponent],
  template: `
    <app-userprofile
      name="John"
      [age]="20"
      [favouriteColors]="['green', 'blue', 'red']"
      [isAvailable]="true"
    />
  `,
})
export class AppComponent {}
```

```vue
<script setup>
import UserProfile from "./UserProfile.vue";
</script>

<template>
  <UserProfile
    name="John"
    :age="20"
    :favourite-colors="['green', 'blue', 'red']"
    is-available
  />
</template>
```
````

<!--

**Angular**
- Import im `imports`-Array.
- Bindings mit `[prop]="value"`.
- Unterschiedliche Syntax für Strings / Booleans.

**Nachteile der Syntax**
- Viele Sonderregeln zum Merken.
- Template wirkt schnell „überladen“.
- Weniger HTML-ähnlich.

**Vue**
- Import im `<script setup>`.
- `:` für Bindings.
- Boolean-Props ohne Wert.
 -->



---
layout: center
---

# Nuxt: Vue als Full-Stack Framework

<v-clicks>

- Baut auf Vue 3 auf, ergänzt um Server-Engine (`Nitro`)
- File-based Routing über den `pages/`-Ordner
- API-Endpunkte direkt im Projekt über `server/api/`
- SSR, SSG und SPA in einem Framework

</v-clicks>

```txt
app/
  pages/
  components/
  server/api/
  nuxt.config.ts
```

---
layout: two-cols-header
---

# Vorteile im Entwickleralltag

::left::

<v-clicks>

- Weniger Boilerplate: Routing, Layouts und Auto-Imports sind eingebaut
- Schnellere Features durch Konventionen statt Setup
- Einheitliche Struktur macht Onboarding einfacher
- Module für typische Themen wie Auth, i18n oder Analytics

</v-clicks>

::right::

```vue
<!-- pages/users.vue -->
<script setup lang="ts">
const { data: users, pending, error } = await useFetch('/api/users')
</script>

<template>
  <p v-if="pending">Lädt...</p>
  <p v-else-if="error">Fehler beim Laden</p>
  <ul v-else>
    <li v-for="user in users" :key="user.id">{{ user.name }}</li>
  </ul>
</template>
```

---
layout: two-cols-header
---

# Auto-Imports & DX in Nuxt

::left::

<v-clicks>

- Vue APIs wie `ref`, `computed` und `watch` sind direkt verfügbar
- Nuxt Composables (`useFetch`, `useAsyncData`, `navigateTo`) ohne manuelle Imports
- Komponenten aus `components/` werden automatisch registriert
- Typen werden automatisch generiert, ideal für TypeScript + IDE
- Ergebnis: weniger Boilerplate, schnelleres Entwickeln

</v-clicks>

::right::

````md magic-move
```vue
<script setup lang="ts">
import { ref, computed } from 'vue'
import UserCard from '~/components/UserCard.vue'
import { useRoute } from '#imports'

const route = useRoute()
const count = ref(0)
const doubled = computed(() => count.value * 2)
</script>
```

```vue
<script setup lang="ts">
const route = useRoute()
const count = ref(0)
const doubled = computed(() => count.value * 2)
</script>

<template>
  <UserCard :id="route.params.id" />
</template>
```
````

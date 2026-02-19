---
layout: two-cols-header
---

# Was ist Capacitor.js?

::left::

<img src="/capacitor.png" alt="Capacitor Logo" class="h-24 w-auto mx-auto my-6" />

::right::

<v-clicks>

- Native Runtime von Ionic für Webanwendungen
- Compiled Anwendungen aus Vue, Nuxt oder Vite als iOS- und Android-App
- Zugriff auf Gerätefunktionen über Plugins (z. B. Kamera, GPS, Dateisystem)
- Eine gemeinsame Codebasis für Web und Mobile

</v-clicks>

---
layout: two-cols-header
---

# Wie funktioniert Capacitor?

::left::

<v-clicks>

- Zunächst wird die Webanwendung gebaut (`dist/`)
- Capacitor kopiert das Build-Ergebnis in native Projekte (`ios/`, `android/`)
- Eine native Shell stellt die Anwendung in einer WebView bereit
- Plugins vermitteln zwischen JavaScript und nativen APIs

</v-clicks>

::right::

```mermaid
flowchart TD
    B["Vue App (HTML/CSS/JS)"]
    B --> C["dist/"]
    C --> D["cap sync"]
    D --> E["ios + android"]
```


---
layout: two-cols-header
---

# Vor- und Nachteile

::left::

## Vorteile

<v-clicks>

- Schneller Übergang von Web zu mobilen Plattformen
- Weiterverwendung bestehender Vue- und TypeScript-Kompetenzen im Team
- Plugins für viele Standardfunktionen sind verfügbar
- Besonders geeignet für Business-Anwendungen und interne Tools

</v-clicks>

::right::

## Nachteile

<v-clicks>

- Eine stark plattformspezifische UI/UX erfordert zusätzliche Anpassungen
- Bei Plugin-Lücken kann die Entwicklung eigener nativer Plugins notwendig sein
- Build-, Signatur- und Store-Prozesse bleiben weiterhin komplex
- Bei grafikintensiven Anwendungen können Performance-Grenzen auftreten

</v-clicks>

---
layout: center
---

# Development Workflow

<v-clicks>

1. Webanwendung entwickeln (`pnpm dev`)
2. Produktions-Build erzeugen (`pnpm build`)
3. Capacitor initialisieren (`npx cap init`)
4. Plattform hinzufügen (`npx cap add ios` / `npx cap add android`)
5. Änderungen synchronisieren (`npx cap sync`)
6. Native Projekt starten (`npx cap open ios` / `npx cap open android`)
7. In Xcode bzw. Android Studio bauen, testen und signieren

</v-clicks>

# Vue Lab — Helpdesk

![Vue.js](vue-anime.png)

**Статус: ⚪ методичка готова, прохождение впереди.**
**Сложность: высокая, если фронтенд — новая территория.** Нужен уверенный JavaScript (ES6+, async/await, деструктуризация); опыт с Vue или другими фреймворками не требуется, готовый мини-бэкенд (Node) дан за вас.

## О чём

Helpdesk (система тикетов) на Vue 3 с нуля — реактивность, компоненты, роутинг и общее состояние, каждое понятие на одном сквозном примере. Бэкенд (готовый мини-бэкенд на Node) дан в первой же сессии — писать его не нужно, только запустить.

## Стек

Vue 3.5 + Vite 6+ + Vue Router 4 + Pinia 2+ + Vitest, бэкенд — готовый мини-бэкенд (Node). Composition API + `<script setup>` (Options API — только в теории для сравнения). Всё в Docker.

## Формат

Методичка [`Vue_Lab_Helpdesk.html`](Vue_Lab_Helpdesk.html) — открывается в браузере.

## Что внутри (5 сессий, порядок строгий — Pinia раньше Router, потому что guard'ам роутера нужен auth-store)

- **Сессия 1** — стенд (`docker-compose`, скаффолд готового бэкенда и `create-vue`); готовый мини-бэкенд на Node (auth, tickets, comments, history, WebSocket-gateway) — дан готовым; песочница реактивности: `ref`/`reactive`/`computed`/`watch`, директивы, `v-model`, `v-for`/`key`; `useAsync` и первый запрос к API
- **Сессия 2** — разбор списка тикетов на компоненты: `StatusBadge`, `TicketCard`, `TicketList` (props/emits, слоты); `BaseModal` (слоты, Teleport, lifecycle, template refs); тосты через `provide`/`inject`; composable `useNow`/`RelativeTime`
- **Сессия 3** — Pinia: `state`/`getters`/`actions`, `storeToRefs`, auth-стор с токеном, persist-плагин; оптимистичная смена статуса тикета с откатом при ошибке
- **Сессия 4** — Vue Router: маршруты, lazy loading, `RouterLink`, guards (`requiresAuth`, роли, redirect после логина), вложенные маршруты, query-синхронизация, 404; страница тикета с вкладками, форма создания, `onBeforeRouteLeave`
- **Сессия 5** — WebSocket (`useSocket`) с живыми обновлениями через store; канбан-доска (`TransitionGroup`, `defineAsyncComponent`, динамический компонент); тесты на Vitest (компонент, composable, store, router guard); production-сборка и деплой за прокси

Главная мысль лабы: Vue — это реактивность + компоненты + экосистема (Router — состояние адресной строки, Pinia — общее состояние), и каждое задание про то, где живёт состояние и кто его меняет.

---

Часть сборного репозитория лабораторных работ — [submodule-group-lab](https://github.com/meeymirita/submodule-group-lab).

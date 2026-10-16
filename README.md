# Vue Lab — Helpdesk

![Vue.js](https://raw.githubusercontent.com/meeymirita/works-lab/main/images/vue.png)

> **24.09.2026 — методичка вычитана и исправлена** (сессии 1–5). Что найдено и что поправлено — в [fixes/frontend/vue.md](https://github.com/meeymirita/lab-fixes/blob/main/frontend/vue.md) репозитория `lab-fixes`.
> **16.10.2026 — расширена с 5 до 15 сессий** (формат Caddy, 27 новых шагов, итоговое ТЗ без ответа). Новые сессии не вычитаны построчно — только прогон логики composables/store в Docker (Vitest, 27/27 тестов зелёных). Подробности — там же, в `fixes/frontend/vue.md`.

**Статус: 🟡 методичка расширена до 15 сессий (16.10.2026); сессии 1–5 проверены запуском (04.10), новые сессии 6–15 — не вычитаны построчно и не прогнаны целиком на стенде; прохождение впереди.**
**Сложность: высокая, если фронтенд — новая территория.** Нужен уверенный JavaScript (ES6+, async/await, деструктуризация); опыт с Vue или другими фреймворками не требуется, готовый мини-бэкенд (Node) дан за вас.

## О чём

Helpdesk (система тикетов) на Vue 3 с нуля — реактивность, компоненты, роутинг и общее состояние, каждое понятие на одном сквозном примере. Бэкенд (готовый мини-бэкенд на Node) дан в первой же сессии — писать его не нужно, только запустить.

## Стек

Vue 3.5 + Vite 7 + Vue Router 4 + Pinia 2+ + Vitest, бэкенд — готовый мини-бэкенд (Node). Composition API + `<script setup>` (Options API — только в теории для сравнения). С сессии 6: `vue-i18n`, DOMPurify, MSW, Playwright. Всё в Docker.

## Формат

Методичка [`vue.html`](vue.html) ([открыть на сайте](https://anitech.meeymirita.ru/works/vue.html)) — открывается в браузере.

## Что внутри (15 сессий, порядок строгий — Pinia раньше Router, потому что guard'ам роутера нужен auth-store)

- **Сессия 1** — стенд (`docker-compose`, скаффолд готового бэкенда и `create-vue`); готовый мини-бэкенд на Node (auth, tickets, comments, history, WebSocket-gateway) — дан готовым; песочница реактивности: `ref`/`reactive`/`computed`/`watch`, директивы, `v-model`, `v-for`/`key`; `useAsync` и первый запрос к API
- **Сессия 2** — разбор списка тикетов на компоненты: `StatusBadge`, `TicketCard`, `TicketList` (props/emits, слоты); `BaseModal` (слоты, Teleport, lifecycle, template refs); тосты через `provide`/`inject`; composable `useNow`/`RelativeTime`
- **Сессия 3** — Pinia: `state`/`getters`/`actions`, `storeToRefs`, auth-стор с токеном, persist-плагин; оптимистичная смена статуса тикета с откатом при ошибке
- **Сессия 4** — Vue Router: маршруты, lazy loading, `RouterLink`, guards (`requiresAuth`, роли, redirect после логина), вложенные маршруты, query-синхронизация, 404; страница тикета с вкладками, форма создания, `onBeforeRouteLeave`
- **Сессия 5** — WebSocket (`useSocket`) с живыми обновлениями через store; канбан-доска (`TransitionGroup`, `defineAsyncComponent`, динамический компонент); тесты на Vitest (компонент, composable, store, router guard); production-сборка и деплой за прокси
- **Сессия 6** — формы и валидация: `defineModel` с модификаторами и несколькими привязками, composable `useForm` (клиентские + серверные ошибки), загрузка вложения с превью и прогрессом
- **Сессия 7** — composable-паттерны: `useFetch` с отменой устаревшего запроса, `useLocalStorage`, `useClipboard`, `Suspense` + `defineAsyncComponent`, `onErrorCaptured`
- **Сессия 8** — производительность: профилирование в Vue Devtools, `v-memo`, `shallowRef`/`shallowReactive`, виртуальный список на 5000 строк
- **Сессия 9** — Pinia в большом приложении: границы между store, композиция store-в-store, аудит действий через `$subscribe`/`$onAction`
- **Сессия 10** — доступность: focus trap в модалке, `aria-label`/`aria-live` на уже кнопочном канбане (сессия 5), контраст, `prefers-reduced-motion`
- **Сессия 11** — интернационализация: `vue-i18n`, ленивая загрузка локали, множественное число (RU), даты и числа через `Intl`
- **Сессия 12** — безопасность фронтенда: санитайзинг `v-html` (DOMPurify), хранение токена и CSRF, CSP, `wss` с авторизацией на подключении
- **Сессия 13** — продвинутое тестирование: MSW (подмена сети, а не модуля), e2e на Playwright, детерминированные тесты WebSocket и guard
- **Сессия 14** — Production Hell: диагностика сломанного прод-билда (base path, build-time конфигурация, history fallback); SSR и гидратация в сравнении с Nuxt
- **Сессия 15** — итоговое ТЗ без ответа: модуль SLA и эскалации, собирающий темы всех предыдущих сессий

Главная мысль лабы: Vue — это реактивность + компоненты + экосистема (Router — состояние адресной строки, Pinia — общее состояние), и каждое задание про то, где живёт состояние и кто его меняет.

## Лицензия и авторство

Код — MIT, тексты — CC BY 4.0, обложки и иллюстрации не покрыты (см. [LICENSE](LICENSE)). Кто что сделал: [NOTICE](NOTICE).

---

Часть сборного репозитория лабораторных работ — [anitech-performance](https://github.com/meeymirita/anitech-performance).

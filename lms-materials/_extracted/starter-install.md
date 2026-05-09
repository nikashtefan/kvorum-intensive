# Установка Claude Code

_Старт · ≈ 12 мин_

![docs.claude.com/setup — официальная документация по установке](/screens/install-claude-code-docs.png)

## Способ 1. npm (для разработчиков)

Этот путь требует **Node.js 18 или выше** — это среда, в которой работают npm-пакеты. Если Node не стоит, его нужно поставить **до** Claude Code.

### Шаг 1.1. Проверить, есть ли Node

В терминале:
```bash
node --version
```

- Если ответ вида `v18.x.x` / `v20.x.x` / `v22.x.x` — Node уже стоит, переходи к шагу 1.2.
- Если `command not found` или версия ниже 18 — Node нет (или старый), сначала поставь его.

### Шаг 1.2. Поставить Node, если его нет

- **macOS:** скачай LTS-версию с [nodejs.org](https://nodejs.org) и пройди мастер установки. Или через [Homebrew](https://brew.sh): `brew install node`.
- **Windows:** скачай LTS-версию с [nodejs.org](https://nodejs.org), запусти `.msi` и пройди мастер. После установки **закрой и заново открой терминал**, иначе `node` не найдётся.
- **Linux (Ubuntu/Debian):** проще всего через [nvm](https://github.com/nvm-sh/nvm) — менеджер версий Node, потом `nvm install --lts`.

LTS (Long-Term Support) — стабильная версия с долгой поддержкой. Бери её, не «Current» — на «Current» периодически ломается совместимость пакетов.

После установки снова проверь: `node --version` должна вернуть `v18+`.

### Шаг 1.3. Поставить Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

Флаг `-g` означает «глобально» — `claude` будет доступен из любой папки. На macOS/Linux — **без `sudo`**, через `nvm` (если ставил Node через nvm — `npm -g` не требует прав). На Windows — нативно работает с Node.js for Windows.

После установки:
```bash
claude --version
```

Источник пакета: [npmjs.com/package/@anthropic-ai/claude-code](https://www.npmjs.com/package/@anthropic-ai/claude-code).

## Способ 2. Native installer (для не-разработчиков)

macOS / Linux:
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Windows (PowerShell, не CMD):
```powershell
irm https://claude.ai/install.ps1 | iex
```

Скачается официальный установщик от Anthropic, бинарник попадёт в `~/.local/bin/`, путь добавится в PATH. **Без зависимости от Node.js**, есть авто-апдейт.

Закрой и открой терминал заново. Проверь:
```bash
claude --version
```

Документация: [code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup).


## Способ 3. Claude Desktop

![claude.com/download — Claude Desktop для Mac/Windows](/screens/install-claude-desktop.png)

Графическая оболочка вокруг Claude Code с параллельными сессиями. Удобно тем, кто не хочет жить в терминале.

- Скачать: [claude.com/download](https://claude.com/download) (Mac/Windows).
- macOS: PKG → перетащи в Приложения → Системные настройки → Конфиденциальность → «Открыть всё равно».
- Windows: MSIX или EXE, требует установленный Git.
- Доступно на тарифах Pro / Max / Team.

После установки войди в тот же аккаунт, на котором оплачен Pro. В Claude Desktop легко подключаются MCP-коннекторы (Notion, Drive, Gmail) через **Settings → Connectors**.

Анонс редизайна: [MacRumors, апрель 2026](https://www.macrumors.com/2026/04/15/anthropic-rebuilds-claude-code-desktop-app/).

## Способ 4. Warp terminal

[Warp](https://www.warp.dev/) — терминал нового поколения с AI-функциями. Claude Code работает в нём как плагин с расширенной интеграцией: нативные нотификации macOS, продвинутая навигация по истории.

Установка плагина (внутри Claude Code):
```
/plugin marketplace add warpdotdev/claude-code-warp
/plugin install warp@claude-code-warp
```

Документация: [docs.warp.dev/agent-platform/cli-agents/claude-code](https://docs.warp.dev/agent-platform/cli-agents/claude-code/), [github.com/warpdotdev/claude-code-warp](https://github.com/warpdotdev/claude-code-warp).

Минус: Warp шлёт телеметрию. Для чувствительных проектов учти.

## Способ 5. VS Code extension

[Marketplace → «Claude Code»](https://marketplace.visualstudio.com/items?itemName=dliedke.ClaudeCodeExtension) от Anthropic.

Что даёт:
- Правки прямо в редакторе (видишь, что меняется, принимаешь по кнопке)
- Доступ к Claude через боковую панель, не открывая отдельный терминал
- Авторизация через тот же аккаунт

Установка: `Cmd+Shift+P` → `Extensions: Install Extensions` → искать «Claude Code».

Гайд: [sagnikbhattacharya.com/blog/claude-code-vscode](https://sagnikbhattacharya.com/blog/claude-code-vscode).

## Системные требования

| Платформа | Поддержка | Особенности |
|---|---|---|
| macOS 13+ | Полная | Самая простая установка |
| Windows 10+ | Полная (с 2025 нативная) | Для npm-пути нужен Git |
| Windows + WSL | Полная | Альтернатива нативной |
| Linux (Ubuntu 20.04+) | Полная | Простая установка |

Также: стабильный интернет, 200–500 МБ места, терминал.

## Первый запуск

```bash
mkdir test-claude
cd test-claude
claude
```

Откроется интерактивный режим, попросит авторизоваться. Откроется браузер с логином Anthropic — войди тем же аккаунтом, на котором оплачен Pro/Max. Вернись в терминал, нажми Enter.

Тест: «напиши hello.txt с текстом "привет"». Claude должен спросить разрешения, подтверди — файл появится.

## Полезные команды

| Команда | Что делает |
|---|---|
| `/help` | Список slash-команд |
| `/init` | Создать `CLAUDE.md` для проекта |
| `/clear` | Очистить контекст сессии |
| `/compact` | Сжать длинный контекст |
| `/model` | Сменить модель (Opus/Sonnet/Haiku) |
| `/cost` | Использование токенов |
| `/context` | Сколько контекста занято |
| `/agents` | Список и установка суб-агентов |
| `/plugin` | Установка плагинов и skills |
| `/exit` | Выйти |

## Plan mode

`Shift + Tab` — переключение между обычным режимом и plan mode. В plan mode Claude формулирует план, но не пишет код, пока не подтвердишь. Используй на нетривиальных задачах.

## Что НЕ делать

- Не запускать через `sudo` — создаёт проблемы с правами.
- Не ставить Claude Code в рабочей папке проекта — глобальная установка лучше.
- Не давать доступ к репо с секретами на первой неделе.
- Не пытаться использовать Cursor вместо Claude Code на интенсиве — другая модель, другой интерфейс.

## Чек-лист готовности

- [ ] Установлен Claude Code, `claude --version` показывает версию
- [ ] Авторизация прошла, в терминале готовность
- [ ] Тестовый запуск создал файл по запросу
- [ ] Знаю про Shift+Tab для plan mode
- [ ] Понял команды `/init`, `/clear`, `/help`, `/agents`, `/plugin`
- [ ] Опционально: установлен Claude Desktop, подключён один MCP

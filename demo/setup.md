# Подготовка окружения для курса

Этот документ собирает все, что нужно поставить и настроить, чтобы выполнять практические задания из уроков. Сами уроки ссылаются сюда; здесь -- полная пошаговая установка в одном месте.

## Что понадобится в сумме

| Компонент | Где используется | Обязательность |
|-----------|------------------|----------------|
| Claude Code или OpenCode | Все уроки | Обязательно (один из двух) |
| Playwright MCP | Уроки 10, 11, прототипирование (6) | Обязательно для уроков 10 и 11 |
| Kaiten MCP | Уроки 8, 10, 11 | Обязательно для уроков 8, 10 |
| `mcp-vector-search` | Урок 11 | Обязательно для урока 11 |
| `glab` (GitLab CLI) | Урок 7, частично 10 | По уроку 7 |

Если вы устанавливаете все «с нуля» -- проходите разделы по порядку.

---

## 1. Claude Code или OpenCode

Курс ориентирован на оба клиента. Разница в формате конфигов MCP отражена ниже в каждом разделе.

- **Claude Code** -- см. инструкции на [claude.com/code](https://claude.com/code).
- **OpenCode** -- см. [opencode.ai](https://opencode.ai). Используется в уроке 7 (через GitLab) и в части уроков как альтернатива.

После установки запустите клиент в корне курса (`learning_course_CC/`) и убедитесь, что он стартует без ошибок.

### Различия конфигов MCP (шпаргалка)

| Параметр | OpenCode | Claude Code |
|----------|----------|-------------|
| Файл конфига | `opencode.json` | `.mcp.json` |
| Ключ для серверов | `"mcp"` | `"mcpServers"` |
| Формат команды | `"command": ["npx", "-y", "пакет"]` | `"command": "npx"` + `"args": ["-y", "пакет"]` |
| Переменные окружения | `"environment": {...}` | `"env": {...}` |
| Файл инструкций для агента | `AGENTS.md` | `CLAUDE.md` |
| Глобальный конфиг | `~/.config/opencode/opencode.json` | `~/.claude/.mcp.json` |

Дальше каждый раздел дает два варианта конфига -- выбирайте свой.

---

## 2. Playwright MCP

Управление браузером из агента: открытие страниц, клики, скрапинг, заполнение форм.

### Установка

В Claude Code Playwright MCP ставится как плагин на уровне пользователя -- настраивать в проекте ничего не нужно. Если плагин не подключен, добавьте сервер вручную (см. ниже).

### Конфиг (если ставите вручную или нужно несколько изолированных копий)

В корне проекта создайте/дополните `.mcp.json` (Claude Code):

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest", "--isolated"]
    }
  }
}
```

Для **OpenCode** -- в `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "playwright": {
      "type": "local",
      "command": ["npx", "@playwright/mcp@latest", "--isolated"],
      "enabled": true
    }
  }
}
```

### Несколько параллельных копий

Если несколько агентов одновременно работают с Playwright, они конфликтуют по состоянию браузера. Решение -- объявить несколько именованных серверов (см. [урок 11](lesson11/plan.md), раздел Playwright):

```json
{
  "mcpServers": {
    "pw-1": { "command": "npx", "args": ["@playwright/mcp@latest", "--isolated"] },
    "pw-2": { "command": "npx", "args": ["@playwright/mcp@latest", "--isolated"] },
    "pw-3": { "command": "npx", "args": ["@playwright/mcp@latest", "--isolated"] }
  }
}
```

Флаг `--isolated` дает каждому серверу свой временный профиль браузера.

### Проверка

Попросите агента: «Открой https://example.com и сделай снапшот страницы». Должны увидеть вызов `browser_navigate` и `browser_snapshot`.

---

## 3. Kaiten MCP

Управление задачами Kaiten (карточки, чеклисты, теги, учет времени и др.). Подробный разбор сценариев -- в [уроке 8](lesson8/plan.md) и [уроке 11](lesson11/plan.md).

### Шаг 1. API-токен

1. Откройте ваш Kaiten (`https://your-company.kaiten.ru`).
2. Аватар в правом верхнем углу -> **Настройки профиля**.
3. В левом меню -- **API Key** -> **Создать токен**.
4. Скопируйте токен (показывается один раз).

### Шаг 2. ID пространства и доски

Видны прямо в URL:

- **Space ID**: `https://your-company.kaiten.ru/space/762572` -> `762572`.
- **Board ID**: `https://your-company.kaiten.ru/space/762572/boards/1727446` -> `1727446`.

### Шаг 3. Конфиг

**Claude Code** -- `.mcp.json`:

```json
{
  "mcpServers": {
    "kaiten": {
      "command": "npx",
      "args": ["-y", "kaiten-mcp"],
      "env": {
        "KAITEN_API_TOKEN": "ваш-токен",
        "KAITEN_URL": "https://your-company.kaiten.ru"
      }
    }
  }
}
```

**OpenCode** -- `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "kaiten": {
      "type": "local",
      "command": ["npx", "-y", "kaiten-mcp"],
      "enabled": true,
      "environment": {
        "KAITEN_API_TOKEN": "ваш-токен",
        "KAITEN_URL": "https://your-company.kaiten.ru"
      }
    }
  }
}
```

Перезапустите клиент после изменения конфига.

### Шаг 4. Подсказка для агента

Чтобы агент сразу понимал иерархию объектов Kaiten и типовые сценарии, добавьте в `CLAUDE.md` (Claude Code) или `AGENTS.md` (OpenCode):

```
Read ./node_modules/kaiten-mcp/LLM_GUIDE.md before working with Kaiten.
```

### Проверка

Попросите агента: «Покажи список пространств в Kaiten». Должен вызвать `kaiten_list_spaces` и вернуть список.

---

## 4. MCP для векторного поиска (`mcp-vector-search`)

Семантический поиск по локальной коллекции файлов: документация конкурентов, ресерчи, наработки. Подробные сценарии -- в [уроке 11](lesson11/plan.md). Репозиторий: [github.com/Amico1285/mcp-vector-search](https://github.com/Amico1285/mcp-vector-search). Локально установленная копия (у автора курса): `/Users/alex/Projects/personal/mcp-vector-search/` -- там лежат `README.md` (подробный гайд) и `OLLAMA_SETUP.md`.

### Требования

- Python 3.10+.
- Один из провайдеров embeddings:
  - **VoyageAI** -- рекомендуется. Лучшее качество поиска + единственный с бесплатным reranker'ом. Щедрый бесплатный лимит. Подходит для открытой документации.
  - **OpenAI** -- альтернатива, когда VoyageAI недоступен. Reranker'а нет, поэтому включают `AI_FILTER_ENABLED=true` (требует Claude CLI на `PATH`).
  - **Ollama** -- локально, без облачных вызовов. Для приватных корпусов компании.

### Установка

Установка через `pip` в виртуальное окружение (рекомендуется в README репозитория):

```bash
python3 -m venv venv
source venv/bin/activate
pip install "git+https://github.com/Amico1285/mcp-vector-search.git#egg=mcp-vector-search[voyage]"
```

Вместо `[voyage]` укажите нужного провайдера: `[openai]`, `[ollama]`.

Проверьте, что бинарь стартует:

```bash
mcp-vector-search   # должен показать баннер FastMCP; Ctrl+C для остановки
```

Если бинаря нет в `PATH` (типично, когда venv не активирован), сервер можно запускать как модуль:

```bash
python -m code_search_mcp
```

### Конфиг (Claude Code)

Самый простой путь -- добавить через CLI:

```bash
claude mcp add code-search --scope project mcp-vector-search
```

Это создаст `.mcp.json` в проекте. Дальше отредактируйте блок `env`. Базовые пресеты (взяты из README репозитория):

**Пресет 1: Документация / база знаний (markdown, прозовые тексты).**
Для большинства сценариев курса -- скрапленная документация конкурентов, ресерчи. Использует контекстуализованные embeddings `voyage-context-3` с маленькими чанками: точное попадание на длинных документах.

```json
{
  "mcpServers": {
    "code-search": {
      "command": "mcp-vector-search",
      "env": {
        "CODEBASE_PATH": "/absolute/path/to/your/folder",
        "DB_NAME": "docs_db",

        "EMBEDDING_PROVIDER": "voyage",
        "VOYAGE_API_KEY": "pa-...",
        "VOYAGE_EMBEDDING_MODEL": "voyage-context-3",
        "VOYAGE_ENABLE_CHUNKING": "true",
        "VOYAGE_MAX_CHUNK_TOKENS": "64",

        "SEMANTIC_SEARCH_N_RESULTS": "30",
        "RERANKER_ENABLED": "true",
        "RERANKER_THRESHOLD": "0.5",
        "AI_FILTER_ENABLED": "false",
        "MAX_RESULTS": "10",

        "PREVIEW_CHARS_OUTPUT": "200"
      }
    }
  }
}
```

`PREVIEW_CHARS_OUTPUT=200` отдаёт агенту первые ~200 символов каждого кандидата -- можно подтвердить релевантность без дополнительного `Read`.

**Пресет 2: Код или код + доки.**
`voyage-3-large` без чанкинга, путь к файлу важнее длинного контекста.

```json
"EMBEDDING_PROVIDER": "voyage",
"VOYAGE_API_KEY": "pa-...",
"VOYAGE_EMBEDDING_MODEL": "voyage-3-large",
"VOYAGE_OUTPUT_DIMENSION": "1024",
"VOYAGE_ENABLE_CHUNKING": "false",

"SEMANTIC_SEARCH_N_RESULTS": "20",
"RERANKER_ENABLED": "true",
"RERANKER_THRESHOLD": "0.5",
"AI_FILTER_ENABLED": "false",
"MAX_RESULTS": "10",
"PREVIEW_CHARS_OUTPUT": "0"
```

`PREVIEW_CHARS_OUTPUT=0` возвращает только пути и скоры; агент дочитывает нужные файлы через `Read`/`Grep`/`Glob`. Экономит токены на больших репозиториях.

**Пресет 3: Локально (Ollama), для приватных корпусов.**

```json
"EMBEDDING_PROVIDER": "ollama",
"OLLAMA_BASE_URL": "http://localhost:11434",
"OLLAMA_EMBEDDING_MODEL": "snowflake-arctic-embed2",

"SEMANTIC_SEARCH_N_RESULTS": "20",
"RERANKER_ENABLED": "false",
"AI_FILTER_ENABLED": "false",
"MAX_RESULTS": "10",
"PREVIEW_CHARS_OUTPUT": "100"
```

Reranker от Voyage работает только с Voyage API, поэтому здесь выключен. Подробнее по моделям Ollama -- в `OLLAMA_SETUP.md` репозитория.

Полная таблица переменных окружения (BM25, гибридный поиск, логирование, preview lines и т.д.) -- в README репозитория.

### Конфиг (OpenCode)

В `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "code-search": {
      "type": "local",
      "command": ["mcp-vector-search"],
      "enabled": true,
      "environment": {
        "CODEBASE_PATH": "/absolute/path/to/your/folder",
        "DB_NAME": "docs_db",
        "EMBEDDING_PROVIDER": "voyage",
        "VOYAGE_API_KEY": "pa-...",
        "VOYAGE_EMBEDDING_MODEL": "voyage-context-3",
        "VOYAGE_ENABLE_CHUNKING": "true",
        "VOYAGE_MAX_CHUNK_TOKENS": "64",
        "RERANKER_ENABLED": "true",
        "RERANKER_THRESHOLD": "0.5",
        "MAX_RESULTS": "10",
        "PREVIEW_CHARS_OUTPUT": "200"
      }
    }
  }
}
```

OpenCode явно в README репозитория не описан -- блок выше получен переносом полей из формата Claude Code в формат OpenCode (см. шпаргалку различий конфигов выше).

### Несколько проектов с одной установкой

Бинарь ставится один раз; разные корпусы разделяются через `DB_NAME` (имя коллекции в ChromaDB). У каждого проекта свой `.mcp.json` с уникальным `DB_NAME` и своим `CODEBASE_PATH`.

### Индексация и проверка

После перезапуска клиента (`/mcp` в Claude Code покажет статус):

1. «Проанализируй мою коллекцию файлов и создай конфигурацию поиска» -- агент проанализирует структуру, покажет, какие файлы и расширения будут проиндексированы.
2. «Запусти векторизацию базы с текущей конфигурацией» -- агент запускает индексацию через отдельный инструмент.

Для больших корпусов включите подробные логи:

```json
"LOGGING_VERBOSE": "true",
"LOGGING_FILE_ENABLED": "true"
```

Дальше -- обычный запрос на естественном языке: «Найди, как реализован Just-in-time access у CyberArk», «Покажи документацию про deployment».

### Типовые проблемы

- **`command not found: mcp-vector-search`** -- бинарь не на `PATH` Claude Code (типично для venv). В `command` укажите абсолютный путь, например `/Users/you/venv/bin/mcp-vector-search`, или вызывайте через `python -m code_search_mcp`.
- **`ModuleNotFoundError: No module named 'fastmcp'`** -- зависимости не установлены в активный Python; переустановите с нужным extra (`[voyage]`, `[openai]`, `[ollama]` или `[all]`).
- **`CODEBASE_PATH environment variable not set`** -- добавьте в блок `env` своего `.mcp.json`.
- **Поиск ничего не возвращает** -- проверьте через `get_server_info()`, индексирован ли корпус; запустите `update_db()`; убедитесь, что API-ключ провайдера верный.

---

## 5. `glab` -- GitLab CLI (для урока 7)

В уроке 7 агент работает с GitLab через `glab`. Установка -- по [официальной инструкции GitLab](https://gitlab.com/gitlab-org/cli). На macOS:

```bash
brew install glab
glab auth login
```

---

## Чек-лист перед курсом

- [ ] Claude Code или OpenCode установлен и запускается в корне `learning_course_CC/`.
- [ ] Playwright MCP подключен (`browser_navigate` отвечает).
- [ ] Kaiten MCP подключен, есть API-токен, известны Space ID и Board ID.
- [ ] `mcp-vector-search` установлен, выбран и сконфигурирован провайдер embeddings.
- [ ] `glab` установлен и авторизован (если планируете урок 7).

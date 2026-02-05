# Генерация релиз-ноутов с помощью AI

## 1. Автогенерация релиз-ноутов из Git commits / PR descriptions

### Существующие подходы

**GitHub Native API**
GitHub предоставляет встроенный API endpoint `/repos/{owner}/{repo}/releases/generate-notes`, который автоматически анализирует все изменения между двумя тегами, извлекает информацию о контрибьюторах и форматирует changelog в markdown.

**GitLab Changelog API**
GitLab также предлагает API для генерации changelog с возможностью использования шаблонов и кастомизации на основе истории коммитов.

### Ключевые инструменты

| Инструмент | Описание |
|------------|----------|
| **semantic-release** | Библиотека, интегрируемая в build-процесс, полностью автоматизирует релизы |
| **release-please** | CLI-инструмент от Google, создает PR для review перед публикацией |
| **changesets** | Markdown-файлы для описания изменений, отвязанные от deployment |
| **conventional-changelog** | Парсит историю коммитов и генерирует структурированный changelog |

### Сравнение подходов

- **semantic-release**: полная автоматизация как часть CI/CD pipeline
- **release-please**: ручной контроль через PR перед релизом, больше гибкости
- **changesets**: разделяет версионирование и deployment, подходит для monorepo

---

## 2. Conventional Commits и их связь с Changelog

### Формат Conventional Commits

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Основные типы коммитов

| Тип | Описание | Версия (SemVer) |
|-----|----------|-----------------|
| `feat` | Новая функциональность | MINOR |
| `fix` | Исправление бага | PATCH |
| `docs` | Документация | - |
| `style` | Форматирование | - |
| `refactor` | Рефакторинг | - |
| `test` | Тесты | - |
| `chore` | Прочее | - |
| `BREAKING CHANGE` | Несовместимые изменения | MAJOR |

### Как работает связь с Changelog

1. Коммиты следуют формату Conventional Commits
2. Инструменты (commitlint, commitizen) валидируют формат
3. При релизе парсеры извлекают типы коммитов
4. Автоматически определяется следующая версия по SemVer
5. Генерируется структурированный changelog с категориями

---

## 3. AI/LLM решения для генерации релиз-ноутов

### Специализированные инструменты

**ReleasesNotes.dev**
- Интеграция с GitHub/GitLab
- Автоматический fetch commit messages
- AI-генерация на основе выбранных коммитов
- 7-дневный бесплатный trial

**AI Release Notes (GitHub Marketplace)**
- GitHub App с использованием OpenAI API
- Автоматическая генерация при каждом релизе
- Интеграция в существующий workflow

**GenAIScript (Microsoft)**
- Open-source фреймворк для AI-скриптов
- Использует git diff и историю коммитов
- Интегрируется с release-it
- Настраиваемые промпты

**Changeish**
- Bash-скрипт с использованием Ollama (локальные модели)
- Работает без облачных API
- Подходит для конфиденциальных проектов

### Инструменты для генерации commit messages (связанные)

| Инструмент | LLM провайдеры | Особенности |
|------------|---------------|-------------|
| **OpenCommit** | GPT, Claude, Ollama | Генерация за 1 секунду |
| **AICommit2** | GPT, Claude, Gemini, Mistral, Ollama | Поддержка Git и Jujutsu |
| **llm-git** | Claude, OpenAI-compatible | Conventional commits, history rewrite |
| **llm-commit** | Различные | Плагин для CLI |

### n8n Workflows

- Workflow для генерации changelog из Git commits с GPT-4
- Интеграция с GitHub API
- Визуальное построение pipeline

---

## 4. Примеры агентных решений

### GitHub Agentic Workflows (GitHub Next)

Исследовательский проект от GitHub для встраивания автономных AI-агентов в GitHub Actions:

- **Natural Language Instructions**: описание поведения на естественном языке вместо скриптов
- **YAML + Markdown**: триггеры и разрешения в YAML, инструкции для AI в markdown
- **Sandboxing**: наследует модель безопасности GitHub Actions
- **Least-privilege tokens**: минимальные разрешения для безопасности

### Типичный агентный пайплайн для релиз-ноутов

```
1. Trigger: merge PR / создание тега
2. Agent собирает: commits, PR descriptions, issues
3. LLM анализирует и категоризирует изменения
4. Генерация draft релиз-ноутов
5. Human review (опционально)
6. Публикация
```

### Ascend.io Pipeline (пример из практики)

- GitHub Actions + OpenAI
- Автоматический trigger при merge PR
- Суммаризация изменений в issue с release notes
- Результат: экономия 1.5 часа на релиз в SaaS-компании

### Паттерны агентных workflow

По данным n8n и IBM, агентные workflow для релиз-ноутов включают:
- Агент классификации (определяет тип изменения)
- Агент генерации (создает текст)
- Агент review (решает публиковать или отправить на review)

---

## 5. Best Practices для написания хороших релиз-ноутов

### Структура и организация

- Единый шаблон для всех релизов
- Категории: New Features, Improvements, Bug Fixes, Breaking Changes
- Версия и дата в заголовке
- Опциональный high-level summary

### Содержание

1. **Фокус на пользе для пользователя**, а не на технических деталях
2. **1-2 предложения на пункт** - краткость
3. **Четкие migration steps** при breaking changes
4. **Known issues** при необходимости
5. **Скриншоты/видео** для UI-изменений

### Язык и тон

- Понятный язык без жаргона (если аудитория не техническая)
- Голос бренда в коммуникации
- Объяснение "что изменилось" доступным языком

### Распространение

- Легкий доступ к релиз-ноутам
- Опция подписки на уведомления
- При частых релизах - weekly digest
- Интеграция с in-app notifications

### Антипаттерны

- Слишком длинные описания
- Технический жаргон для нетехнической аудитории
- Отсутствие категоризации
- Пропуск breaking changes

---

## Ссылки на источники

### Автогенерация и инструменты
- [How to Automate Release Notes with AI - Ascend.io](https://www.ascend.io/blog/how-we-built-an-ai-powered-release-notes-pipeline)
- [Tutorial: Automate releases with GitLab](https://about.gitlab.com/blog/tutorial-automated-release-and-release-notes-with-gitlab/)
- [GitHub's AI-Powered Release Notes - Arinco](https://arinco.com.au/blog/devops-enhanced-release-automation-with-githubs-ai-powered-release-notes/)
- [AI Release Notes - GitHub Marketplace](https://github.com/marketplace/ai-github-release-notes)

### Conventional Commits и Changelog
- [Conventional Commits Specification](https://www.conventionalcommits.org/en/about/)
- [conventional-changelog on GitHub](https://github.com/conventional-changelog/conventional-changelog)
- [standard-version on GitHub](https://github.com/conventional-changelog/standard-version)
- [Semantic Versioning and Conventional Commits - negg Blog](https://negg.blog/en/semantic-versioning-and-conventional-commits/)

### AI/LLM инструменты
- [ReleasesNotes.dev](https://www.releasesnotes.dev/)
- [GenAIScript Release Notes - Microsoft](https://microsoft.github.io/genaiscript/blog/creating-release-notes-with-genai/)
- [OpenCommit on GitHub](https://github.com/di-sukharev/opencommit)
- [Changeish - DEV Community](https://dev.to/itlackey/changeish-automate-your-changelog-with-ai-45kj)
- [n8n Changelog Workflow](https://n8n.io/workflows/8137-generate-professional-changelogs-from-git-commits-with-gpt-4-and-github/)

### Сравнение инструментов
- [NPM Release Automation: Semantic Release vs Release Please vs Changesets](https://oleksiipopov.com/blog/npm-release-automation/)
- [Release-please vs semantic-release](https://www.hamzak.xyz/blog-posts/release-please-vs-semantic-release)

### Агентные решения
- [GitHub Next - Agentic Workflows](https://githubnext.com/projects/agentic-workflows/)
- [AI Agentic Workflows - n8n](https://blog.n8n.io/ai-agentic-workflows/)
- [Agentic Workflows - IBM](https://www.ibm.com/think/topics/agentic-workflows)

### Best Practices
- [How To Create Perfect Release Notes - Monday.com](https://www.monday.com/blog/rnd/release-note-template/)
- [Release Notes Best Practices - ProductPlan](https://www.productplan.com/learn/release-notes-best-practices/)
- [How to Write Release Notes - Appcues](https://www.appcues.com/blog/release-notes-examples)
- [Release Notes Best Practices - Userpilot](https://userpilot.com/blog/release-notes-best-practices/)
- [The Ultimate Guide - LaunchNotes](https://www.launchnotes.com/blog/how-to-write-great-product-release-notes-the-ultimate-guide)

---

## Выводы

1. **Conventional Commits - основа автоматизации**: стандартизированный формат коммитов позволяет автоматически генерировать changelog и определять версии по SemVer.

2. **Выбор инструмента зависит от workflow**: semantic-release для полной автоматизации, release-please для контроля через PR, changesets для monorepo.

3. **AI добавляет "человечность"**: LLM-инструменты трансформируют технические коммиты в понятные пользователям описания, экономя до 1.5 часов на релиз.

4. **Агентные решения - следующий шаг**: GitHub Agentic Workflows и подобные решения позволяют описывать поведение на естественном языке вместо написания скриптов.

5. **Best practices остаются актуальны**: независимо от инструмента, фокус на пользе для пользователя, четкая структура и краткость критически важны для эффективных релиз-ноутов.

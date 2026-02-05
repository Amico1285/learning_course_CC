# Агентные пайплайны для документации

## 1. Существующие AI/агентные решения для автоматизации документации

### Специализированные инструменты

**RepoAgent** - LLM-powered фреймворк для генерации документации на уровне репозитория. Поддерживает автоматическое создание и обновление документации при изменении кода. Интегрируется через pre-commit hooks. Поддерживает GPT-4, Llama-2 и другие модели.
- GitHub: https://github.com/OpenBMB/RepoAgent

**DocAider** - многоагентная система от UCL и Microsoft для автоматизированного создания и обновления документации. Использует Semantic Kernel и Autogen. Включает агентов для контекста кода, генерации документации и ревью.
- GitHub: https://github.com/ucl-docaider/docAider

**GitLab AI Agents** - встроенные агенты GitLab для генерации тестов и документации с учетом контекста проекта.

### Платформы для автоматизации

**AutoGPT Platform** - low-code платформа для создания автономных агентов. Поддерживает создание контента, обработку данных, исследования.
- Документация: https://docs.agpt.co/

**n8n** - гибридная платформа с 400+ интеграциями для визуального построения workflow с поддержкой кастомного кода.

## 2. Архитектура агентных систем для docs-as-code

### Agentic Document Workflows (ADW)

Архитектура ADW от LlamaIndex объединяет обработку документов, извлечение информации, структурированные выходы и агентную оркестрацию. В отличие от традиционных IDP и RAG подходов, ADW обеспечивает end-to-end автоматизацию.

Минимальная ADW система включает 4 стадии, связанные формальными контрактами данных (typed messages, например Pydantic models):
1. Парсинг документов
2. Извлечение информации
3. Обогащение из базы знаний
4. Генерация результатов

### Ключевые принципы (по Anthropic)

**Prompt Chaining** - декомпозиция сложной задачи на последовательность промптов с разделением ответственности.

**Routing** - классификация входных данных и направление к специализированным обработчикам.

**Orchestrator-Worker** - центральный агент координирует процесс, делегируя задачи специализированным субагентам, работающим параллельно.

### Docs-as-Code подход

Современные практики включают:
- Фиксацию ошибок реализации в `.memory.md`
- Документирование успешных паттернов в `.instructions.md`
- Итеративное улучшение workflow в `.prompt.md` файлах

## 3. Типы агентов для документационных workflow

### Основные роли агентов

| Агент | Функция |
|-------|---------|
| **Content Gathering Agent** | Сбор информации из различных источников |
| **Writer Agent** | Генерация текста документации |
| **Information Design Agent** | Структурирование контента в outline |
| **Review Agent** | Проверка качества и точности |
| **Translation Agent** | Перевод на другие языки |
| **Link Checker** | Проверка работоспособности ссылок |
| **Style Linter** | Проверка соответствия стилевым гайдлайнам |
| **Verification Agent** | Валидация технических утверждений |

### Паттерны взаимодействия

**Sequential Pipeline:**
```
Content Gathering -> Information Design -> Writer -> Reviewer -> Publisher
```

**Parallel with Orchestrator:**
```
Orchestrator -> [Writer | Translator | Linter] -> Aggregator -> Publisher
```

**Verification Loop:**
```
Writer -> Verification -> (pass) -> Publisher
         |
         v
        (fail) -> Writer (с обратной связью)
```

## 4. Open Source проекты

### Документационные агенты

| Проект | Описание | GitHub Stars |
|--------|----------|--------------|
| **RepoAgent** | LLM-фреймворк для документации репозиториев | OpenBMB/RepoAgent |
| **DocAider** | Многоагентная система с GitHub Actions | ucl-docaider/docAider |
| **RAGFlow** | RAG-движок с глубоким пониманием документов | - |

### Фреймворки для агентов

| Проект | Описание |
|--------|----------|
| **SuperAGI** | Dev-first фреймворк для автономных агентов |
| **Goose** | Расширяемый AI агент от Block |
| **OpenHands** | Агент для редактирования кода, выполнения команд, веб-браузинга |

### Коллекции и списки

- [e2b-dev/awesome-ai-agents](https://github.com/e2b-dev/awesome-ai-agents) - курируемый список AI агентов
- [kyrolabs/awesome-agents](https://github.com/kyrolabs/awesome-agents) - каталог агентов
- [ashishpatel26/500-AI-Agents-Projects](https://github.com/ashishpatel26/500-AI-Agents-Projects) - 500 примеров использования

## 5. Фреймворки для построения агентных систем

### LangChain / LangGraph

- Библиотека для построения LLM-приложений
- LangGraph для workflow и агентов
- Интеграция с множеством инструментов
- Документация: https://docs.langchain.com/

### CrewAI

Фреймворк для многоагентных систем, где агенты работают как команда:
- **Agents** - специализированные AI с ролью, целью и backstory
- **Tasks** - дискретные единицы работы с зависимостями
- **Crews** - группы агентов для совместной работы
- Интеграция с LangChain через LangChainTool

### AutoGPT

- Автономный агент на базе GPT-4
- Разбивает цели на подзадачи
- Поддерживает веб-браузинг и работу с файлами
- Low-code UI для построения workflow

### Claude Agent SDK (Anthropic)

- Паттерн "дайте агенту компьютер"
- Поддержка субагентов для параллелизации
- Изолированные контексты для управления памятью
- Оркестратор-воркер архитектура

### AgentWorkflow (LlamaIndex)

- Система для построения и оркестрации агентных систем
- Координация между агентами
- Поддержание состояния
- Гибкость и расширяемость

### Сравнение фреймворков (2026)

| Фреймворк | Сильные стороны | Применение |
|-----------|-----------------|------------|
| LangChain | Гибкость, экосистема | Универсальные LLM приложения |
| CrewAI | Командная работа агентов | Сложные многоэтапные задачи |
| AutoGPT | Автономность | Исследования, контент |
| Claude SDK | Надежность, субагенты | Production системы |

## 6. CI/CD интеграция

### GitHub Actions

GitHub Actions - основная платформа для запуска AI агентов благодаря глубокой интеграции с экосистемой GitHub.

**Возможности интеграции:**
- Автоматический запуск агентов при PR
- Генерация и обновление документации
- Проверка качества документации
- Линтинг и проверка ссылок

### GitHub Copilot Coding Agent

Новый агент GitHub Copilot:
- Запускается при назначении issue
- Работает в защищенном окружении на GitHub Actions
- Специализируется на задачах низкой и средней сложности
- Может улучшать документацию

### Документационный линтинг в CI/CD

Практики docs-as-code требуют автоматизации линтинга в CI:
- Ошибки документации (битые ссылки, стилевые нарушения) блокируют merge
- Документация проходит те же проверки, что и код
- AI агент может автоматически исправлять проблемы

### Инструменты

**Fern** - автоматизация качества документации:
- Встроенный линтинг
- Проверка ссылок
- AI-powered генерация контента
- Документация: https://buildwithfern.com/

**Vale** - линтер для прозы:
- Кастомные правила стиля
- Интеграция в CI/CD

### Пример workflow (DocAider)

```yaml
# Триггер на PR
on:
  pull_request:
    types: [opened]

# Агенты:
# 1. CodeContextAgent - анализ изменений кода
# 2. DocumentationGenerationAgent - генерация документации
# 3. ReviewAgent - ревью и улучшение
# 4. AgentManager - оркестрация
```

### Безопасность

Агенты в GitHub Actions наследуют привилегии через GITHUB_TOKEN и другие секреты. Необходимы:
- Минимальные необходимые права
- Аудит действий агентов
- Изоляция окружений

## Источники

### Архитектура и паттерны
- [Building Effective Agents - Anthropic](https://www.anthropic.com/research/building-effective-agents)
- [Introducing Agentic Document Workflows - LlamaIndex](https://www.llamaindex.ai/blog/introducing-agentic-document-workflows)
- [Workflows and agents - LangChain](https://docs.langchain.com/oss/python/langgraph/workflows-agents)
- [Agentic Workflows: The Ultimate Guide 2026 - Vellum](https://www.vellum.ai/blog/agentic-workflows-emerging-architectures-and-design-patterns)

### Фреймворки
- [CrewAI Documentation](https://docs.crewai.com/)
- [AutoGPT Documentation](https://docs.agpt.co/)
- [MCP vs LangChain vs CrewAI Comparison 2026](https://www.digitalapplied.com/blog/mcp-vs-langchain-vs-crewai-agent-framework-comparison)

### Open Source проекты
- [RepoAgent - OpenBMB](https://github.com/OpenBMB/RepoAgent)
- [DocAider - UCL](https://github.com/ucl-docaider/docAider)
- [Awesome AI Agents](https://github.com/e2b-dev/awesome-ai-agents)
- [500 AI Agents Projects](https://github.com/ashishpatel26/500-AI-Agents-Projects)

### CI/CD и автоматизация
- [Docs Linting in CI/CD - Netlify](https://www.netlify.com/blog/a-key-to-high-quality-documentation-docs-linting-in-ci-cd/)
- [Docs Linting Guide - Fern](https://buildwithfern.com/post/docs-linting-guide)
- [GitHub Copilot Coding Agent](https://github.blog/news-insights/product-news/github-copilot-meet-the-new-coding-agent/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)

### Многоагентные системы
- [Multi-Agent Workflows Guide - Kanerika](https://medium.com/@kanerika/multi-agent-workflows-a-practical-guide-to-design-tools-and-deployment-3b0a2c46e389)
- [Using Multiple AI Agents in Documentation - Cherryleaf](https://www.cherryleaf.com/2024/04/using-multiple-ai-agents-in-a-technical-documentation-production-workflow/)
- [Scaling Content Review with Multi-Agent Workflow - AWS](https://aws.amazon.com/blogs/machine-learning/scaling-content-review-operations-with-multi-agent-workflow/)

### Тренды 2026
- [Agentic AI Trends 2026 - EMA](https://www.ema.co/additional-blogs/addition-blogs/agentic-ai-trends-predictions-2025)
- [Agentic AI Strategy - Deloitte](https://www.deloitte.com/us/en/insights/topics/technology-management/tech-trends/2026/agentic-ai-strategy.html)
- [AI Agent Trends 2026 - Blue Prism](https://www.blueprism.com/resources/blog/future-ai-agents-trends/)

## Выводы

1. **Зрелость технологий**: Агентные системы для документации активно развиваются. Существуют готовые open source решения (RepoAgent, DocAider), но большинство организаций находятся на стадии пилотов (38%) или исследований (30%).

2. **Архитектурные паттерны**: Наиболее эффективны паттерны orchestrator-worker и sequential pipeline с формальными контрактами данных между агентами. Anthropic рекомендует начинать с простых решений и добавлять сложность только при необходимости.

3. **Специализация агентов**: Оптимальный подход - использование специализированных агентов (writer, reviewer, translator, linter) с четким разделением ответственности и координацией через оркестратор.

4. **CI/CD интеграция**: GitHub Actions становится стандартной платформой для запуска документационных агентов. Практики docs-as-code требуют автоматизированного линтинга и проверки качества.

5. **Выбор фреймворка**: Для документационных задач подходят CrewAI (командная работа), LangChain/LangGraph (гибкость), Claude Agent SDK (надежность). Выбор зависит от сложности задач и требований к интеграции.

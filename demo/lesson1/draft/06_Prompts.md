# Промпты

## Рекомендуемый курс

**Anthropic's Interactive Prompt Engineering Tutorial** - интерактивный курс от создателей Claude. 9 глав с упражнениями, от базовых техник до сложных промптов для бизнеса.

- [Google Sheets версия](https://docs.google.com/spreadsheets/d/19jzLgRruG9kjUQNKtCg1ZjdD6l6weA6qRXG5zLIAhC8/edit?usp=sharing) (рекомендуется)
- [GitHub репозиторий](https://github.com/anthropics/prompt-eng-interactive-tutorial)
- Требует установки [Claude for Sheets](https://workspace.google.com/marketplace/app/claude_for_sheets/909417792257) и API-ключа

**Содержание курса:**
1. Basic Prompt Structure
2. Being Clear and Direct
3. Assigning Roles
4. Separating Data from Instructions (XML tags)
5. Formatting Output & Speaking for Claude
6. Precognition (Thinking Step by Step)
7. Using Examples
8. Avoiding Hallucinations
9. Building Complex Prompts (Industry Use Cases)

---

## Основные техники промптинга

### Zero-shot Prompting

Задание без примеров - модель полагается только на свои знания.

**Когда использовать:** простые задачи (классификация, перевод), быстрое прототипирование.

**Пример:**
```
Классифицируй отзыв как позитивный или негативный:
"Отличный продукт, рекомендую всем!"
```

[Подробнее на Prompt Engineering Guide](https://www.promptingguide.ai/techniques/zeroshot)

---

### Few-shot Prompting

Даем модели несколько примеров желаемого поведения перед задачей.

**Когда использовать:** нестандартный формат вывода, специфическая классификация, когда zero-shot недостаточно точен.

**Пример:**
```
Определи тональность:
"Ужасный сервис" -> Негативный
"Все отлично" -> Позитивный
"Доставка пришла вовремя" -> ?
```

[Подробнее на Prompt Engineering Guide](https://www.promptingguide.ai/techniques/fewshot)

---

### Chain-of-Thought (CoT)

Просим модель рассуждать пошагово перед ответом. Значительно улучшает качество на сложных задачах.

**Когда использовать:** математика, логические задачи, многошаговое планирование.

**Пример:**
```
Реши задачу шаг за шагом:
В магазине было 50 яблок. Продали 23. Потом привезли еще 15. Сколько яблок?
```

[Оригинальная статья Wei et al., 2022](https://arxiv.org/abs/2201.11903) | [Lilian Weng's Blog](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/)

---

### Role Prompting

Назначаем модели роль или персону перед задачей.

**Когда использовать:** нужен специфический тон/стиль, экспертный взгляд, креативные задачи.

**Пример:**
```
Ты - опытный UX-исследователь. Проанализируй этот пользовательский сценарий...
```

[Anthropic Tutorial - Assigning Roles](https://github.com/anthropics/prompt-eng-interactive-tutorial)

---

### Tree of Thoughts (ToT)

Расширение CoT - модель исследует несколько путей решения параллельно, может возвращаться и выбирать лучший.

**Когда использовать:** сложные задачи с множеством решений, стратегическое планирование, головоломки.

**Результаты:** В задаче Game of 24 обычный CoT дает 4% успеха, ToT - 74%.

[Оригинальная статья Yao et al., NeurIPS 2023](https://arxiv.org/abs/2305.10601) | [Prompt Engineering Guide](https://www.promptingguide.ai/techniques/tot)

---

### ReAct (Reasoning + Acting)

Чередование рассуждений и действий. Модель думает, выполняет действие (поиск, вызов API), анализирует результат, думает снова.

**Когда использовать:** задачи с поиском информации, автономные агенты, верификация фактов.

**Пример цикла:**
```
Thought: Мне нужно найти население Токио
Action: search("население Токио 2024")
Observation: 13.96 млн человек
Thought: Теперь могу ответить на вопрос
```

[Оригинальная статья Yao et al., ICLR 2023](https://arxiv.org/abs/2210.03629) | [Google Research Blog](https://research.google/blog/react-synergizing-reasoning-and-acting-in-language-models/)

---

## Структурные фреймворки для промптов

### CO-STAR

Победитель GPT-4 Prompt Engineering Competition в Сингапуре.

| Буква | Значение | Описание |
|-------|----------|----------|
| C | Context | Контекст задачи |
| O | Objective | Цель |
| S | Style | Стиль ответа |
| T | Tone | Тон (формальный, дружелюбный) |
| A | Audience | Целевая аудитория |
| R | Response | Формат ответа |

[Подробнее о CO-STAR](https://www.parloa.com/knowledge-hub/prompt-engineering-frameworks/)

---

### RISEN

| Буква | Значение | Описание |
|-------|----------|----------|
| R | Role | Роль AI |
| I | Instructions | Инструкции |
| S | Steps | Шаги выполнения |
| E | End Goal | Конечная цель |
| N | Narrowing | Ограничения |

[Подробнее о RISEN](https://clickup.com/general-resources/playbooks/ai-prompts)

---

### Другие популярные фреймворки

| Фреймворк | Расшифровка |
|-----------|-------------|
| **RTF** | Role, Task, Format |
| **RACE** | Role, Action, Context, Execute |
| **APE** | Action, Purpose, Expectation |
| **CARE** | Context, Action, Result, Example |

[Обзор 57 фреймворков](https://juuzt.ai/knowledge-base/prompt-frameworks/)

---

## Когда применять эти техники?

Все описанные выше техники и фреймворки наиболее полезны когда:
- Промпт зашит в код (pipelines, production systems)
- Есть набор evaluations для тестирования промптов
- Нужна воспроизводимость результатов

Для **интерактивной работы с AI-агентами** (Claude Code, Cursor, и др.) применяется другой подход.

---

## Agentic Prompting: работа с AI-агентами

### Context Engineering вместо Prompt Engineering

Anthropic выделяет новую дисциплину для работы с агентами:

| Prompt Engineering | Context Engineering |
|-------------------|---------------------|
| Фокус на формулировке инструкций | Управление состоянием контекста |
| Одиночный запрос | Множественные шаги с фидбеком |
| Статичный промпт | Динамическое управление токенами |

> "Building with language models is becoming less about finding the right words and more about context engineering"
> -- [Anthropic Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

---

### Iterative Prompting: поток мыслей вместо "идеального промпта"

Вместо того чтобы тратить время на формулирование идеального промпта по фреймворку, эффективнее:

1. **Наговорить поток мыслей** с избыточностью (redundancy)
2. **Получить фидбек** от модели
3. **Уточнить** и повторить

**Исследования подтверждают:**
- Iterative refinement улучшает качество на 22-35%
- "Claude's outputs improve significantly with iteration - after 2-3 iterations it will look much better"

**Паттерн "Brain Dump + AI":**
- Голосовой ввод помогает быть "intentionally imperfect"
- Выгружаем сырые мысли без структуры
- AI синтезирует и выделяет паттерны
- Человек решает, что идет в финальную версию

[IBM: Iterative Prompting](https://www.ibm.com/think/topics/iterative-prompting) | [Thinking Out Loud with AI](https://www.tdotf.com/blog/thinking-out-loud-with-ai)

---

### Plan Mode / Act Mode

Разделение планирования и выполнения - ключевой паттерн для работы с агентами:

**Plan Mode:**
- Агент анализирует задачу в режиме "только чтение"
- Задает уточняющие вопросы
- Создает детальный план
- Работает быстрее, потребляет меньше токенов

**Act Mode:**
- Выполнение после утверждения плана
- Чистый контекст без "мусора" от исследования
- Реальные изменения

> "Plan Mode separates research from execution... Perfect for exploring codebases, planning complex changes, or reviewing code safely"

[Claude Code Plan Mode](https://claudelog.com/mechanics/plan-mode/)

---

### Отличия от классического промптинга

| Аспект | Chat Prompting | Agentic Prompting |
|--------|---------------|-------------------|
| Инструкции | "Как сделать X" | "Зачем делать X" (агент сам решит как) |
| Цель | Ответ на вопрос | Результат/outcome |
| Границы | Не обязательны | Критически важны |
| Верификация | Человек проверяет | Агент проверяет себя (тесты, скриншоты) |

**Специфичные практики:**
- Использовать `/clear` между несвязанными задачами
- Делегировать исследование субагентам
- Давать агенту способ проверить себя (тесты, ожидаемый output)

[Claude Code Best Practices](https://code.claude.com/docs/en/best-practices) | [Prompt Engineering for AI Agents](https://www.prompthub.us/blog/prompt-engineering-for-ai-agents)

---

### Meta-Prompting: AI пишет промпты

Вместо ручного написания промптов можно попросить AI сгенерировать их:

**Anthropic Prompt Generator:**
- Описываешь задачу -> Claude создает оптимальный промпт
- Решает "проблему чистого листа"
- Доступен в [Anthropic Console](https://console.anthropic.com/)

**Automatic Prompt Engineer (APE):**
- AI генерирует варианты промптов
- Тестирует их и выбирает лучший
- APE нашел промпт лучше человеческого для Chain-of-Thought

[Anthropic Prompt Generator](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/prompt-generator) | [APE на Prompt Engineering Guide](https://www.promptingguide.ai/techniques/ape)

---

### CLAUDE.md: конфигурация агента

Для постоянных инструкций агенту используется файл CLAUDE.md в корне проекта.

**Что включать:**
- Команды, которые агент не угадает сам
- Правила стиля, отличающиеся от стандартных
- Инструкции по тестированию
- Архитектурные решения проекта

**Что НЕ включать:**
- То, что агент поймет из кода
- Стандартные конвенции языка
- Информацию, которая часто меняется

> "Frontier LLMs can follow ~150-200 instructions consistently. С учетом системного промпта Claude Code (~50 инструкций), CLAUDE.md должен быть максимально лаконичным"

[Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) | [CLAUDE.md Best Practices](https://arize.com/blog/claude-md-best-practices-learned-from-optimizing-claude-code-with-prompt-learning/)

---

## Дополнительные ресурсы

### Курсы

| Курс | Описание |
|------|----------|
| [ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) | DeepLearning.AI + OpenAI. Бесплатно. |
| [Prompt Engineering for Llama 2 & 3](https://www.deeplearning.ai/short-courses/prompt-engineering-with-llama-2/) | DeepLearning.AI. Open-source модели. |
| [Prompt Engineering for Vision Models](https://www.deeplearning.ai/short-courses/prompt-engineering-for-vision-models/) | DeepLearning.AI. Работа с изображениями. |

### Документация

| Ресурс | Ссылка |
|--------|--------|
| OpenAI Prompt Engineering Guide | [platform.openai.com/docs/guides/prompt-engineering](https://platform.openai.com/docs/guides/prompt-engineering) |
| Anthropic Claude Best Practices | [docs.claude.com](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices) |
| Prompt Engineering Guide | [promptingguide.ai](https://www.promptingguide.ai/) |
| Lilian Weng's Blog | [lilianweng.github.io](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/) |


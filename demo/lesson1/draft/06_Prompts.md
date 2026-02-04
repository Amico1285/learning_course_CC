# Промпты

## Классические техники

Эти техники полезны для production pipelines, когда промпт зашит в код и нужна воспроизводимость результатов.

| Техника | Суть | Когда нужно |
|---------|------|-------------|
| **Zero-shot** | Задание без примеров | Простые задачи |
| **Few-shot** | Несколько примеров перед задачей | Нестандартный формат вывода |
| **Chain-of-Thought** | "Думай пошагово" | Логика, математика |
| **Role Prompting** | Назначение роли/персоны | Специфический тон/стиль |
| **Tree of Thoughts** | Исследование нескольких путей | Сложные задачи с ветвлением |
| **ReAct** | Чередование рассуждений и действий | Поиск информации, агенты |

[Prompt Engineering Guide](https://www.promptingguide.ai/) | [Lilian Weng's Blog](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/)

---

## Фреймворки для промптов

Полезны для production систем, где промпт фиксирован.

| Фреймворк | Компоненты |
|-----------|------------|
| **CO-STAR** | Context, Objective, Style, Tone, Audience, Response |
| **RISEN** | Role, Instructions, Steps, End goal, Narrowing |
| **RTF** | Role, Task, Format |
| **RACE** | Role, Action, Context, Execute |

[Обзор 57 фреймворков](https://juuzt.ai/knowledge-base/prompt-frameworks/)

---

## Agentic Prompting

Для интерактивной работы с AI-агентами (Claude Code, Cursor) применяется другой подход - **Context Engineering**.

> "Building with language models is becoming less about finding the right words and more about context engineering"
> -- [Anthropic Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

Для агентов важнее **что находится в контексте**, чем как сформулирован промпт.

---

### Iterative Prompting: поток мыслей вместо "идеального промпта"

Вместо формулирования промпта по фреймворку:

1. **Наговорить поток мыслей** с избыточностью (redundancy)
2. **Получить фидбек** от модели
3. **Уточнить** и повторить

**Почему это работает:**
- Iterative refinement улучшает качество на 22-35% ([IBM](https://www.ibm.com/think/topics/iterative-prompting))
- Голосовой ввод позволяет быть "intentionally imperfect"
- AI синтезирует сырые мысли в структуру
- 2-3 итерации дают лучший результат, чем один "идеальный" промпт

[Thinking Out Loud with AI](https://www.tdotf.com/blog/thinking-out-loud-with-ai)

---

### Plan Mode

Режим планирования - агент анализирует задачу без внесения изменений.

- Работает в режиме "только чтение"
- Задает уточняющие вопросы
- Создает детальный план
- Потребляет меньше токенов

Исследование "загрязняет" контекст лишней информацией. Plan Mode позволяет исследовать задачу отдельно, а потом выполнять с чистого контекста.

---

### Act Mode

Режим выполнения - агент реализует утвержденный план.

- Выполнение после утверждения плана
- Чистый контекст без "мусора" от исследования
- Реальные изменения в файлах

**Практики:**
- `/clear` между несвязанными задачами
- Делегировать исследование субагентам
- Давать агенту способ проверить себя (тесты, ожидаемый output)

[Claude Code Plan Mode](https://claudelog.com/mechanics/plan-mode/) | [Best Practices](https://code.claude.com/docs/en/best-practices)

---

### CLAUDE.md: конфигурация агента

Файл в корне проекта с постоянными инструкциями.

**Включать:** команды которые агент не угадает, нестандартные правила стиля, инструкции по тестированию.

**Не включать:** то что агент поймет из кода, стандартные конвенции, часто меняющуюся информацию.

> "Frontier LLMs follow ~150-200 instructions consistently. CLAUDE.md должен быть лаконичным."

[Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)

---

### Meta-Prompting

Вместо написания промптов вручную - попросить AI сгенерировать их.

**Anthropic Prompt Generator** в [Console](https://console.anthropic.com/): описываешь задачу -> Claude создает оптимальный промпт.

[Документация](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/prompt-generator)

---

### Голосовой ввод: ускорение feedback loop

Главное бутылочное горлышко при работе с AI - скорость ввода. Печатать медленно, формулировать "идеальный" промпт еще медленнее. Голосовой ввод снимает это ограничение: говоришь поток мыслей -> получаешь фидбек -> уточняешь. Цикл сокращается в разы.

**Приложения для Mac:**

| Приложение | Цена | Особенности |
|------------|------|-------------|
| [VoiceInk](https://apps.apple.com/us/app/voiceink-ai-dictation/id6751431158) (рекомендую, проверено) | $25 разово | Whisper, офлайн, open-source, LLM-обработка |
| [Handy](https://handy.computer/) (рекомендую, проверено) | Бесплатно, open-source | Кроссплатформенный, Whisper, офлайн |
| [Superwhisper](https://superwhisper.com/) | от $5/мес, 15 мин бесплатно | Whisper, офлайн, горячие клавиши |
| [MacWhisper](https://goodsnooze.gumroad.com/l/macwhisper) | $69 разово / бесплатная версия | Whisper, офлайн, транскрипция файлов |
| macOS Dictation | Бесплатно (встроено) | Fn Fn, облачная обработка |

**Приложения для Windows:**

| Приложение | Цена | Особенности |
|------------|------|-------------|
| [Handy](https://handy.computer/) (рекомендую, проверено) | Бесплатно, open-source | Кроссплатформенный, Whisper, офлайн |
| [WizWhisp](https://apps.microsoft.com/detail/9pgq3h6jxl4c) | Бесплатно | Whisper, офлайн, GPU-ускорение |
| [WhisperUI](https://apps.microsoft.com/detail/9n3srnm2j6xx) | Платно | Whisper, офлайн, CUDA |
| [Wispr Flow](https://wisprflow.ai/) | Подписка | Mac/Windows/iOS, AI-улучшение |

---

## Ресурсы для изучения

### Рекомендуемый курс

**Anthropic's Interactive Prompt Engineering Tutorial** - 9 глав с упражнениями.

- [Google Sheets версия](https://docs.google.com/spreadsheets/d/19jzLgRruG9kjUQNKtCg1ZjdD6l6weA6qRXG5zLIAhC8/edit?usp=sharing) (рекомендуется)
- [GitHub](https://github.com/anthropics/prompt-eng-interactive-tutorial)
- Требует [Claude for Sheets](https://workspace.google.com/marketplace/app/claude_for_sheets/909417792257)

### Документация и курсы

| Ресурс | Описание |
|--------|----------|
| [Claude Code Best Practices](https://code.claude.com/docs/en/best-practices) | Официальные рекомендации Anthropic |
| [Context Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | Anthropic Engineering blog |
| [OpenAI Prompt Guide](https://platform.openai.com/docs/guides/prompt-engineering) | Официальный гайд OpenAI |
| [DeepLearning.AI Course](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) | Бесплатный курс с OpenAI |
| [Prompt Engineering Guide](https://www.promptingguide.ai/) | Комплексный справочник |

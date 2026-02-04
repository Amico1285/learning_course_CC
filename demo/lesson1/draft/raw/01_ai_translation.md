# AI-перевод технической документации

## 1. Сравнение подходов: специализированные MT vs LLM

### Специализированные системы машинного перевода (DeepL, Google Translate)

**DeepL:**
- Выдающееся качество перевода, особенно для бизнес-документов
- Результаты требуют в 2-3 раза меньше правок, чем переводы от Google или GPT-4
- В 2024 году выпустили новую модель с улучшением точности в 1.7 раза
- Отличная работа со специализированной терминологией
- Поддержка глоссариев для консистентности

**Google Translate:**
- Самый быстрый — результаты за миллисекунды, до 20x быстрее LLM
- Хорош для быстрых переводов большого объема
- Neural Machine Translation (NMT) обеспечивает хорошее качество для популярных языковых пар

### Large Language Models (GPT-4, Claude)

**Claude 3.5:**
- В слепом исследовании Lokalise 2025 года профессиональные переводчики оценивали переводы Claude как "хорошие" чаще, чем GPT-4, DeepL или Google Translate
- На конкурсе WMT24 занял первое место в 9 из 11 языковых пар
- Отлично работает с очень длинными документами на высокой скорости и относительно низкой стоимости
- Лучше конкурентов справляется с техническим контентом, юридическими документами и академическими работами

**GPT-4:**
- Для языков с большими ресурсами (EN-ES, EN-ZH, EN-DE) показывает качество на уровне человека
- Сильные позиции в переводе санскрита и хинди

### Ключевые преимущества LLM перед традиционным MT

- Беспрецедентный контроль стиля через промпты — можно указать тон, голос бренда, жанр
- Контекстная адаптивность существенно снижает потребность в пост-редактировании
- Возможность работать с контекстом всего документа, а не отдельных предложений

### Вывод по сравнению

Нет единственного "лучшего" инструмента. Оптимальная стратегия — гибридный workflow с использованием разных инструментов для разных задач:
- DeepL Pro — для быстрого и надежного перевода документов с нюансами
- Claude — для сложных технических документов, где важна логическая связность
- Google Translate — когда критична скорость и объем

---

## 2. Локализация документации в крупных open source проектах

### Kubernetes

Kubernetes — крупнейший проект CNCF, успешно перевел документацию на 14 языков, еще 3+ в работе.

**Структура команд:**
- Минимум 2 человека в команде (нельзя апрувить собственные PR)
- Китайская команда — несколько десятков контрибьюторов
- Каждая команда имеет собственный workflow

**Технический процесс:**
- Переведенные документы хранятся в своих поддиректориях content/**/
- URL-путь соответствует английскому источнику
- Approver открывает development branch от source branch версии Kubernetes
- Контрибьюторы открывают feature branches от development branch
- Approvers мержат feature branches в development, периодически — в source

**Автоматизация:**
- Prow автоматически применяет языковые лейблы по пути файла
- OWNERS файлы в поддиректориях позволяют локализационным командам ревьюить без одобрения нефранкоязычных ревьюеров
- Slack-каналы для каждой локализации + общий канал SIG Docs Localizations

**Гибкость workflow:**
- Некоторые команды переводят весь контент вручную
- Другие используют редакторы с плагинами для перевода и проверяют машинный вывод
- SIG Docs фокусируется на стандартах вывода, оставляя командам свободу в выборе процесса

### React

- Перевод выполняется на language-specific форках react.dev
- Работа включает прямой перевод Markdown-файлов и создание PR
- Децентрализованная модель — разные языковые сообщества поддерживают свои форки

### Инструменты для open source локализации

- **Tolgee** — open-source платформа с поддержкой React, Angular, Vue, плагин для Figma
- **i18next** — интеграции для React, Angular, Vue.js и других фреймворков
- **Transifex** — бесплатный план для open-source проектов
- **locize** — поддержка open-source философии

---

## 3. Post-editing workflow с AI (MTPE)

### Что такое MTPE

Machine Translation Post-Editing (MTPE) — процесс улучшения машинно-переведенного текста для достижения точности, естественности и соответствия целевой аудитории. Комбинирует скорость MT с экспертизой человека.

### Типы пост-редактирования

**Light post-editing:**
- Фокус на исправлении ошибок, мешающих пониманию
- Грамматические ошибки и очевидные неточности перевода
- Высокая производительность

**Full post-editing:**
- Цель — качество на уровне человеческого перевода
- Комплексная ревизия: стиль, тон, культурная уместность
- Больше времени, но выше качество

### Лучшие практики для технической документации

1. **Качество исходного текста**
   - Качество источника напрямую влияет на качество MT
   - Ясный, хорошо структурированный, однозначный текст снижает ошибки и усилия на пост-редактирование

2. **Обучение редакторов**
   - Инвестиции в обучение распознаванию паттернов MT
   - Исправление тонких лингвистических ошибок
   - Поддержание консистентности с требованиями проекта

3. **Справочные материалы**
   - Style guide и глоссарии всегда под рукой
   - Ключ к консистентности и соответствию бренду

4. **Баланс в редактировании**
   - Избегать over-editing — предпочтительных или стилистических правок, которые не необходимы
   - Если синоним работает, структура корректна и смысл понятен — оставить как есть

5. **Выбор инструментов**
   - Neural Machine Translation (NMT) — лучший выбор для базового перевода
   - Современные инструменты имеют встроенные QA-функции, которые мгновенно помечают ошибки

---

## 4. Специфика перевода RU-EN для техдокументации

### Лингвистические различия

- Русская падежная система vs фиксированный синтаксис английского
- Отсутствие артиклей в русском — необходимо добавлять a/an/the
- Гибкий порядок слов в русском vs строгий в английском
- Кириллица — дополнительная сложность при работе со скриптами

### Терминологическая специфика

- Юридические, медицинские, технические документы требуют специализированных знаний терминологии на обоих языках
- Технические документы полны терминов без прямых эквивалентов
- Ошибки могут привести к серьезным недоразумениям или юридическим проблемам

### Консистентность и точность

- Поддержание консистентности в рамках документа и между документами проекта критически важно
- Даже небольшая ошибка или неточный перевод может иметь серьезные последствия в инженерии или медицине

### Работа с форматами

- Технические переводчики работают с разными форматами файлов (AutoCAD, интерфейсы ПО)
- Необходимо владеть инструментами для сохранения целостности файлов при переводе

### Профессиональные решения

- Для сложной терминологии — коллаборация с предметными экспертами
- CAT-инструменты (Computer-Assisted Translation) для консистентности, управления терминологией, ускорения процесса

---

## 5. Лучшие практики и инструменты

### Ключевые принципы

1. **Нет единственного "лучшего" инструмента** — выбор зависит от типа контента
2. **Тестирование на реальных примерах** — маркетинговые тексты, техдокументация, коммуникации с клиентами имеют разные требования
3. **Human review обязателен для критического контента** — всегда включать специалистов-переводчиков и независимых ревьюеров

### Критические функции для техдокументации

- **Глоссарии и терминология** — must-have для индустриальной специфики, обеспечивают консистентность
- **Quality Assurance** — встроенные QA-функции для мгновенной пометки ошибок
- **Сохранение форматирования** — особенно для PDF, чтобы избежать ручного переформатирования

### Рекомендуемые инструменты по задачам

| Задача | Рекомендуемый инструмент |
|--------|-------------------------|
| Быстрый перевод документов | DeepL Pro |
| Сложный технический контент | Claude 3.5 |
| Большие объемы, скорость | Google Translate |
| Управление локализацией | Crowdin, Lokalise, Phrase |
| Open-source проекты | Tolgee, Transifex |

### Тренды 2024-2025

- LLM превосходят MT в точности перевода
- Machine-assisted translation используется в 70% языковых workflows
- Claude 3.5 — #1 в результатах по всем языкам в исследованиях
- Гибридные подходы становятся стандартом

---

## Источники

### Сравнение MT и LLM
- [Best LLMs for Translation in 2025: GPT-4 vs Claude, Gemini](https://www.getblend.com/blog/which-llm-is-best-for-translation/)
- [The Definitive Guide to AI Translation Tools](https://medium.com/@ai2ai/the-definitive-guide-to-ai-translation-tools-a-thorough-comparison-of-deepl-gpt-4-and-claude-776bbcfbd503)
- [DeepL's next-gen LLM outperforms ChatGPT-4, Google, and Microsoft](https://www.deepl.com/en/blog/next-gen-language-model)
- [DeepL vs LLMs for Translation](https://www.vincentschmalbach.com/deepl-vs-llms-for-translation/)
- [The best LLM for translation - Contentful](https://www.contentful.com/blog/best-llm-translation/)
- [Best LLMs for Translation - Crowdin Blog](https://crowdin.com/blog/best-llms-for-translation)

### Локализация open source
- [Kubernetes Community: A Guide to Open Source Localization](https://thenewstack.io/kubernetes-community-a-guide-to-open-source-localization/)
- [Localizing Kubernetes documentation](https://kubernetes.io/docs/contribute/localization/)
- [How You Can Help Localize Kubernetes Docs](https://kubernetes.io/blog/2019/04/26/how-you-can-help-localize-kubernetes-docs/)
- [Spotlight on SIG Docs](https://kubernetes.io/blog/2022/08/02/sig-docs-spotlight-2022/)
- [React Translations](https://react.dev/community/translations)
- [Tolgee](https://tolgee.io/)

### MTPE workflow
- [MTPE - Lokalise](https://lokalise.com/blog/mtpe/)
- [Machine Translation Post-Editing - Crowdin Blog](https://crowdin.com/blog/mt-post-editing)
- [Best Practices for MTPE - Phrase](https://phrase.com/blog/posts/machine-translation-post-editing-best-practices/)
- [MTPE Best Practice Guide - GAI](https://www.gaitranslate.ai/machine-translation-post-editing-best-practice-guide/)
- [10 Best Practices in MT and AI Post-Editing](https://www.translastars.com/blog/best-practices-mt-ai-postediting)

### RU-EN специфика
- [Common Challenges in Russian-English Translation](https://www.polilingua.com/blog/post/russian-english-translation-services-challenges.htm)
- [English to Russian Technical Translation - LinkedIn](https://www.linkedin.com/pulse/english-russian-technical-translation)
- [Technical Russian Translation - Talk Russian](https://www.talkrussian.com/technical-russian-translation)
- [Russian Technical Translation Services](https://www.russian-translation-pros.com/russian-translation-technical.html)

### Инструменты и лучшие практики
- [7 of the best AI translation tools for enterprise localization 2025](https://xtm.cloud/blog/ai-translation-tools/)
- [10 Best AI Translation Tools 2025](https://www.bluente.com/blog/best-ai-translation-tools)
- [Localization trends report 2025 - Lokalise](https://lokalise.com/library/data-reports/localization-trends-2025/)
- [Embracing AI in Localization: A 2025-2028 Roadmap](https://medium.com/@hastur/embracing-ai-in-localization-a-2025-2028-roadmap-a5e9c4cd67b0)

---

## Краткие выводы

1. **Гибридный подход — оптимален.** Нет единственного лучшего инструмента; DeepL для скорости и консистентности, Claude для сложного контента, специализированные платформы для workflow.

2. **LLM превосходят традиционный MT по качеству**, особенно Claude 3.5, но DeepL выигрывает по скорости редактирования (в 2-3 раза меньше правок).

3. **MTPE — стандарт индустрии.** Качество источника критично, обучение редакторов необходимо, over-editing — главная ошибка.

4. **Open source проекты** используют децентрализованные модели с гибкостью workflow — от ручного перевода до проверки машинного вывода.

5. **RU-EN перевод** требует особого внимания к артиклям, порядку слов и терминологии; коллаборация с экспертами снижает риск ошибок.

6. **Human review обязателен** для критического контента, независимо от качества AI-перевода.

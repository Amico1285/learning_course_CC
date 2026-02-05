# Фидбэк и качество документации

## 1. Измерение понятности документации: метрики и подходы

### Основные метрики качества

**Количественные метрики:**
- **Task Completion Rate (TCR)** - процент успешно выполненных задач с использованием документации. Формула: количество успешных завершений / общее количество попыток
- **Time-to-Success** - время, необходимое пользователю для выполнения задачи с помощью документации
- **Self-Service Success Rate** - доля проблем, решенных пользователями через документацию без обращения в поддержку

**Качественные метрики:**
- **Customer Satisfaction (CSAT)** - удовлетворенность пользователей конкретной страницей или разделом документации (обычно хороший показатель: 75-85%)
- **Net Promoter Score (NPS)** - готовность рекомендовать документацию (долгосрочная лояльность)
- **Readability scores** - оценка читаемости текста

### Методология Goal-Question-Metric (GQM)

Наиболее распространенный подход к оценке качества документации:
1. Определение целей качества
2. Формулировка вопросов для оценки достижения целей
3. Выбор метрик для ответа на вопросы

### Чеклист качества API-документации

Комплексный чеклист может включать более 70 аспектов:
- Accuracy (точность)
- Clarity (ясность)
- Completeness (полнота)
- Relevance (релевантность)

**Источники:**
- [I'd Rather Be Writing - Measuring Documentation Quality](https://idratherbewriting.com/learnapidoc/docapis_measuring_impact.html)
- [Archbee - Technical Writing Metrics](https://www.archbee.com/blog/technical-writing-metrics)
- [BetterDocs - Technical Documentation KPIs 2025](https://betterdocs.co/top-technical-documentation-kpis-to-track/)
- [MeasuringU - Task Completion Rate](https://measuringu.com/task-completion/)

---

## 2. Инструменты для сбора фидбэка

### Встроенные системы фидбэка в платформах документации

**GitBook:**
- Встроенная панель аналитики с метриками трафика, кликов по ссылкам, запросов к AI
- Интеграция с Google Analytics, Fathom, HotJar
- Экспорт данных в CSV

**Mintlify:**
- Аналитика поисковых запросов
- Отслеживание того, что ищут разработчики и где испытывают трудности
- Детальные метрики запросов и диалогов по дням

**ReadMe:**
- Аналитика API-вызовов
- Персонализация для разработчиков
- Интерактивные API-функции

### Универсальные инструменты для фидбэка

**AI-powered инструменты (2025):**
- BuildBetter.ai - автоматическая категоризация фидбэка
- Zonka Feedback - многоязычная поддержка, детальная аналитика
- Pendo - Software Experience Management без кода
- UserVoice - централизованный сбор и приоритизация идей
- Mopinion - сбор фидбэка с сайтов, приложений, email в реальном времени

**Ключевые возможности современных инструментов:**
- Автоматический сбор данных
- Аналитика настроений (sentiment analysis)
- Кросс-платформенные интеграции
- Voice of Customer (VOC) инсайты

**Источники:**
- [GitBook - Documentation Analytics Guide](https://gitbook.com/docs/guides/docs-analytics/documentation-analytics)
- [Pendo - User Feedback Tools 2026](https://www.pendo.io/pendo-blog/the-top-10-user-feedback-tools-in-2025/)
- [FeatureBase - Customer Feedback Tools 2025](https://www.featurebase.app/blog/customer-feedback-tools)

---

## 3. A/B тестирование документации

### Текущее состояние практики

A/B тестирование документации - **менее распространенная практика** по сравнению с маркетинговыми страницами. Основное применение A/B тестирования в контексте документации:

**Где применяется:**
- Тестирование layouts и навигации
- Тестирование формулировок заголовков
- Тестирование порядка разделов
- Тестирование размещения code snippets

### Методология документирования A/B тестов

Рекомендуемая структура документации теста:
1. **Введение** - гипотеза и цель теста
2. **Experimental Design** - аудитория, размер выборки, уровень значимости
3. **Results** - фактические данные без интерпретации
4. **Conclusions** - выводы и рекомендации
5. **Learnings** - уроки для будущих тестов

### Примеры успешных A/B тестов (из смежных областей)

- Zalora: +12.3% checkout rate от унификации CTA
- Intertop: +54.68% conversion rate от редизайна
- Bannersnack: +25% sign-ups от увеличения CTA кнопки
- Sony: +21.3% adds to cart от персонализации CTA

**Источники:**
- [VWO - A/B Testing Examples 2026](https://vwo.com/blog/ab-testing-examples/)
- [A|B Growth Marketing - How to Document A/B Tests](https://www.abgrowthmarketing.com/blog/2019/10/1/how-to-document-ab-tests)
- [Contentful - A/B Testing Best Practices](https://www.contentful.com/blog/ab-testing-best-practices/)

---

## 4. Readability Scores для технической документации

### Основные формулы

**Flesch-Kincaid Grade Level:**
- Рассчитывается на основе соотношения слов к предложениям и слогов к словам
- Результат = уровень образования, необходимый для понимания текста
- Первоначально использовался армией США для оценки технических руководств (с 1978)

**Flesch Reading Ease:**
- Шкала от 0 до 100
- Чем выше балл, тем легче читать

### Применимость к техдокументации

| Тип контента | Рекомендуемый Flesch Score |
|--------------|---------------------------|
| Маркетинговые тексты | 60-80 |
| Техническая документация | 30-50 |
| Академические работы | 20-40 |

**Ограничения для техдокументации:**
- Формулы не учитывают специфическую терминологию
- Техническая документация inherently имеет низкие scores из-за сложности
- Лучше использовать в комбинации с другими метриками

### Инструменты для проверки

- Microsoft Word (встроенная проверка)
- Readable.com
- ClickHelp (для технических документов)
- Hemingway Editor
- Grammarly

**Источники:**
- [ClickHelp - Flesch-Kincaid for Technical Documentation](https://clickhelp.com/clickhelp-technical-writing-blog/improve-the-readability-of-your-technical-documentation-with-flesch/)
- [Wikipedia - Flesch-Kincaid Readability Tests](https://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_tests)
- [Readable - Flesch Reading Ease](https://readable.com/readability/flesch-reading-ease-flesch-kincaid-grade-level/)

---

## 5. Analytics для документации

### Ключевые метрики для отслеживания

**Engagement метрики:**
- Page views / unique visitors
- Dwell time (время на странице)
- Bounce rate
- Pages per session
- Scroll depth

**Search метрики:**
- Поисковые запросы без результатов
- Популярные поисковые запросы
- Click-through rate по результатам поиска

**Feedback метрики:**
- Thumbs up/down рейтинги
- Количество комментариев
- Запросы в поддержку по теме документации

**API-специфичные метрики:**
- OpenAPI usage
- Количество вызовов API из документации
- Копирование code snippets

### Рекомендуемые инструменты

| Инструмент | Специализация | Особенности |
|------------|---------------|-------------|
| Google Analytics | Общая аналитика | Бесплатный, мощный, но сложный |
| Plausible | Privacy-focused | Простой, GDPR-compliant |
| GitBook Analytics | Документация | Встроенная аналитика, экспорт CSV |
| HotJar | Поведение | Heatmaps, session recordings |
| PostHog | Product analytics | Open-source, self-hosted опция |

### Рекомендации по настройке

1. Создать dashboard для каждого use case до или сразу после запуска
2. Группировать данные по разным атрибутам (тип пользователя, раздел, сложность)
3. Отслеживать динамику по временным периодам
4. Связывать метрики документации с бизнес-показателями (снижение тикетов в поддержку)

**Источники:**
- [GitBook - Documentation Analytics](https://gitbook.com/docs/guides/docs-analytics/documentation-analytics)
- [Contentsquare - Web Analytics Metrics 2026](https://contentsquare.com/guides/web-analytics/metrics/)
- [Infrasity - Best Documentation Tools for Developers 2025](https://www.infrasity.com/blog/best-documentation-tools-for-developers)

---

## 6. Практики крупных компаний

### Stripe

**Подход к фидбэку:**
- Виджет фидбэка на каждой странице документации
- Двухуровневая система: сначала выбор из предустановленных вариантов, затем опциональный текстовый комментарий
- Психологически облегченный процесс (опциональные поля)

**Особенности документации:**
- Знаменитый трехколоночный layout
- Навигация + контент + live code snippets
- Интерактивное выполнение кода прямо в документации

### Microsoft Learn

**Система фидбэка:**
- Thumbs up / thumbs down на каждой странице
- После рейтинга - выбор причины (одна или несколько)
- Опциональный комментарий до 999 символов
- Поддержка локализации с отдельной опцией оценки качества перевода

**Маршрутизация фидбэка:**
- Автоматическая маршрутизация к support, product или content командам
- Фидбэк оценивается content writers, не product teams
- Инструменты автоматического перевода для глобальных команд

### Google

**Практики:**
- Thumbs up/down виджеты в Google Cloud документации
- Встроенные feedback buttons в Vertex AI
- Интеграция с Google Analytics для tracking

### Общие паттерны

1. **Минимизация friction** - простые виджеты с минимумом обязательных полей
2. **Многоуровневый фидбэк** - от простого рейтинга к детальным комментариям
3. **Анонимность** - возможность оставить фидбэк без регистрации
4. **Локализация** - поддержка фидбэка на разных языках
5. **Интеграция с workflow** - автоматическая маршрутизация в нужные команды

**Источники:**
- [Feelback - Case Study: Stripe Documentation Feedback System](https://www.feelback.dev/blog/case-study-stripe-documentation/)
- [Microsoft Learn - New Feedback System](https://learn.microsoft.com/en-us/archive/teamblog/a-new-feedback-system-is-coming-to-docs)
- [Microsoft Learn - Provide Feedback](https://learn.microsoft.com/en-us/contribute/content/provide-feedback)
- [Google Cloud - Configure Widget Feedback](https://cloud.google.com/generative-ai-app-builder/docs/configure-feedback)

---

## Выводы

### Ключевые рекомендации

1. **Комбинируйте количественные и качественные метрики** - TCR и time-to-success дают объективную картину, CSAT и NPS - субъективную оценку удовлетворенности

2. **Начните с простого фидбэка** - thumbs up/down с опциональными комментариями обеспечивает высокий response rate при минимальном friction

3. **Readability scores - полезный, но не единственный индикатор** - для техдокументации нормальны более низкие показатели; важнее отслеживать динамику, чем абсолютные значения

4. **A/B тестирование документации возможно, но требует адаптации** - фокус на navigation, layout, формулировках заголовков, а не на контенте

5. **Инвестируйте в аналитику** - платформы вроде GitBook, Mintlify, ReadMe предоставляют встроенную аналитику; для глубокого анализа добавьте HotJar или PostHog

6. **Учитесь у лидеров** - Stripe, Microsoft, Google демонстрируют лучшие практики простого, многоуровневого, анонимного сбора фидбэка

### Минимальный набор метрик для старта

- Page views и time on page
- Thumbs up/down рейтинг
- Search queries без результатов
- Support tickets, связанные с документацией

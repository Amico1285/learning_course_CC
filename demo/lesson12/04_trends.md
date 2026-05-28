# Тренды

### Разрыв растет

![The rich get richer](images/rich-get-richer.png)

*Ранние adopters наращивают преимущество, отстающие отстают еще больше. Прогноз: 10x разрыв к 2030 ([Stanford SWEPRI](https://youtu.be/tbDDYKRFjhk?si=gI1RGEbaqPx10u70))*

![Uniform access doesn't guarantee uniform usage](images/uniform-access.png)

*Одинаковый доступ к AI-инструментам не гарантирует одинаковое использование. Два подразделения одной компании -- радикально разный уровень adoption ([Stanford SWEPRI](https://youtu.be/tbDDYKRFjhk?si=gI1RGEbaqPx10u70))*

### Стоимость токенов

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'xyChart': {'plotColorPalette': '#2E86AB', 'xAxisLabelColor': '#888888', 'yAxisLabelColor': '#888888', 'xAxisTitleColor': '#888888', 'yAxisTitleColor': '#888888', 'xAxisTickColor': '#CCCCCC', 'yAxisTickColor': '#CCCCCC', 'xAxisLineColor': '#CCCCCC', 'yAxisLineColor': '#CCCCCC'}}}}%%
xychart-beta
    title "Token Cost Reduction - OpenAI API (per 1M input tokens)"
    x-axis ["Mar 2023", "Nov 2023", "May 2024", "Jul 2024", "Aug 2025"]
    y-axis "Price ($)" 0 --> 35
    line [30, 10, 5, 0.15, 0.05]
```

**Эволюция моделей:** GPT-4 ($30) → GPT-4 Turbo ($10) → GPT-4o ($5) → GPT-4o Mini ($0.15) → GPT-5 Nano ($0.05)

*Снижение стоимости: 99.8% (в 600 раз дешевле) с марта 2023 по август 2025*

### Скорость прогресса AI

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'xyChart': {'plotColorPalette': '#FF6B35', 'xAxisLabelColor': '#888888', 'yAxisLabelColor': '#888888', 'xAxisTitleColor': '#888888', 'yAxisTitleColor': '#888888', 'xAxisTickColor': '#CCCCCC', 'yAxisTickColor': '#CCCCCC', 'xAxisLineColor': '#CCCCCC', 'yAxisLineColor': '#CCCCCC'}}}}%%
xychart-beta
    title "METR Time Horizon - Autonomous Task Complexity (minutes)"
    x-axis ["GPT-4", "O1", "Claude 3.5", "Claude 3.7", "O3", "Opus 4.5"]
    y-axis "Minutes" 0 --> 300
    line [5, 22, 30, 56, 94, 289]
```

**Что измеряет:** длительность задач (в минутах работы человека), которые AI может выполнить автономно с 50% надежностью

*Рост 58x за 2 года. Удвоение каждые 4-7 месяцев ([METR Research](https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/))*

> Если завтра выйдет модель с показателем в 2 раза выше -- насколько наш бизнес от этого выиграет? Как быстро мы получим бенефиты? Или их получат наши конкуренты?

---

# От чата к харнесу

### Эволюция подходов

**2023** -- Prompt Engineering: как правильно задать вопрос

**2024** -- Context Engineering: какие данные дать модели

**2025** -- Harness Engineering: как встроить AI в процессы бизнеса

### Метафора: гоночная машина

### Когда мы используем чат

![Chat without harness](images/IMG_24E47512-413E-4113-B3CD-99E7B0511097.JPEG)

### Когда у нас есть AI Business Harness

![AI Business Harness](images/IMG_0AB24388-663B-4025-A516-E690853DFDEB.JPEG)

### Business Harness Engineering

Бизнес разбит на процессы. Для каждого процесса:
- какова **цена ошибки** AI?
- какова **стоимость внедрения** AI?

### Пример: Telegram-канал маркетинга

| | AI делает | Человек делает |
|---|-----------|----------------|
| **Что** | Ресерч рынка, сбор ключевых пунктов, драфт текста, создание задачи на ревью | Ревью драфта, финальный текст, решение о публикации |
| **Цена ошибки** | Низкая -- драфт никто не видит | Высокая -- плохой пост роняет доверие канала |

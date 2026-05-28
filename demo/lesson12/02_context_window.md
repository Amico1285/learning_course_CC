# Контекстное окно

## Что такое контекстное окно?

Контекстное окно - это "рабочая память" модели. Все, что модель знает о вашей задаче, должно поместиться в это окно. Это отличается от данных, на которых модель обучалась.

## Как растет контекст

<div align="left">

### Ход 1

```mermaid
block
    columns 1
    block:frame1
        columns 12
        sys["System"] i1["In"] o1["Out"] space space space space space space space space res["Reserve"]
    end
    style sys fill:#d0d0d0,stroke:#999
    style i1 fill:#a8d4f0,stroke:#6ba3c9
    style o1 fill:#f0c54d,stroke:#c9a23d
    style res fill:#e8e8e8,stroke:#999
    style frame1 fill:#f8f9fa,stroke:#666
```

### Ход 2

```mermaid
block
    columns 1
    block:frame2
        columns 12
        sys["System"] i1["In"] o1["Out"] i2["In"] o2["Out"] space space space space space space res["Reserve"]
    end
    style sys fill:#d0d0d0,stroke:#999
    style i1 fill:#a8d4f0,stroke:#6ba3c9
    style o1 fill:#f0c54d,stroke:#c9a23d
    style i2 fill:#a8d4f0,stroke:#6ba3c9
    style o2 fill:#f0c54d,stroke:#c9a23d
    style res fill:#e8e8e8,stroke:#999
    style frame2 fill:#f8f9fa,stroke:#666
```

### Ход 3

```mermaid
block
    columns 1
    block:frame3
        columns 12
        sys["System"] i1["In"] o1["Out"] i2["In"] o2["Out"] i3["In"] o3["Out"] space space space space res["Reserve"]
    end
    style sys fill:#d0d0d0,stroke:#999
    style i1 fill:#a8d4f0,stroke:#6ba3c9
    style o1 fill:#f0c54d,stroke:#c9a23d
    style i2 fill:#a8d4f0,stroke:#6ba3c9
    style o2 fill:#f0c54d,stroke:#c9a23d
    style i3 fill:#a8d4f0,stroke:#6ba3c9
    style o3 fill:#f0c54d,stroke:#c9a23d
    style res fill:#e8e8e8,stroke:#999
    style frame3 fill:#f8f9fa,stroke:#666
```

**200K токенов** - контекстное окно для моделей Claude 4.5

</div>

**Ключевые моменты:**

- **Накопление токенов:** С каждым ходом беседы сообщения пользователя и ответы ассистента накапливаются в контекстном окне. Предыдущие ходы сохраняются полностью.
- **Линейный рост:** Использование контекста растет линейно с каждым ходом.

## Деградация качества при росте контекста

NoLiMa Benchmark Results (arXiv:2502.05167, March 2025)

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'xyChart': {'plotColorPalette': '#1f77b4, #ff7f0e, #9467bd, #8c564b, #2ca02c, #d62728, #7f7f7f', 'xAxisLabelColor': '#666666', 'yAxisLabelColor': '#666666', 'xAxisLineColor': '#CCCCCC', 'yAxisLineColor': '#CCCCCC'}}}}%%
xychart-beta
    title "Model Performance vs Context Length"
    x-axis "Context Length (tokens)" [1K, 2K, 4K, 8K, 16K, 32K]
    y-axis "Performance Score" 0 --> 100
    line "GPT-4o" [100, 95, 90, 82, 78, 65]
    line "GPT-4o mini" [88, 85, 78, 70, 58, 45]
    line "Llama 3.3 70B" [98, 92, 85, 72, 50, 30]
    line "Llama 3.1 405B" [92, 88, 75, 62, 47, 28]
    line "Gemini 1.5 Pro" [85, 82, 75, 68, 42, 27]
    line "Claude 3.5 Sonnet" [85, 80, 72, 58, 40, 28]
    line "Gemini 1.5 Flash" [70, 68, 60, 52, 32, 15]
```

<div align="left">

| Model | Context Window | 1K | 32K | Падение |
|-------|----------------|-----|------|---------|
| ![](images/dot-blue.svg) GPT-4o | 128K | 100% | 65% | -35% |
| ![](images/dot-orange.svg) GPT-4o mini | 128K | 88% | 45% | -43% |
| ![](images/dot-purple.svg) Llama 3.3 70B | 128K | 98% | 30% | -68% |
| ![](images/dot-brown.svg) Llama 3.1 405B | 128K | 92% | 28% | -64% |
| ![](images/dot-green.svg) Gemini 1.5 Pro | 2M | 85% | 27% | -58% |
| ![](images/dot-red.svg) Claude 3.5 Sonnet | 200K | 85% | 28% | -57% |
| ![](images/dot-gray.svg) Gemini 1.5 Flash | 1M | 70% | 15% | -55% |

</div>

**Вывод:** Даже на 32K токенов (16% от заявленных 200K) производительность падает на 50-70%.

<div style="background-color: #f0f7ff; padding: 20px; border-radius: 8px; border-left: 4px solid #1f77b4;">

## Практические рекомендации

### 1. Давайте только необходимый контекст

Не загружайте "всю документацию на всякий случай". Чем меньше контекста - тем лучше модель работает. Давайте только то, что нужно для конкретной задачи.

### 2. Новая задача = новая беседа

После завершения задачи не продолжайте в той же беседе. Накопленный контекст (ваши вопросы, ответы модели, результаты поиска) снижает качество следующей задачи.

### 3. Используйте форки бесед

Если несколько задач требуют одинакового начального контекста (например, изучение документации проекта):

1. Создайте базовую беседу где модель изучила документацию
2. Для каждой новой задачи делайте форк от этой точки
3. Каждая задача выполняется в "чистом" контексте

</div>



# Источники: Снижение стоимости токенов

## Исследование проведено: 3 февраля 2025

## Основные источники

### 1. OpenAI API Pricing Documentation
- **Что:** Официальная документация по ценам OpenAI
- **Данные:**
  
| Model | Release Date | Input (per 1M tokens) | Output (per 1M tokens) |
|-------|-------------|----------------------|----------------------|
| GPT-4 | March 2023 | $30.00 | $60.00 |
| GPT-4 Turbo | Nov 2023 | $10.00 | $30.00 |
| GPT-4o | May 2024 | $2.50 | $10.00 |
| GPT-4o Mini | July 2024 | $0.15 | $0.60 |
| GPT-4.1 Nano | April 2025 | $0.10 | $0.40 |
| GPT-5 Nano | Current | $0.05 | $0.40 |

- **Общее снижение:** 99.8% (в 600 раз дешевле) с GPT-4 по GPT-5 Nano
- **URL:** https://openai.com/pricing

### 2. Anthropic Claude Pricing
- **Что:** Цены на API Anthropic Claude
- **Данные:**
  - Claude 3 Opus: $15.00 / $75.00 per 1M
  - Claude 3.5 Sonnet (June 2024): $3.00 / $15.00 per 1M
  - Claude Sonnet 4.5: $3.00 / $15.00 per 1M
  - Claude Haiku 4.5: $1.00 / $5.00 per 1M
- **URL:** https://www.anthropic.com/pricing

### 3. Epoch AI Research
- **Что:** Исследования Epoch AI по трендам AI
- **Данные:**
  - Снижение цен на inference: ~40x для fixed performance
  - FLOP/s per dollar: улучшение 2.34x per year
  - Algorithmic progress: снижение compute requirements на ~10x per year
  - Training compute: рост 4-5x per year (компенсируется эффективностью)
- **URL:** https://epoch.ai/

### 4. Драйверы снижения стоимости

#### Model Optimization
- Distillation (дистилляция моделей)
- Quantization (квантизация)

#### Hardware Advances
- NVIDIA GPU improvements (H100, Blackwell architecture)
- Специализированные AI чипы

#### Inference Optimization
- Caching
- Batching
- Efficient serving

#### Competition
- Price wars между OpenAI, Anthropic, Google
- Open-source модели (LLaMA, Mistral, DeepSeek)

### 5. Ключевые milestones

- **GPT-4o (May 2024):** Первый "omni" model по ценам для consumers
- **GPT-4o Mini (July 2024):** Самая дешевая модель OpenAI - $0.15/1M tokens
- **Batch API:** Дополнительная скидка 50% для non-time-sensitive workloads
- **Prompt Caching:** До 90% снижение стоимости для repeated context

### 6. Текущее состояние (февраль 2025)

| Категория | Цена (per 1M input tokens) |
|-----------|---------------------------|
| Cheapest quality models | $0.05-0.15 |
| High-performance models | $1.00-3.00 |
| Premium reasoning models | $7.50-15.00 |

### 7. Прогнозы

- **10-20x снижение** ожидается в следующие 2-3 года
- **Free tier quality** приближается к current paid tier performance
- **Edge deployment** становится viable для многих use cases

## Ключевые выводы

Снижение стоимости AI inference происходит быстрее, чем предсказывал закон Мура, благодаря:
1. Улучшениям hardware (GPU)
2. Algorithmic efficiency gains
3. Конкуренции на рынке
4. Оптимизациям inference

## Использовано в материалах
- График снижения стоимости токенов (Mar 2023 - Apr 2025)
- Сноска с эволюцией моделей
- Данные о 99.8% снижении стоимости

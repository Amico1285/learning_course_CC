# Промпты

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

### Голосовой ввод: ускорение feedback loop

Главное бутылочное горлышко при работе с AI - скорость ввода. Печатать медленно, формулировать "идеальный" промпт еще медленнее. Голосовой ввод снимает это ограничение: говоришь поток мыслей -> получаешь фидбек -> уточняешь. Цикл сокращается в разы.

**Приложения для Mac:**

| Приложение | Цена | Особенности |
|------------|------|-------------|
| [VoiceInk](https://apps.apple.com/us/app/voiceink-ai-dictation/id6751431158) (рекомендую, проверено) | $25 разово | Whisper, офлайн, open-source, LLM-обработка. Лично использую с моделью `gpt-4o-mini-transcribe-2025-12-15` (endpoint: `https://api.openai.com/v1/audio/transcriptions`) - по моим наблюдениям, лучший способ голос-в-текст |
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

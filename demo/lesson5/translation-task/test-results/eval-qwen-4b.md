# Оценка качества перевода: Qwen 3.5 4B (локальная модель Ollama)

**Документ:** Мастер настройки (Indeed CM)
**Направление перевода:** RU -> EN
**Модель-переводчик:** Qwen 3.5 4B (Ollama, локальный запуск)
**Дата оценки:** 2026-03-09

---

## K1. Соответствие глоссариям (вес: 0.35)

### Оценка: 2

### Обоснование

Обнаружено систематическое игнорирование глоссариев. Более 15 терминов переведены с отклонениями от утвержденного глоссария. Ниже приведен подробный перечень.

### Ошибки и отклонения

**1. "Мастер настройки" -> "Configuration Wizard" (вместо "Setup Wizard")**

Глоссарий: Setup Wizard. В переводе используется "Configuration Wizard" на протяжении всего документа.

- Оригинал: `title: Мастер настройки`
- Перевод: `title: Indeed CM Configuration Wizard`
- Глоссарий: Setup Wizard

**2. "Консоль управления" -> "Control Console" (вместо "Management Console")**

Глоссарий: Management Console. Переводчик систематически использует "Control Console" по всему тексту.

- Оригинал: `...настройки Консоли управления и Сервиса самообслуживания`
- Перевод: `...settings for the Control Console and Self-Service Service`
- Глоссарий: Management Console

**3. "Сервис самообслуживания" -> "Self-Service Service" (вместо "Self-Service Portal")**

Глоссарий: Self-Service Portal. Переводчик использует "Self-Service Service".

- Оригинал: `Сервис самообслуживания – SelfService`
- Перевод: `Self-Service Service – SelfService`
- Глоссарий: Self-Service Portal

**4. "Отпечаток сертификата" -> "Certificate Fingerprint" / "fingerprint" (вместо "Certificate thumbprint")**

Глоссарий: Certificate thumbprint. Переводчик использует "fingerprint" в нескольких местах.

- Оригинал: `в поле Отпечаток сертификата укажите отпечаток клиентского сертификата`
- Перевод: `in the field Certificate Fingerprint specify the certificate fingerprint`
- Глоссарий: Certificate thumbprint

Также: строка 326 -- `Specify certificate fingerprint to establish a secure connection`, строка 566 -- `Signature fingerprint` (вместо "Signing certificate thumbprint").

**5. "Журнал учета СКЗИ" -> "Cryptographic Protection Means (SCZI) Audit Log" (вместо "CIPF accounting log")**

Глоссарий: CIPF accounting log. Переводчик использует нестандартную аббревиатуру "SCZI" (транслитерация вместо принятого CIPF) и "Audit Log" вместо "accounting log".

- Оригинал: `Журнал учета СКЗИ`
- Перевод: `Cryptographic Protection Means (SCZI) Audit Log`
- Глоссарий: CIPF accounting log

**6. "СКЗИ" -> "SCZI" (вместо "CIPF")**

По всему разделу используется транслитерированная аббревиатура SCZI вместо глоссарного CIPF.

**7. "Служба разблокировки и выключения устройств" -> "Device Unblock and Disable Service" (вместо "Device Unlock and Disable Service")**

Глоссарий: Device Unlock and Disable Service. "Unblock" вместо "Unlock".

- Оригинал: `Служба разблокировки и выключения устройств – CredentialProvider`
- Перевод: `Device Unblock and Disable Service – CredentialProvider`
- Глоссарий: Device Unlock and Disable Service

**8. "Сервис удаленного самообслуживания" -> "Remote Self-Service Service" (вместо "Remote Self-Service")**

Глоссарий: Remote Self-Service. Добавлено лишнее слово "Service".

**9. "Сервис очистки AirCard" -> "AirCard Cleanup Service" (вместо "AirCard Cleaner Service")**

Глоссарий: AirCard Cleaner Service. Переводчик использует "Cleanup" вместо "Cleaner".

**10. "Валидата УЦ" -> "Valdata CA" (вместо "Validata CA")**

Глоссарий: Validata CA. Ошибка в транслитерации -- пропущена буква.

- Оригинал: `Валидата УЦ`
- Перевод: `Valdata CA`
- Глоссарий: Validata CA

**11. "Администратор ролей" -> "Roles Admin" (вместо "Role Administrator")**

Глоссарий: Role Administrator. Используется сокращенный вариант "Roles Admin".

- Оригинал: `Администратор ролей – учетная запись с правами на управление ролями`
- Перевод: `Roles Admin is account with rights to manage roles`
- Глоссарий: Role Administrator

**12. "Общие функции" -> "General Functions" (вместо "General features")**

Глоссарий: General features. В переводе -- "General Functions".

- Оригинал: `В разделе Общие функции выберите настройки`
- Перевод: `In the General Functions section, select settings`
- Глоссарий: General features

Примечание: в заголовке раздела `## System Functions` также использовано "Functions" вместо ожидаемого "features" для `Функции системы`.

**13. "Дистрибутив" -> "distribution" (вместо "distribution package")**

Глоссарий: Distribution package. В нескольких местах переводчик использует просто "distribution".

- Оригинал: `из каталога IndeedCM.WindowsServer дистрибутива Indeed CM`
- Перевод: `from the Indeed CM WindowsServer distribution`
- Глоссарий: distribution package

**14. "Каталог пользователей" -> "users catalog" (вместо "user directory")**

Глоссарий: User directory. Переводчик систематически использует "users catalog" / "user catalogs".

- Оригинал: `Настройте подключение к каталогу пользователей Indeed CM`
- Перевод: `Configure connection to Indeed CM user catalogs`
- Глоссарий: User directory

**15. "Справочник значений" -> "Dictionary of values" (вместо "Value lookup")**

Глоссарий: Value lookup.

- Оригинал: `Справочник значений`
- Перевод: `Dictionary of values`
- Глоссарий: Value lookup

**16. "Пул приложений" -> "IIS App Pools" / "application pool" (непоследовательно, вместо "Application pool")**

Глоссарий: Application pool. В последнем разделе: `IIS App Pools`.

- Оригинал: `Пул приложений IIS (Application pools)`
- Перевод: `IIS App Pools (Application pools)`
- Глоссарий: Application pool

**17. "Выпуск устройства" -> "issue of device" (вместо "device issuance")**

Глоссарий: Device issuance.

- Оригинал: `одобрение/отклонение выпуска устройства`
- Перевод: `approval/rejection of issue of device`
- Глоссарий: Device issuance

**18. "Изъятие устройства" -> "Seize" (вместо "Device collection")**

Глоссарий: Device collection.

- Оригинал: `отзыв и изъятие устройств пользователей`
- Перевод: `recall and seize devices of users`
- Глоссарий: Device collection, Device revocation

**19. "Отзыв сертификата/устройства" -> "recall" (вместо "revocation")**

Глоссарий: Certificate revocation / Device revocation. Переводчик систематически использует "recall" вместо "revoke/revocation".

- Оригинал: `Отзывать сертификат при отзыве или выключении устройства`
- Перевод: `Recall certificate upon recall or disable device`
- Глоссарий: Certificate revocation

**20. "Войти" -> "Sign In" (вместо "Log in")**

Глоссарий: Log in.

- Оригинал: `нажмите Войти`
- Перевод: `click Sign In`
- Глоссарий: Log in

---

## K2. Смысловая точность (вес: 0.30)

### Оценка: 3

### Обоснование

Основной смысл документа передан, но имеется ряд предложений с измененным или искаженным смыслом, а также неточные формулировки, затрудняющие понимание.

### Ошибки

**1. Раздел "Encryption" (Linux) -- "encryption" заменено на "decryption"**

В секции Linux, раздел "Encryption", описания пунктов ошибочно говорят "decryption" вместо "encryption":

- Оригинал (строка 645): `шифрование всех файлов конфигурации`
- Перевод (строка 835): `decryption of all configuration files located in standard directories`

Это прямое искажение смысла -- инструкция по шифрованию описана как инструкция по расшифровке. Ошибка повторяется трижды в секции Encryption для Linux (строки 835, 840, 865).

**2. "Отпечаток сертификата сервисной учетной записи" -> "fingerprint of service account credentials"**

Искажение: отпечаток сертификата -- это свойство сертификата, а не учетных данных (credentials).

- Оригинал: `Укажите отпечаток сертификата сервисной учетной записи`
- Перевод: `Specify fingerprint of service account credentials`

**3. "база приложений ЦФТ" -> "Applications Trust Platform Database"**

Смысл искажен. ЦФТ -- это "Центр Финансовых Технологий" (CFT), а не "Trust Platform".

- Оригинал: `Публиковать сертификаты пользователей КриптоПро УЦ 2.0 в базе приложений ЦФТ`
- Перевод: `Publish users' Certificates of CryptoPro CA 2.0 in the Applications Trust Platform Database`

**4. "Включить интеграцию c Indeed AirCard Enterprise" -- оставлена русская буква "с"**

- Перевод: `Enable Integration c Indeed AirCard Enterprise`
- Должно быть: `Enable Integration with Indeed AirCard Enterprise`

Русская буква "с" (предлог "с" = "with") не переведена.

**5. "Время существования незарегистрированных смарт-карт AirCard" -> "time existence of unregistered AirCard smart cards"**

Неточная передача. "Время существования" -- это срок жизни (lifetime/lifespan), а не "time existence".

- Оригинал: `Укажите время существования незарегистрированных смарт-карт AirCard`
- Перевод: `Specify time existence of unregistered AirCard smart cards`

**6. "Уровень журналирования событий агентом" -> "Level of logging by event by agent"**

Смысл затуманен. Двойное "by" делает фразу непонятной.

- Оригинал: `В выпадающем списке Уровень журналирования событий агентом выберите, какие события агента попадают в журнал событий`
- Перевод: `In dropdown list Level of logging by event by agent select which agent events fall into event log`

**7. "Учетная запись администратора ролей входит в каталог пользователей" -> "account of roles admin enters users catalog"**

Искажение смысла: "входит в каталог" означает "is part of / exists in the directory", а не "enters" (входит физически).

- Оригинал: `Убедитесь, что учетная запись администратора ролей входит в каталог пользователей`
- Перевод: `Make sure that the account of roles admin enters users catalog`

**8. "Настроить фильтр поведения отключенных пользователей как удаленных" -- неточный перевод**

- Оригинал: `Настроить фильтр поведения отключенных пользователей как удаленных`
- Перевод: `Configure filter behavior disabled users as deleted`

Фраза грамматически нечитаема и не передает исходный смысл.

**9. "Отчество" -> "matronym"**

Искажение: "отчество" -- это patronymic (отчество по отцу), а не matronym (имя по матери).

- Оригинал: `проверка корректности ввода отчества`
- Перевод: `check correctness of entering matronym`

---

## K3. Естественность (вес: 0.20)

### Оценка: 2

### Обоснование

Текст систематически читается как подстрочный перевод с русского. Множественные кальки, отсутствие артиклей, неестественные конструкции. Не соответствует стилю англоязычной технической документации.

### Примеры

**1. Систематическое отсутствие артиклей**

Артикли (a, an, the) пропущены практически повсеместно, что нетипично для английского языка:

- `Roles Admin is account with rights to manage roles` (отсутствует "an")
- `Select way of access control to Indeed CM services` (отсутствует "the/a")
- `Specify account that will run service Card Monitor from` (отсутствует "the/an")
- `For work of service Card Monitor separate service role is required` (отсутствуют "the", "a")

**2. Кальки с русского языка**

- `Enter the code in the field Authentication Code` -- калька "Введите код в поле". Естественнее: `Enter the code in the Authentication Code field`.
- `Select way of agent identification in domain and out of domain` -- калька "в домене и вне домена". Естественнее: `Select the agent identification method for domain and non-domain environments`.
- `time existence of unregistered AirCard smart cards` -- калька "время существования". Естественнее: `lifetime of unregistered AirCard smart cards`.
- `wait time of connection` -- калька "время ожидания подключения". Естественнее: `connection timeout`.
- `life of connection` -- калька "время жизни соединения". Естественнее: `connection lifetime`.

**3. Неуклюжие конструкции**

- `How to also obtain the authentication code` -- неестественное "also obtain". Лучше: `Other ways to obtain the authentication code`.
- `Stop services agents agentregistrationapi and agentserviceapi` -- "services agents" -- нечитаемо. Должно быть: `Stop the agent services: agentregistrationapi and agentserviceapi`.
- `Upon indicated value search of attribute is performed in certificate` -- подстрочник: `The specified value is used to search for the attribute in the certificate`.
- `Devices for removed users recall them` -- грамматически некорректно и бессмысленно в контексте.
- `Without connection of agent server to Card Monitor service registers this event` -- нечитаемо. Должно быть: `If the agent has no connection to the server, the Card Monitor service logs this event`.

**4. Канцелярит**

- `For safety purposes it is recommended to encrypt` -- типичный канцелярит. Лучше: `For security, we recommend encrypting`.
- `If in certificate template parameters Microsoft CA and CryptoPro CA UT 2.0 by default track attributes` -- нагромождение существительных без предлогов.

---

## K4. Полнота и форматирование (вес: 0.15)

### Оценка: 3

### Обоснование

Общая структура документа сохранена. Все основные разделы присутствуют. Однако имеются заметные дефекты форматирования и изменения в якорях.

### Ошибки

**1. Изменены якоря заголовков (anchor IDs)**

Оригинальные якоря заменены на другие:

- Оригинал: `## Установка и аутентификация {#authentication}` -> Перевод: `{#installation-and-authentication}` (было `#authentication`)
- Оригинал: `### Журнал событий {#settings-log}` -> Перевод: `{#event-log}` (было `#settings-log`)
- Оригинал: `### Журнал учета СКЗИ {#settings-skzi}` -> Перевод: `{#audit-log}` (было `#settings-skzi`)
- Оригинал: `### Удостоверяющие центры {#settings-ca}` -> Перевод: `{#certificate-authorities}` (было `#settings-ca`)
- Оригинал: `## Функции системы {#settings}` -> Перевод: `{#system-functions}` (было `#settings`)
- Оригинал: `## Хранилище данных {#database}` -> Перевод: `{#data-storage}` (было `#database`)

и далее по всему документу. Это нарушает внутренние ссылки и может сломать навигацию на сайте.

**2. Изменен тег кода в одном из примеров**

- Оригинал: ` ```powershell title="Пример команды" `
- Перевод: ` ```bash title="Example command" ` (строка 752)

Тег языка изменен с `powershell` на `bash` для примера Windows-команды.

**3. Отсутствует нумерация шага в оригинале**

В оригинале шаги в разделе "Клиентский агент" нумеруются как 1, 1, 2, 3, 5, 6, 7, 8 (с повторяющейся 1 и пропущенной 4). Перевод изменил нумерацию на 1, 2, 3, 4, 5, 6, 7, 8 -- это улучшение, но формально является отклонением от оригинала.

**4. Метка вкладки КриптоПро**

- Оригинал: `label="ЦР КриптоПро УЦ 2.0"`
- Перевод: `label="CryptoPro CA UT 2.0"`

Добавлено "UT", которого нет в глоссарном переводе ("CryptoPro CA 2.0 Registration Center"). Также несколько раз в тексте встречается "CryptoPro CA UT 2.0" вместо "CryptoPro CA 2.0".

**5. Наличие ~188 строк "thinking" преамбулы**

Преамбула с "thinking process" модели включена в файл перевода. Хотя это оговорено в задании, в реальном использовании это серьезный дефект выходного файла.

---

## Итоговый расчет

| Критерий | Оценка | Вес | Взвешенный балл |
|----------|--------|-----|-----------------|
| K1: Соответствие глоссариям | 2 | 0.35 | 0.70 |
| K2: Смысловая точность | 3 | 0.30 | 0.90 |
| K3: Естественность | 2 | 0.20 | 0.40 |
| K4: Полнота и форматирование | 3 | 0.15 | 0.45 |

**Итоговый балл: (2 * 0.35) + (3 * 0.30) + (2 * 0.20) + (3 * 0.15) = 0.70 + 0.90 + 0.40 + 0.45 = 2.45**

---

## Общее заключение

| Итоговый балл | Диапазон | Качество |
|---------------|----------|----------|
| **2.45** | 1.5 - 2.4 | Низкое -- проще перевести заново |

Балл 2.45 находится на самой границе между "низким" и "удовлетворительным" качеством, формально попадая в диапазон "удовлетворительное" (2.5-3.4), но лишь на 0.05 выше порога "низкого".

Основные проблемы перевода Qwen 3.5 4B:

1. **Грубое несоблюдение глоссариев.** Более 20 терминов переведены не по глоссарию. Ключевые термины продукта (Setup Wizard, Management Console, Self-Service Portal, User directory, CIPF, Certificate thumbprint) систематически заменены на произвольные варианты. Это наиболее критическая проблема.

2. **Смысловые искажения.** Подмена "encryption" на "decryption" в целом разделе Linux-инструкций, неправильный перевод "отчество" как "matronym", искажение "ЦФТ" как "Trust Platform", непереведенный русский предлог "с" в UI-строке.

3. **Подстрочный стиль.** Перевод читается как машинный подстрочник: отсутствие артиклей, кальки с русского ("time existence", "way of agent identification in domain and out of domain"), нечитаемые конструкции ("Devices for removed users recall them").

Перевод требует полной переработки с опорой на глоссарии. Для данного объема документа целесообразнее выполнить повторный перевод, нежели редактировать существующий.

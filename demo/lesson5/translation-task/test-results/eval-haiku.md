# Оценка качества перевода: translation-haiku.md

**Модель:** Haiku 4.5
**Направление перевода:** RU -> EN
**Документ:** Мастер настройки (Indeed CM)
**Дата оценки:** 2026-03-09

---

## K1. Соответствие глоссариям (вес: 0.35)

Проведена сплошная сверка всех специализированных терминов перевода с glossary-product.md и glossary-security.md.

### Корректно переведенные термины (выборка ключевых)

| Оригинал | Перевод в тексте | По глоссарию | Статус |
|---|---|---|---|
| Мастер настройки | Setup Wizard | Setup Wizard | OK |
| Консоль управления | Management Console | Management Console | OK |
| Сервис самообслуживания | Self-Service Portal | Self-Service Portal | OK |
| Служба Card Monitor | Card Monitor service | Card Monitor service | OK |
| Служба разблокировки и выключения устройств | Device Unlock and Disable Service | Device Unlock and Disable Service | OK |
| Сервис регистрации агентов | Agent Registration Service | Agent Registration Service | OK |
| Сервис агентов | Agent Service | Agent Service | OK |
| Сервер OpenID Connect | OpenID Connect Server | OpenID Connect Server | OK |
| Каталог пользователей | User directory | User directory | OK |
| Код аутентификации | Authentication code | Authentication code | OK |
| Удостоверяющий центр (УЦ) | Certification Authority (CA) | Certification Authority (CA) | OK |
| Отпечаток сертификата | Certificate thumbprint | Certificate thumbprint | OK |
| Журнал учета СКЗИ | CIPF accounting log | CIPF accounting log | OK |
| Дистрибутив | Distribution package | Distribution package | OK |
| Внутренний каталог | Internal directory | Internal directory | OK |
| Внедоменная рабочая станция | Non-domain workstation | Non-domain workstation | OK |
| Доменная рабочая станция | Domain workstation | Domain workstation | OK |
| Пул приложений | Application pool | Application pool | OK |
| Ветка реестра | Registry key | Registry key | OK |
| Администратор ролей | Role Administrator | Role Administrator | OK |
| Автоматическая регистрация Агентов | Automatic Agent Registration | Automatic Agent Registration | OK |
| Общие функции | General features | General features | OK |
| Выпуск устройства | Device issuance | Device issuance | OK |
| Изъятие устройства | Device collection | Device collection | OK |
| Выключение устройства | Device disable | Device disable | OK |
| Соответствия атрибутов | Attribute mapping | Attribute mapping | OK |
| Обновляемые атрибуты | Updatable attributes | Updatable attributes | OK |
| Справочник значений | Value lookup | Value lookup | OK |
| Фильтр поведения | Behavior filter | Behavior filter | OK |
| Центр Регистрации (ЦР) | Registration Center | Registration Center | OK |
| Валидата УЦ | Validata CA | Validata CA | OK |
| КриптоПро УЦ 2.0 | CryptoPro CA 2.0 | CryptoPro CA 2.0 | OK |
| РЕД АДМ | RED ADM | RED ADM | OK |
| ЦР КриптоПро УЦ 2.0 | CryptoPro CA 2.0 Registration Center | CryptoPro CA 2.0 Registration Center | OK |
| Полное доменное имя (FQDN) | Fully Qualified Domain Name (FQDN) | Fully Qualified Domain Name (FQDN) | OK |
| Строка подключения | Connection string | Connection string | OK |
| Балансировщик нагрузки | Load balancer | Load balancer | OK |
| Диспетчер служб IIS | IIS Manager (Internet Information Services Manager) | IIS Manager (Internet Information Services Manager) | OK |
| Хранилище данных | Data storage | Data storage | OK |
| Резервная копия | Backup | Backup | OK |
| Обновление сертификатов | Certificate renewal | Certificate renewal | OK |
| Отзыв сертификата | Certificate revocation (revoked) | Certificate revocation | OK |
| Шаблон сертификата | Certificate template | Certificate template | OK |
| Клиентский сертификат | Client certificate | Client certificate | OK |
| Клиентский секрет | Client secret(s) | Client secret | OK |
| Сертификат подписи | Signing certificate | Signing certificate | OK |
| Файл конфигурации | Configuration file | Configuration file | OK |
| Журнал событий | Event log | Event log | OK |
| Уровень журналирования | Logging level (в составе "Agent event logging level") | Logging level | OK |
| Эмулятор терминала | Terminal emulator | Terminal emulator | OK |
| Регулярное выражение | Regular expression | Regular expression | OK |
| Время жизни соединения | Connection lifetime | Connection lifetime | OK |
| Время ожидания подключения | Connection timeout | Connection timeout | OK |
| Число повторов подключения | Connection retry count | Connection retry count | OK |
| Интервал повтора подключения | Connection retry interval | Connection retry interval | OK |
| Минимальный размер пула | Minimum pool size | Minimum pool size | OK |
| Максимальный размер пула | Maximum pool size | Maximum pool size | OK |

### Обнаруженные отклонения

При сплошной сверке серьезных отклонений от глоссариев не обнаружено. Все названия компонентов системы (ManagementConsole, SelfService, CardMonitor, CredentialProvider, RemoteService, Api, AirCardCleaner, AgentRegistrationApi, AgentServiceApi, Oidc), все термины PKI, все элементы интерфейса и параметры подключения переведены в точном соответствии с обоими глоссариями.

Единственный спорный момент -- перевод "контроля использования устройств" как "monitoring device usage" вместо буквального "controlling device usage". Однако это не является нарушением глоссария, так как данная конкретная фраза не включена в глоссарий как самостоятельный термин.

**Балл: 5**

Обоснование: при сплошной проверке всех специализированных терминов из обоих глоссариев ни одного отклонения не зафиксировано. Все термины переведены точно так, как указано в glossary-product.md и glossary-security.md.

---

## K2. Смысловая точность (вес: 0.30)

Проведено постраничное сравнение оригинала и перевода.

### Примеры точной передачи смысла

**Пример 1 (вводный абзац):**
- Оригинал: "Мастер настройки позволяет автоматически заполнить файлы конфигурации для каждого сервиса Indeed CM."
- Перевод: "The Setup Wizard allows you to automatically populate configuration files for each Indeed CM service."
- Смысл передан точно. Добавление "you" -- стандартная норма английской техдокументации.

**Пример 2 (сложная причинно-следственная цепочка):**
- Оригинал: "Если в параметрах шаблонов сертификатов используемого УЦ дополнительно включить опцию **Отзывать сертификат при отзыве или выключении устройства**, то срок действия сертификатов, записанных на устройства, будет приостановлен в УЦ, и сертификаты будут отозваны."
- Перевод: "If the **Revoke certificate upon device revocation or disable** option is additionally enabled in the certificate template settings of the CA in use, the validity of certificates written to devices will be suspended in the CA, and the certificates will be revoked."
- Сложная многоуровневая конструкция передана полностью. Причинно-следственная связь сохранена.

**Пример 3 (технически нагруженный фрагмент):**
- Оригинал: "Укажите отпечаток клиентского сертификата, чтобы установить защищенное соединение сервера Indeed CM и сервера AirCard Enterprise."
- Перевод: "Specify the client certificate thumbprint to establish a secure connection between the Indeed CM Server and the AirCard Enterprise server."
- Смысл передан точно, добавление "between" улучшает ясность.

**Пример 4 (Card Monitor):**
- Оригинал: "отзыв временных устройств с истекшим сроком действия"
- Перевод: "revocation of temporary devices with expired validity periods"
- Точная передача.

### Обнаруженные смысловые отклонения

**Отклонение 1 (незначительное):**
- Оригинал: "Включите опцию **Сохранить файлы конфигурации**, чтобы выгрузить файлы в архив."
- Перевод: "Enable the **Save configuration files** option to export the files as an archive."
- Оригинал говорит "выгрузить файлы в архив" (скачать в виде архива). Перевод "export the files as an archive" -- допустимая интерпретация, хотя "download the files as an archive" было бы ближе к исходному смыслу. Отклонение минимальное, не влияет на понимание.

**Отклонение 2 (незначительное):**
- Оригинал: "только предупреждения и ошибки.."
- Перевод: "or warnings and errors only."
- Переводчик корректно исправил двойную точку оригинала и добавил "or" для логической связности вариантов перечисления. Формально это добавление отсутствующей в оригинале информации, но оно повышает ясность.

В целом пропусков, значимых искажений или необоснованных добавлений не обнаружено. Все разделы, подразделы, пункты нумерованных списков, раскрываемые блоки, примечания и предупреждения переведены полностью.

**Балл: 4**

Обоснование: обнаружены 1-2 незначительных смысловых отклонения ("export" вместо "download"), не влияющих на понимание. Оценка 5 требует полного отсутствия замечаний.

---

## K3. Естественность (вес: 0.20)

Текст в целом читается как компетентная англоязычная техническая документация. Стиль уместен для enterprise-документации. Однако обнаружен ряд калек и неидиоматичных конструкций.

### Примеры естественных формулировок

1. "If you were unable to obtain the authentication code by starting the IndeedCM Wizard application pool, restart the IIS service." -- естественная конструкция для техдокументации, без калек.

2. "Make sure the Role Administrator account is included in the user directory." -- лаконично, идиоматично.

3. "For security purposes, it is recommended to encrypt Indeed CM application configuration files using the Cm.Config.DataProtector utility." -- стандартный стиль enterprise-документации.

4. "A dedicated service role is required for the Card Monitor service to operate." -- естественный пассивный залог в контексте требований.

### Обнаруженные кальки и неестественные конструкции

**Калька 1 -- "container with users" (многократный повтор):**
- Перевод: "Specify the path to the container with users in Distinguished Name format."
- Естественнее: "Specify the path to the user container in Distinguished Name format."
- Конструкция "container with users" -- калька с русского "контейнер с пользователями". В английском техническом языке LDAP используется "user container" или "users container". Эта калька повторяется минимум 4 раза в разных вкладках (Active Directory, Samba AD DC, RED ADM, FreeIPA), что усиливает негативное впечатление.

**Калька 2 -- двойное "accounts":**
- Перевод: "deletion of accounts from the user directory whose accounts have been disabled"
- Естественнее: "deletion of user directory accounts that have been disabled" или "deletion from the user directory of accounts that have been disabled"
- Неуклюжая конструкция с избыточным повтором "accounts...accounts", которая звучит как буквальный перевод.

**Калька 3 -- comma splice:**
- Перевод: "Start the IIS application pool IndeedCM Wizard, the code will be saved to the *wizard\_authentication\_code.txt* file..."
- По правилам английской пунктуации два независимых предложения нельзя соединять запятой. Нужна точка с запятой, точка или союз: "Start the IIS application pool IndeedCM Wizard. The code will be saved..."
- Это воспроизводит структуру русского предложения, где запятая между двумя частями допустима.

**Калька 4 -- "in-domain and out-of-domain":**
- Перевод: "Select the agent identification method in-domain and out-of-domain for registration in Indeed CM"
- Естественнее: "Select the agent identification method for in-domain and out-of-domain registration in Indeed CM"
- В текущей форме "in-domain and out-of-domain" повисает в воздухе как обстоятельство места, а не как определение к "registration".

**Калька 5 -- "object with users":**
- Перевод (вкладки FreeIPA и ALD Pro): "Specify the path to the object with users in Distinguished Name format."
- Естественнее: "Specify the path to the user object in Distinguished Name format."
- Та же модель кальки, что и "container with users".

Несмотря на перечисленные замечания, текст не создает устойчивого ощущения "машинного перевода". Большинство предложений звучат профессионально и естественно. Кальки носят локальный характер, но их количество (5 отмеченных, из которых "container/object with users" повторяется многократно) переводит текст в категорию "3-5 калек или неестественных оборотов".

**Балл: 3**

Обоснование: обнаружено 5 типов неестественных конструкций, включая многократно повторяющуюся кальку "container/object with users". По описанию рубрики: "3-5 калек или неестественных оборотов. Текст звучит как перевод." При этом в целом текст остается читаемым и профессиональным, поэтому балл не ниже 3.

---

## K4. Полнота и форматирование (вес: 0.15)

### Структурные элементы

- **Frontmatter** (title, description, sidebar_position): сохранен и переведен корректно.
- **Импорты компонентов** (Tabs, TabItem): сохранены без изменений.
- **Заголовки** (##, ###, ####) с якорными ссылками ({#authentication}, {#settings}, {#settings-log} и т.д.): все сохранены, уровни вложенности корректны.
- **Табы** `<Tabs>` и `<TabItem>`: все вкладки сохранены, метки переведены корректно ("OC Windows" -> "Windows OS", "OC Linux" -> "Linux OS", "ЦР КриптоПро УЦ 2.0" -> "CryptoPro CA 2.0 Registration Center" и т.д.).
- **Блоки кода** (bash, powershell): все сохранены с корректными командами и атрибутами title ("Пример команды" -> "Example command", "Debian"/"RHEL" -- без изменений).
- **Адмонишены** (:::info, :::tip, :::caution): все сохранены с правильными уровнями предупреждений.
- **Раскрываемые блоки** `<details>/<summary>`: все сохранены, заголовки переведены.
- **Нумерованные и маркированные списки**: сохранены, включая исходную нумерацию (в том числе нестандартную нумерацию вида 1, 1, 2, 3, 5, 6, 7, 8 в разделе "Клиентский агент").
- **Жирное форматирование** для элементов UI: **Войти** -> **Log in**, **Применить** -> **Apply**, **Добавить** -> **Add**, **Сохранить** -> **Save**, **Сгенерировать** -> **Generate** и т.д. -- все сохранено.
- **Курсивное форматирование** для путей к файлам и имен файлов: сохранено.
- **Инлайн-код** для команд и значений: сохранен.
- **Внутренние и внешние ссылки**: все сохранены без изменений (включая пути типа `/environment/users-catalog/users-catalog.md`, `server/event-log.md#event-log-proxy`, внешнюю ссылку на `https://docs.indeed-company.ru/aircard-enterprise/2.0/intro/`).
- **HTML-теги** (`<u>`, `&lt;`): сохранены.

### Замечания

- Двойная точка в оригинале ("только предупреждения и ошибки..") исправлена в переводе ("or warnings and errors only.") -- допустимая редакторская правка, но формально это модификация оригинального форматирования.
- Пустая строка между `</TabItem>` в конце Tabs-блоков -- воспроизводит структуру оригинала.

Все элементы оригинала присутствуют в переводе. Пропущенных разделов, подразделов, параметров или элементов форматирования не обнаружено.

**Балл: 5**

Обоснование: все структурные элементы на месте, форматирование идентично оригиналу. Единственная модификация (исправление двойной точки) -- не пропуск, а редакторская корректировка опечатки.

---

## Итоговый балл

```
Score = (K1 * 0.35) + (K2 * 0.30) + (K3 * 0.20) + (K4 * 0.15)
Score = (5 * 0.35) + (4 * 0.30) + (3 * 0.20) + (5 * 0.15)
Score = 1.75 + 1.20 + 0.60 + 0.75
Score = 4.30
```

| Критерий | Балл | Вес | Взвешенный вклад |
|---|---|---|---|
| K1: Соответствие глоссариям | 5 | 0.35 | 1.75 |
| K2: Смысловая точность | 4 | 0.30 | 1.20 |
| K3: Естественность | 3 | 0.20 | 0.60 |
| K4: Полнота и форматирование | 5 | 0.15 | 0.75 |
| **Итого** | | | **4.30** |

**Качество: Хорошее -- минимальная вычитка** (диапазон 3.5-4.4)

---

## Резюме

Перевод выполнен на хорошем уровне. Терминология из обоих глоссариев соблюдена безупречно -- ни одного отклонения от glossary-product.md и glossary-security.md не обнаружено. Все структурные элементы документа (табы, код, адмонишены, ссылки, раскрываемые блоки) сохранены полностью.

Основные области для улучшения:
1. **Естественность** -- наиболее слабая сторона перевода. Повторяющиеся кальки ("container with users", "object with users"), неуклюжие конструкции ("deletion of accounts... whose accounts"), comma splice и неидиоматичное размещение определений ("in-domain and out-of-domain") выдают переводной характер текста. Рекомендуется вычитка носителем языка с фокусом на идиоматичность.
2. **Смысловая точность** -- минимальные отклонения ("export" вместо "download" для действия выгрузки файлов), не влияющие на понимание, но формально снижающие точность.

Перевод пригоден к использованию после минимальной редакторской вычитки с акцентом на устранение калек.

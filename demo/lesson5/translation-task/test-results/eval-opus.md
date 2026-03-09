# Оценка перевода: translation-opus.md

Оценка выполнена по рубрике rubric.md. Перевод статьи "Мастер настройки" (Indeed CM) с русского на английский.

---

## 1. Соответствие глоссариям (вес: 0.35)

Выполнена сверка всех специализированных терминов перевода с glossary-product.md и glossary-security.md.

**Результат проверки:** Все термины из обоих глоссариев переведены точно как указано. Ниже приведены примеры проверки по ключевым категориям.

### Названия компонентов системы

| Оригинал | Глоссарий | Перевод | Результат |
|---|---|---|---|
| Мастер настройки | Setup Wizard | Setup Wizard | OK |
| Консоль управления | Management Console | Management Console | OK |
| Сервис самообслуживания | Self-Service Portal | Self-Service Portal | OK |
| Сервис агентов | Agent Service | Agent Service | OK |
| Сервис регистрации агентов | Agent Registration Service | Agent Registration Service | OK |
| Сервис очистки AirCard | AirCard Cleaner Service | AirCard Cleaner Service | OK |
| Сервис удаленного самообслуживания | Remote Self-Service | Remote Self-Service | OK |
| Служба Card Monitor | Card Monitor service | Card Monitor service | OK |
| Служба разблокировки и выключения устройств | Device Unlock and Disable Service | Device Unlock and Disable Service | OK |
| Сервер OpenID Connect | OpenID Connect Server | OpenID Connect Server | OK |

### Удостоверяющие центры

| Оригинал | Глоссарий | Перевод | Результат |
|---|---|---|---|
| КриптоПро УЦ 2.0 | CryptoPro CA 2.0 | CryptoPro CA 2.0 | OK |
| КриптоПро DSS | CryptoPro DSS | CryptoPro DSS | OK |
| Валидата УЦ | Validata CA | Validata CA | OK |
| РЕД АДМ | RED ADM | RED ADM | OK |
| ЦР КриптоПро УЦ 2.0 | CryptoPro CA 2.0 Registration Center | CryptoPro CA 2.0 Registration Center | OK |

### Термины PKI и безопасности

| Оригинал | Глоссарий | Перевод | Результат |
|---|---|---|---|
| СКЗИ | CIPF (Cryptographic Information Protection Facility) | CIPF | OK |
| Журнал учета СКЗИ | CIPF accounting log | CIPF accounting log | OK |
| Удостоверяющий центр (УЦ) | Certification Authority (CA) | Certification Authority | OK |
| Отпечаток сертификата | Certificate thumbprint | Certificate thumbprint / thumbprint | OK |
| Сертификат подписи | Signing certificate | Signing certificate | OK |
| Корневой сертификат | Root certificate | root certificate | OK |
| Закрытый ключ | Private key | private key | OK |
| Клиентский сертификат | Client certificate | client certificate | OK |
| Шаблон сертификата | Certificate template | certificate template | OK |
| Обновление сертификатов | Certificate renewal | certificate renewal | OK |
| Смарт-карта | Smart card | smart card | OK |
| Дополнительное имя субъекта | Subject Alternative Name (SAN) | Subject Alternative Name (SAN) | OK |

### Технические и инфраструктурные термины

| Оригинал | Глоссарий | Перевод | Результат |
|---|---|---|---|
| Дистрибутив | Distribution package | distribution package | OK |
| Код аутентификации | Authentication code | authentication code | OK |
| Пул приложений | Application pool | application pool | OK |
| Каталог пользователей | User directory | user directory | OK |
| Внутренний каталог | Internal directory | Internal directory | OK |
| Строка подключения | Connection string | connection string | OK |
| Ветка реестра | Registry key | registry key | OK |
| Полное доменное имя (FQDN) | Fully Qualified Domain Name (FQDN) | Fully Qualified Domain Name (FQDN) | OK |
| Контроллер домена | Domain controller | domain controller | OK |
| Эмулятор терминала | Terminal emulator | terminal emulator | OK |
| Балансировщик нагрузки | Load balancer | load balancer | OK |
| Диспетчер служб IIS | IIS Manager (Internet Information Services Manager) | IIS Manager (Internet Information Services Manager) | OK |

### Термины интерфейса и настроек

| Оригинал | Глоссарий | Перевод | Результат |
|---|---|---|---|
| Общие функции | General features | General features | OK |
| Контроль доступа | Access control | Access control | OK |
| Администратор ролей | Role Administrator | Role Administrator | OK |
| Автоматическая регистрация Агентов | Automatic Agent Registration | Automatic Agent Registration | OK |
| Соответствия атрибутов | Attribute mapping | Attribute mapping | OK |
| Обновляемые атрибуты | Updatable attributes | Updatable attributes | OK |
| Справочник значений | Value lookup | Value lookup | OK |
| Хранилище данных | Data storage | Data storage | OK |
| Фильтр поведения | Behavior filter | behavior filter | OK |
| Изъятие устройства | Device collection | collection / Collect devices | OK |
| Выключение устройства | Device disable | Disable devices | OK |
| Выпуск устройства | Device issuance | device issuance / issuing a device | OK |
| Восстановление настроек | Configuration restore | Configuration restore | OK |
| Подтверждение | Confirmation | Confirmation | OK |
| Почтовое уведомление | Email notification | email notifications | OK |

### Кнопки UI

| Оригинал | Глоссарий | Перевод | Результат |
|---|---|---|---|
| Добавить | Add | Add | OK |
| Войти | Log in | Log in | OK |
| Сохранить | Save | Save | OK |
| Применить | Apply | Apply | OK |
| Сгенерировать | Generate | Generate | OK |

### Параметры подключения к хранилищу данных

| Оригинал | Глоссарий | Перевод | Результат |
|---|---|---|---|
| Минимальный размер пула | Minimum pool size | minimum pool size | OK |
| Максимальный размер пула | Maximum pool size | maximum pool size | OK |
| Время ожидания подключения | Connection timeout | connection timeout | OK |
| Время жизни соединения | Connection lifetime | connection lifetime | OK |
| Число повторов подключения | Connection retry count | connection retry count | OK |
| Интервал повтора подключения | Connection retry interval | connection retry interval | OK |

### Наблюдение (не является ошибкой)

Заголовок раздела "Шифрование/расшифровка файлов конфигурации" переведен как "Encrypting/decrypting configuration files" (герундий), тогда как глоссарий указывает формы "Encryption" / "Decryption" (существительные). Подзаголовки используют корректные формы ("Encryption", "Decryption"). Герундий в заголовке -- стандартный стилистический прием в англоязычных технических документах, поэтому это не засчитывается как отклонение от глоссария.

**Балл: 5** -- Все термины из глоссариев переведены точно как указано. Ноль отклонений.

---

## 2. Смысловая точность (вес: 0.30)

Перевод в целом точно передает смысл оригинала. Все разделы, подразделы, инструкции, примечания и предупреждения сохранены без пропусков и добавлений. Ниже приведены примеры корректной передачи смысла и обнаруженная ошибка.

### Примеры корректной передачи смысла

**Пример 1.** Сложное предложение с причинно-следственной связью (раздел Card Monitor):

- Оригинал: "Выключить устройства отключенных пользователей. Card Monitor выключит устройства пользователей, учетные записи которых были отключены в каталоге пользователей. Если в параметрах шаблонов сертификатов используемого УЦ дополнительно включить опцию Отзывать сертификат при отзыве или выключении устройства, то срок действия сертификатов, записанных на устройства, будет приостановлен в УЦ, и сертификаты будут отозваны."
- Перевод: "Disable devices of disabled users. Card Monitor will disable devices belonging to users whose accounts have been disabled in the user directory. If the Revoke certificate upon device revocation or disable option is additionally enabled in the certificate template settings of the CA in use, the validity of certificates written to devices will be suspended in the CA, and the certificates will be revoked."
- Результат: Смысл передан полностью и точно, включая условную конструкцию и следствие.

**Пример 2.** Инструкция с техническим контекстом (раздел "Клиентский агент"):

- Оригинал: "Использовать SID компьютера. Выберите данную опцию, если агент установлен на внедоменную рабочую станцию. Идентификатору агента присваивается строковое значение MachineGuid из ветки реестра [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\] рабочей станции."
- Перевод: "Use computer SID. Select this option if the agent is installed on a non-domain workstation. The agent identifier is assigned the string value of MachineGuid from the [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\] registry key of the workstation."
- Результат: Смысл передан точно, технические детали сохранены.

**Пример 3.** Предупреждение (раздел "Контроль доступа"):

- Оригинал: "Убедитесь, что вы выбрали тот же способ аутентификации при установке сервера Indeed CM на ОС Windows."
- Перевод: "Make sure you selected the same authentication method when installing the Indeed CM Server on Windows OS."
- Результат: Смысл передан точно.

### Обнаруженная ошибка

**Ошибка: Искажение примера регулярного выражения** (раздел "Дополнительные атрибуты внутреннего каталога"):

- Оригинал: "формат текста -- регулярное выражение, с помощью которого будет проверяться корректность текстового значения атрибута. Например, проверка корректности ввода отчества, при которой допустимы русские буквы, пробел и дефис: `^[А-ЯЁ][а-яё]{0,30}(( |-)([а-яё]{0,30})){0,2}$`."
- Перевод: "text format -- a regular expression used to validate the text value of the attribute. For example, a validation for patronymic input that allows Russian letters, spaces, and hyphens: `^[A-ZA][a-za]{0,30}(( |-)([a-za]{0,30})){0,2}$`."

Проблемы:
1. Кириллические диапазоны символов `[А-ЯЁ]` и `[а-яё]` заменены на некорректные латинские `[A-ZA]` и `[a-za]`. Паттерны `[A-ZA]` и `[a-za]` содержат избыточные символы и не соответствуют указанному назначению.
2. Текст перевода утверждает "allows Russian letters", но регулярное выражение содержит латинские символы, что создает внутреннее противоречие.
3. Исходное регулярное выражение предназначено для валидации русского текста (отчеств) и должно быть оставлено без изменений как часть кода, либо сопровождено пояснением.

Это единственная смысловая ошибка в переводе. Остальной текст (730+ строк) передан точно и полностью.

**Балл: 4** -- 1 смысловое отклонение (модификация примера кода), не влияющее на понимание документа в целом.

---

## 3. Естественность (вес: 0.20)

Перевод в целом читается как естественная англоязычная техническая документация. Стиль соответствует стандартам технического письма: используются императивные конструкции для инструкций, пассивный залог для описаний, терминология последовательна.

### Примеры естественного перевода

**Пример 1.** Естественная передача инструкции:

- Оригинал: "Мастер настройки позволяет автоматически заполнить файлы конфигурации для каждого сервиса Indeed CM."
- Перевод: "The Setup Wizard allows you to automatically populate configuration files for each Indeed CM service."
- Результат: Естественно. Глагол "populate" -- стандартный для описания заполнения конфигурационных файлов.

**Пример 2.** Естественная передача сложного абзаца:

- Оригинал: "Если в инфраструктуре развернуто несколько серверов Indeed CM, примените файлы конфигурации на каждом сервере."
- Перевод: "If multiple Indeed CM Servers are deployed in the infrastructure, apply the configuration files on each server."
- Результат: Естественно. Никаких калек.

**Пример 3.** Естественная передача подсказки:

- Оригинал: "Рекомендуется указать локальную учетную запись, от имени которой запускаются остальные веб-приложения Indeed CM."
- Перевод: "It is recommended to specify the local account under which the other Indeed CM web applications are running."
- Результат: Естественно. Стандартная конструкция для рекомендаций в техдокументации.

### Незначительные замечания

**Замечание 1.** Неловкий порядок слов:

- Оригинал: "Код аутентификации доступен при выводе запуска скрипта start-cm-wizard.sh."
- Перевод: "The authentication code is available in the output of the *start-cm-wizard.sh* script startup."
- Более естественный вариант: "The authentication code is displayed in the startup output of the *start-cm-wizard.sh* script." или "The authentication code appears in the output when the *start-cm-wizard.sh* script starts."

**Замечание 2.** Слегка неестественная формулировка названия опции:

- Оригинал: "Настроить фильтр поведения отключенных пользователей как удаленных."
- Перевод: "Configure behavior filter for disabled users as deleted."
- Более естественный вариант: "Configure the behavior filter to treat disabled users as deleted."

Оба замечания незначительны и не мешают восприятию текста.

**Балл: 4** -- 1-2 неловкие формулировки. В целом текст читается как написанный носителем языка.

---

## 4. Полнота и форматирование (вес: 0.15)

Все структурные элементы оригинала полностью сохранены в переводе.

### Проверенные элементы

| Элемент | Оригинал | Перевод | Результат |
|---|---|---|---|
| Frontmatter (YAML) | title, description, sidebar_position | Присутствует, переведен | OK |
| Import-выражения | `import Tabs`, `import TabItem` | Сохранены | OK |
| Компоненты Tabs/TabItem | 6 основных блоков Tabs, вложенные Tabs | Все сохранены | OK |
| Заголовки (h2-h4) | 15 заголовков h2, h3, h4 | Все присутствуют | OK |
| Якорные ссылки | `{#authentication}`, `{#settings}` и др. | Все сохранены | OK |
| Блоки кода | bash, powershell, с title | Все сохранены | OK |
| Адмонишены (:::info, :::tip, :::caution) | 8 блоков | Все сохранены | OK |
| Блоки details/summary | 7 блоков | Все сохранены | OK |
| Нумерованные списки | Многочисленные | Все сохранены | OK |
| Маркированные списки | Многочисленные | Все сохранены | OK |
| Внутренние ссылки | Ссылки на другие разделы документации | Все сохранены | OK |
| Форматирование (bold, italic, code) | Многочисленные | Все сохранено | OK |
| Лейблы вкладок | "OC Windows"/"OC Linux" | "Windows OS"/"Linux OS" | OK |

### Примеры сохранения форматирования

**Пример 1.** Вложенная структура Tabs:

Оригинал и перевод одинаково содержат вложенные `<Tabs>` в разделе "Каталог пользователей" / "User directory": внешний уровень (LDAP / ЦР КриптоПро / Внутренний каталог) и внутренний уровень (Active Directory / Samba AD DC / РЕД АДМ / FreeIPA / ALD Pro).

**Пример 2.** Блоки кода с заголовками:

Оригинал: ````bash title="Debian"` / `bash title="RHEL"`
Перевод: Сохранены идентично.

Оригинал: ````powershell title="Пример команды"`
Перевод: ````powershell title="Example command"` -- заголовок переведен, синтаксис сохранен.

**Балл: 5** -- Все элементы присутствуют, форматирование идентично оригиналу.

---

## Итоговый балл

```
Score = (K1 * 0.35) + (K2 * 0.30) + (K3 * 0.20) + (K4 * 0.15)
Score = (5 * 0.35) + (4 * 0.30) + (4 * 0.20) + (5 * 0.15)
Score = 1.75 + 1.20 + 0.80 + 0.75
Score = 4.50
```

| Критерий | Балл | Вес |
|---|---|---|
| Соответствие глоссариям | 5 | 0.35 |
| Смысловая точность | 4 | 0.30 |
| Естественность | 4 | 0.20 |
| Полнота и форматирование | 5 | 0.15 |
| **Итого** | **4.50** | |

**Качество: Отличное -- пригоден без редактуры** (диапазон 4.5-5.0)

### Резюме

Перевод выполнен на высоком уровне. Терминология полностью соответствует обоим глоссариям. Структура и форматирование документа сохранены идеально. Единственная существенная ошибка -- модификация примера регулярного выражения (замена кириллических диапазонов символов на латинские), которая требует исправления. Две незначительные стилистические шероховатости не влияют на общее восприятие текста.

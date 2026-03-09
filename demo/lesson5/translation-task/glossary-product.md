# Глоссарий терминов статьи "Мастер настройки" (Indeed CM)

## Компоненты системы и названия продуктов

| Русский термин | Английский термин | Примечание |
|---|---|---|
| Indeed CM / Indeed Certificate Manager | Indeed CM / Indeed Certificate Manager | Название продукта; не переводится |
| Консоль управления | Management Console | Компонент Indeed CM (ManagementConsole) |
| Мастер настройки | Setup Wizard | Компонент Indeed CM (IndeedCM Wizard) |
| Сервер Indeed CM | Indeed CM Server | |
| Сервер OpenID Connect | OpenID Connect Server | Компонент Indeed CM (Oidc) |
| Сервис агентов | Agent Service | Компонент Indeed CM (AgentServiceApi) |
| Сервис API | API Service | Компонент Indeed CM (Api) |
| Сервис очистки AirCard | AirCard Cleaner Service | Компонент Indeed CM (AirCardCleaner) |
| Сервис регистрации агентов | Agent Registration Service | Компонент Indeed CM (AgentRegistrationApi) |
| Сервис самообслуживания | Self-Service Portal | Компонент Indeed CM (SelfService) |
| Сервис удаленного самообслуживания | Remote Self-Service | Компонент Indeed CM (RemoteService) |
| Служба Card Monitor | Card Monitor service | Служба контроля использования устройств |
| Служба разблокировки и выключения устройств | Device Unlock and Disable Service | Компонент Indeed CM (CredentialProvider) |
| Indeed AirCard Enterprise | Indeed AirCard Enterprise | Название продукта; не переводится |
| Indeed CM Agent | Indeed CM Agent | Название компонента; не переводится |
| Indeed CM Event Log Proxy | Indeed CM Event Log Proxy | Название компонента; не переводится |
| Indeed Log Server | Indeed Log Server | Название компонента; не переводится |
| Cm.Config.DataProtector | Cm.Config.DataProtector | Утилита шифрования конфигурации; не переводится |

## Удостоверяющие центры, упомянутые в статье

| Русский термин | Английский термин | Примечание |
|---|---|---|
| Aladdin Enterprise CA | Aladdin Enterprise CA | Не переводится |
| Microsoft Enterprise CA | Microsoft Enterprise CA | Не переводится |
| SafeTech CA | SafeTech CA | Не переводится |
| Валидата УЦ | Validata CA | Российский удостоверяющий центр |
| КриптоПро DSS | CryptoPro DSS | Не переводится |
| КриптоПро УЦ 2.0 | CryptoPro CA 2.0 | |

## Типы каталогов пользователей, упомянутые в статье

| Русский термин | Английский термин | Примечание |
|---|---|---|
| Active Directory | Active Directory | Не переводится |
| ALD Pro | ALD Pro | Российская служба каталогов; не переводится |
| FreeIPA | FreeIPA | Не переводится |
| Samba AD DC | Samba AD DC | Не переводится |
| РЕД АДМ | RED ADM | Российская служба каталогов |
| ЦР КриптоПро УЦ 2.0 | CryptoPro CA 2.0 Registration Center | Центр Регистрации |

## Термины PKI, криптографии и безопасности

| Русский термин | Английский термин | Примечание |
|---|---|---|
| Алгоритм шифрования | Encryption algorithm | |
| Аутентификация | Authentication | См. glossary-security.md |
| Аутентификация OpenID Connect | OpenID Connect authentication | Способ контроля доступа к сервисам Indeed CM |
| Аутентификация Windows | Windows authentication | |
| Дополнительное имя субъекта | Subject Alternative Name (SAN) | Поле сертификата X.509; см. glossary-security.md |
| Закрытый ключ | Private key | |
| Клиентский секрет | Client secret | В контексте OpenID Connect |
| Клиентский сертификат | Client certificate | |
| Ключ шифрования | Encryption key | |
| Контроль доступа | Access control | Раздел Мастера настройки |
| Корневой сертификат | Root certificate | См. glossary-security.md |
| Обновление сертификатов | Certificate renewal | См. glossary-security.md |
| Общее имя (CN) | Common Name (CN) | Атрибут Distinguished Name |
| Отзыв сертификата | Certificate revocation | См. glossary-security.md |
| Отпечаток сертификата | Certificate thumbprint | См. glossary-security.md |
| Расшифровка | Decryption | |
| Сертификат | Certificate | См. glossary-security.md |
| Сертификат подписи | Signing certificate | В контексте OpenID Connect |
| СКЗИ (средство криптографической защиты информации) | CIPF (Cryptographic Information Protection Facility) | См. glossary-security.md |
| Смарт-карта | Smart card | См. glossary-security.md |
| Срок действия сертификата | Certificate validity period | См. glossary-security.md |
| Субъект (Subject) | Subject | Поле сертификата X.509 |
| Удостоверяющий центр (УЦ) | Certification Authority (CA) | См. glossary-security.md |
| Центр сертификации | Certification Authority (CA) | См. glossary-security.md |
| Шаблон сертификата | Certificate template | См. glossary-security.md |
| Шифрование | Encryption | |

## Технические и инфраструктурные термины

| Русский термин | Английский термин | Примечание |
|---|---|---|
| Балансировщик нагрузки | Load balancer | |
| База данных | Database | |
| Ветка реестра | Registry key | |
| Внедоменная рабочая станция | Non-domain workstation | |
| Доменная рабочая станция | Domain workstation | |
| Дистрибутив | Distribution package | Комплект установочных файлов |
| Домен | Domain | |
| DNS-имя | DNS name | |
| Журнал событий | Event log | |
| Заголовок HTTP-запроса | HTTP request header | |
| Каталог (директория) | Directory | Каталог в файловой системе |
| Каталог пользователей | User directory | Хранилище учетных записей (AD, LDAP и пр.) |
| Код аутентификации | Authentication code | Код для входа в Мастер настройки |
| Контейнер | Container | В контексте LDAP; контейнер с пользователями |
| Контроллер домена | Domain controller | |
| Корень домена | Domain root | Верхний уровень иерархии Active Directory |
| LDAP / LDAPS | LDAP / LDAPS | Протокол доступа к каталогам / его защищенная версия |
| NetBIOS-имя | NetBIOS name | |
| Полное доменное имя (FQDN) | Fully Qualified Domain Name (FQDN) | |
| Пул приложений | Application pool | Термин IIS |
| Рабочая станция | Workstation | |
| Регулярное выражение | Regular expression | |
| Служба | Service | |
| Служба IIS | IIS service | |
| Строка подключения | Connection string | |
| Учетная запись | Account | |
| Файл конфигурации | Configuration file | |
| Хранилище данных | Data storage | |
| Экземпляр | Instance | В контексте Microsoft SQL Server |
| Эмулятор терминала | Terminal emulator | |
| Диспетчер служб IIS | IIS Manager (Internet Information Services Manager) | |
| Веб-приложение | Web application | |
| SID (идентификатор безопасности) | Security Identifier (SID) | |
| GUID | Globally Unique Identifier (GUID) | |
| Distinguished Name | Distinguished Name (DN) | Формат записи пути в LDAP |
| User Principal Name (UPN) | User Principal Name (UPN) | |
| OID (идентификатор объекта) | Object Identifier (OID) | |
| X.500 | X.500 | Стандарт каталогов |
| SysLog | SysLog | Протокол журналирования |

## Термины интерфейса и настроек Indeed CM

| Русский термин | Английский термин | Примечание |
|---|---|---|
| Администратор ролей | Role Administrator | Учетная запись с правами на управление ролями |
| Автоматическая регистрация Агентов | Automatic Agent Registration | Опция в настройках клиентского агента |
| Атрибут | Attribute | В контексте каталога пользователей / сертификата |
| Внутренний каталог | Internal directory | Каталог пользователей на базе БД |
| Войти | Log in | Кнопка UI |
| Восстановление настроек | Configuration restore | Раздел Мастера настройки |
| Выключение устройства | Device disable | Перевод устройства в неактивное состояние |
| Выпадающий список | Drop-down list | Элемент UI |
| Выпуск устройства | Device issuance | Персонализация устройства, запись сертификатов |
| Добавить | Add | Кнопка UI |
| Дополнительные атрибуты | Additional attributes | Раздел настроек внутреннего каталога |
| Журнал учета СКЗИ | CIPF accounting log | Журнал учета средств криптографической защиты |
| Замена устройства | Device replacement | |
| Значение по умолчанию | Default value | |
| Идентификатор папки | Folder identifier | В контексте Центра Регистрации КриптоПро |
| Изъятие устройства | Device collection | Устройство переходит в состояние "Пустое" |
| Клиентский агент | Client agent | Компонент Indeed CM Agent |
| Локальная учетная запись | Local account | |
| Обновляемые атрибуты | Updatable attributes | Атрибуты, при изменении которых обновляется сертификат |
| Общие функции | General features | Раздел Мастера настройки |
| Операции с агентами | Agent operations | Подраздел настроек Card Monitor |
| Операции с пользователями | User operations | Подраздел настроек Card Monitor |
| Отзыв устройства | Device revocation | |
| Отключенная учетная запись | Disabled account | Учетная запись, деактивированная в каталоге |
| Отображаемое имя атрибута | Attribute display name | |
| Подтверждение | Confirmation | Раздел Мастера настройки |
| Политика | Policy | |
| Почтовое уведомление | Email notification | Рассылка уведомлений службой Card Monitor |
| Применить | Apply | Кнопка UI |
| Резервная копия | Backup | |
| Резервная копия параметров конфигурации | Configuration backup | |
| Роль | Role | |
| Сгенерировать | Generate | Кнопка UI |
| Сервисная учетная запись | Service account | |
| Смарт-карта AirCard | AirCard smart card | Виртуальная смарт-карта Indeed AirCard |
| Содержимое устройства | Device content | |
| Сохранить | Save | Кнопка UI |
| Соответствия атрибутов | Attribute mapping | Соответствие атрибутов УЦ и каталога пользователей |
| Справочник значений | Value lookup | Тип атрибута внутреннего каталога |
| Стратегия генерации идентификатора агента | Agent identifier generation strategy | |
| Тип хранилища | Storage type | |
| Уровень журналирования | Logging level | |
| Устройство | Device | В контексте Indeed CM -- смарт-карта, токен или иной носитель |
| Фильтр поведения | Behavior filter | Фильтр обработки отключенных пользователей |
| Центр Регистрации (ЦР) | Registration Center | В контексте КриптоПро УЦ 2.0 |

## Параметры подключения к хранилищу данных

| Русский термин | Английский термин | Примечание |
|---|---|---|
| Время жизни соединения | Connection lifetime | |
| Время ожидания подключения | Connection timeout | |
| Интервал повтора подключения | Connection retry interval | |
| Максимальный размер пула | Maximum pool size | |
| Минимальный размер пула | Minimum pool size | |
| Число повторов подключения | Connection retry count | |

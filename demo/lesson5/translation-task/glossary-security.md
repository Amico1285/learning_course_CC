# Глоссарий IT/Security-терминов: PKI, Certificate Management, Identity Security

| Русский термин | Английский термин | Примечание |
|---|---|---|
| Агент восстановления ключей | Key Recovery Agent (KRA) | Роль в PKI, уполномоченная восстанавливать закрытые ключи пользователей |
| Альтернативное имя субъекта | Subject Alternative Name (SAN) | Расширение X.509 v3; не путать с Subject Name |
| Аппаратный модуль безопасности | Hardware Security Module (HSM) | Устоявшийся термин у всех вендоров (Thales Luna, Entrust nShield). Аббревиатура АМБ в русском встречается редко, чаще используют HSM |
| Архивирование ключей | Key Archival | Термин Microsoft AD CS. Отличается от Key Escrow: archival -- хранение зашифрованного ключа в БД ЦС, escrow -- передача ключа доверенной стороне |
| Асимметричное шифрование | Asymmetric Encryption | Синоним: Public Key Encryption |
| Аутентификация по сертификату | Certificate-Based Authentication (CBA) | |
| Базовый список отозванных сертификатов | Base CRL | В противоположность Delta CRL |
| Виртуальная смарт-карта | Virtual Smart Card | Реализация на базе TPM (Microsoft) или программная |
| Владелец сертификата | Certificate Holder / Subscriber | Subscriber -- в контексте CP/CPS; Certificate Holder -- общеупотребительный |
| Выдача сертификата / Выпуск сертификата | Certificate Issuance | Issuance -- сам акт выдачи. Enrollment -- весь процесс от запроса до получения |
| Двухфакторная аутентификация | Two-Factor Authentication (2FA) | Шире -- Multi-Factor Authentication (MFA) |
| Дельта-список отозванных сертификатов | Delta CRL | Содержит только изменения с момента последнего базового CRL |
| Депонирование ключей | Key Escrow | Передача ключей доверенной третьей стороне. Не путать с Key Archival |
| Доверенная третья сторона | Trusted Third Party (TTP) | |
| Доверенный корневой центр сертификации | Trusted Root Certification Authority | Хранилище в Windows: Trusted Root Certification Authorities |
| Запрос на сертификат / Запрос на подпись сертификата | Certificate Signing Request (CSR) | Также: Certificate Request. Формат PKCS#10 |
| Идентификатор объекта | Object Identifier (OID) | Глобально уникальный идентификатор в формате ASN.1 (напр., 1.2.840.113549) |
| Имя субъекта | Subject Name / Common Name (CN) | CN -- часть Distinguished Name (DN) |
| Инфраструктура открытых ключей | Public Key Infrastructure (PKI) | Русская аббревиатура ИОК используется редко; в профессиональной среде говорят "PKI" |
| Использование ключа | Key Usage | Расширение сертификата X.509; задает допустимые операции (подпись, шифрование и т.д.) |
| Ключевая пара | Key Pair | Пара из открытого и закрытого ключей |
| Ключевой контейнер | Key Container / Private Key Container | Защищенное хранилище для закрытого ключа |
| Ключевой носитель | Token / Security Token / Key Carrier | В контексте PKI чаще используют token; key carrier -- буквальный перевод |
| Контроль доступа на основе ролей | Role-Based Access Control (RBAC) | |
| Корневой сертификат | Root Certificate | Самоподписанный сертификат корневого УЦ |
| Корневой центр сертификации | Root Certification Authority (Root CA) | Верхний уровень иерархии PKI; обычно офлайн |
| Криптопровайдер | Cryptographic Service Provider (CSP) | Термин Microsoft; в CNG заменен на Key Storage Provider (KSP). КриптоПро CSP -- российский криптопровайдер |
| Массовый выпуск | Batch Issuance / Mass Provisioning | Массовый выпуск смарт-карт или сертификатов |
| Модуль доверенной платформы | Trusted Platform Module (TPM) | Аппаратный чип; используется для виртуальных смарт-карт |
| Назначение сертификата / Расширенное использование ключа | Enhanced Key Usage (EKU) | Расширение X.509, определяющее конкретные сценарии применения |
| Неотказуемость / Неотрекаемость | Non-Repudiation | Невозможность отрицать факт подписания |
| Обнаружение сертификатов | Certificate Discovery | Автоматический поиск всех сертификатов в инфраструктуре |
| Область доступа информации о центре сертификации | Authority Information Access (AIA) | Расширение X.509, указывающее путь к сертификату издателя и OCSP-респондеру |
| Отзыв сертификата | Certificate Revocation | |
| Отпечаток сертификата | Certificate Thumbprint / Certificate Fingerprint | Thumbprint -- термин Microsoft; Fingerprint -- OpenSSL и другие |
| Открытый ключ | Public Key | |
| Перевыпуск ключей / Смена ключей | Re-Key / Certificate Re-Key | Выпуск нового сертификата с новой ключевой парой |
| Перекрестная сертификация | Cross-Certification | Установление доверия между двумя независимыми PKI |
| Персонализация смарт-карты | Smart Card Personalization | Запись сертификатов, ключей и данных на карту |
| ПИН-код | Personal Identification Number (PIN) | |
| Подпись кода | Code Signing | |
| Подчиненный центр сертификации | Subordinate CA | Синоним: Issuing CA (если выдает сертификаты конечным пользователям) |
| Подписант | Signer / Signatory | В юридическом контексте -- Signatory |
| Политика сертификатов | Certificate Policy (CP) | Документ, определяющий правила и требования PKI; RFC 3647 |
| Поставщик хранилища ключей | Key Storage Provider (KSP) | Заменяет CSP в Microsoft CNG API |
| Приостановка действия сертификата | Certificate Hold | Временная приостановка (reason code 6 в CRL); сертификат можно восстановить |
| Проверка подлинности сертификата / Валидация сертификата | Certificate Validation | Проверка цепочки доверия, сроков, отзыва и т.д. |
| Продление сертификата | Certificate Renewal | Выпуск нового сертификата взамен истекающего |
| Промежуточный центр сертификации | Intermediate CA / Policy CA | Policy CA -- если только выдает сертификаты другим ЦС |
| Протокол проверки статуса сертификата в реальном времени | Online Certificate Status Protocol (OCSP) | Альтернатива CRL для проверки отзыва в реальном времени |
| Разблокировка ПИН-кода | PIN Unlock / PIN Unblock | PUK -- PIN Unlock Key |
| Расширение сертификата | Certificate Extension | Дополнительные поля сертификата X.509 v3 |
| Регистрация сертификата | Certificate Enrollment | Весь процесс: от создания запроса до получения сертификата |
| Регламент удостоверяющего центра | Certification Practice Statement (CPS) | Публичный документ, описывающий практику работы УЦ; RFC 3647 |
| Самоподписанный сертификат | Self-Signed Certificate | Сертификат, подписанный собственным закрытым ключом |
| Серийный номер сертификата | Certificate Serial Number | Уникальный номер, присвоенный ЦС |
| Симметричное шифрование | Symmetric Encryption | |
| Система управления жизненным циклом сертификатов | Certificate Lifecycle Management (CLM) System | Основная категория продукта Indeed CM |
| Система управления смарт-картами | Smart Card Management System (SCMS / CMS) | CMS -- Card Management System |
| Служба веб-регистрации сертификатов | Certificate Enrollment Web Service (CES) | Компонент Microsoft AD CS |
| Служба подачи заявок на сертификаты через Интернет | Certificate Authority Web Enrollment (CAWE) | Компонент Microsoft AD CS |
| Служба регистрации сетевых устройств | Network Device Enrollment Service (NDES) | Реализация SCEP от Microsoft |
| Служба сертификатов Active Directory | Active Directory Certificate Services (AD CS) | Роль Windows Server |
| Смарт-карта | Smart Card | |
| Список доверенных сертификатов | Certificate Trust List (CTL) | |
| Список отозванных сертификатов (СОС) | Certificate Revocation List (CRL) | Русская аббревиатура СОС используется в ГОСТах; в практике чаще CRL |
| Средство криптографической защиты информации (СКЗИ) | Cryptographic Information Protection Facility / Cryptographic Tool | Устоявшегося перевода нет. Рекомендуется пояснение: "CIPF (a Russian regulatory term for certified cryptographic modules)" |
| Срок действия сертификата | Certificate Validity Period | |
| Токен | Token / Security Token | Аппаратный или программный носитель ключей |
| Точка распространения списка отзыва | CRL Distribution Point (CDP) | Расширение сертификата с URL для загрузки CRL |
| Удостоверяющий центр (УЦ) | Certification Authority (CA) | Юридический термин из 63-ФЗ. В техническом контексте = Центр сертификации |
| Управление жизненным циклом сертификатов | Certificate Lifecycle Management (CLM) | Включает обнаружение, выпуск, мониторинг, продление, отзыв |
| Хранилище сертификатов | Certificate Store | Windows Certificate Store: Personal, Trusted Root, Intermediate и др. |
| Хэш-функция / Хеш-функция | Hash Function / Hash Algorithm | SHA-256, SHA-384, ГОСТ Р 34.11 (Стрибог/Streebog) |
| Цепочка сертификатов / Цепочка доверия | Certificate Chain / Chain of Trust | Иерархия от конечного сертификата до корневого |
| Центр регистрации | Registration Authority (RA) | Проверяет личность заявителя перед выдачей сертификата |
| Центр сертификации (ЦС) | Certification Authority (CA) | Технический синоним "удостоверяющий центр" |
| Цифровой сертификат | Digital Certificate | Формат X.509 |
| Шаблон сертификата | Certificate Template | Термин Microsoft AD CS; определяет формат и содержимое сертификата |
| Шифрование файловой системы | Encrypting File System (EFS) | Компонент Windows, использующий сертификаты |
| Электронная подпись (ЭП) | Electronic Signature / Digital Signature | Electronic Signature -- юридический (eIDAS, 63-ФЗ); Digital Signature -- технический |
| Усиленная квалифицированная электронная подпись (УКЭП) | Qualified Electronic Signature (QES) | Термин eIDAS |
| Усиленная неквалифицированная электронная подпись | Advanced Electronic Signature (AES/AdES) | Термин eIDAS |

## Российская криптография

| Русский термин | Английский термин | Примечание |
|---|---|---|
| ГОСТ Р 34.10 | GOST R 34.10 | Стандарт цифровой подписи. Транслитерируется |
| ГОСТ Р 34.11 (Стрибог) | GOST R 34.11 (Streebog) | Хэш-функция. Streebog -- официальное латинское название |
| КриптоПро CSP | CryptoPro CSP | Имя собственное; не переводится |
| Кузнечик | Kuznyechik (GOST R 34.12) | Блочный шифр; транслитерация по RFC 7801 |

## Методические замечания

1. **УЦ vs ЦС**: "Удостоверяющий центр" -- юридический термин из 63-ФЗ, "Центр сертификации" -- технический. Оба переводятся как Certification Authority (CA).

2. **СКЗИ**: Не имеет точного англоязычного эквивалента. Регуляторный термин ФСБ России. При первом упоминании давать пояснение.

3. **Электронная подпись vs Цифровая подпись**: В российском законодательстве -- "электронная подпись" (Electronic Signature), что шире "цифровой подписи" (Digital Signature).

4. **Certificate Enrollment vs Certificate Issuance**: Enrollment -- весь процесс получения сертификата. Issuance -- только акт выдачи.

5. **Thumbprint vs Fingerprint**: Microsoft использует Thumbprint; OpenSSL -- Fingerprint. Оба означают хэш сертификата.

Thinking...
The user wants me to translate a technical Russian documentation article about Indeed CM wizard settings into English. The key requirements are:

1. Keep ALL markdown formatting including HTML tags like Tabs, TabItem, :::info etc. exactly as they are.
2. Translate EVERY part including notes and warnings.
3. Use standard PKI/security terminology: Certificate Authority (CA), private key, certificate revocation list (CRL), certificate enrollment, etc.

Let me break down what needs to be translated:

1. **Introduction** - About the Indeed CM Wizard settings tool
2. **Authentication Section** - How to get authentication codes and how to configure it across different platforms
3. **Settings Section** - Various configuration options including logs, certificate authorities, user catalog, etc.
4. **Access Control** - Authentication methods (Windows, OAuth/OpenID Connect), roles, database storage
5. **Database Storage** - SQL or PostgreSQL integration for users and certificates
6. **Encryption/Decryption** - Using the DataProtector utility to encrypt/de-encrypt configuration files on different platforms
7. **Card Monitor** - For managing and auditing device usage
8. **Confirmation** - Summary of what needs to be configured

I need to ensure:
- All TabItem labels are preserved
- All code blocks (tabs, details) are formatted correctly
- The :::info tag is used appropriately for warnings
- Standard PKI terms like CA, certificate revocation lists (CRL), private key, etc.

Let me construct the translation carefully following all formatting requirements. I'll preserve:
- All <TabItem> tags with values and labels
- All details content within :::details or :::info tags
- The entire article structure including code blocks

I'll now provide the translated English version with all HTML tags preserved as specified.
...done thinking.

---

# Master Setup Configuration for Indeed CM Services

The Wizard of Settings allows you to automatically configure Each Service configuration files.

## Installation and Authentication {#authentication}

The Wizard of Settings is an independent component and can be installed independently depending on the OS where Indeed CM is installed.

<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

1. Run the IndeedCM installer package file *IndeedCM.Wizard-{version}.exe-ru.msi* from the IndeedCM.WindowsServer directory and perform installation. The Wizard of Settings is placed in the path C:\inetpub\wwwroot\cm\wizard.
2. Obtain the authentication code. Launch IIS TrueCM Wizard app, the code will be stored in file `wizard_authentication_code.txt` in the path `C:\inetpub\wwwroot\cm\wizard\logs`.
3. Open the file `wizard_authentication_code.txt` and copy the authentication code.
4. Open the web browser and visit https://<IP address of TrueCM Server> / cm/wizard.
5. Enter the code in the **Authentication Code** field and click **Login**.

:::info
If you cannot obtain the authentication code through running the IndeedCM Wizard app, restart IIS service.
:::


</TabItem>
<TabItem value="linux" label="Linux (OC Linux)">

1. Install the Wizard of Settings.

 ```bash title="Debian"
 sudo dpkg -i cm.wizard-{version}_amd64.deb
 ```

 ```bash title="RHEL"
 sudo rpm -i cm.wizard-{version}.x86_64.rpm
 ```

2. Launch the bash script `start-cm-wizard.sh` located in the directory where the server's distribution is installed.

 ```
 sudo bash ./start-cm-wizard.sh
 ```

3. Obtain the authentication code. The authentication code is available when you run the startup script `start-cm-wizard.sh`.
3. Visit https://<IP address of TrueCM Server> / cm/wizard in your browser.
4. Enter the code in the **Authentication Code** field and click **Login**.

<details>
<summary>How to obtain more authentication codes</summary>

**Method 1.** Launch the service `cm-wizard.service`. The authentication code will be saved in file `wizard_authentication_code.txt` in the path */opt/indeed/cm/wizard/logs/ for your distribution.  
**Method 2.** Run `systemctl status`:

```bash
sudo systemctl status cm-wizard.service | grep AuthenticationCode
```

**Method 3.** Obtain authentication code from journal entry of service system:

```bash
sudo journalctl -u cm-wizard.service | grep AuthenticationCode
```

</details>


</TabItem>
<TabItem value="windows" label="Windows (OC Windows) default">

### Configuration and Administration {#configuration}

#### General Settings {#general-settings}

In the **General** section, select Console Administrator service settings.

### System Logs {#system-logs}

Configure journal log:
1. Specify the attribute by which user search in journal logs. The default value is CN (Common name).
2. Select option:
   - **Local Log**, to write logs from one or several TrueCM servers into a single Windows log.
   - **Log Server** to write logs of multiple TrueCM servers into a single Windows SysLog, database of Microsoft SQL or PostgreSQL.

<details>
    <summary>Use Local Log</summary>

Logs will be written in the local Windows log.

If several TrueCM Servers are deployed on different OS, then use Indeed CM Event Log Proxy to all servers write logs into a single Windows log:
1. Install and configure Indeed CM Event Log Proxy. [<u>Indeed CM Event Log Proxy Installation</u>](server/event-log.md#event-log-proxy)
2. Enable option **Enable Event Log Proxy**.
3. Specify the URL connection to Event Log Proxy. For example, `https://server.domain.loc/cm/eventlogproxy`.
4. If server TrueCM is installed on Windows OS, enter username account with rights to access the unified log of events (from file `appsettings.json` Application Event Log Proxy).  
   If server TrueCM is installed on Linux OS, fill in the **Certificate** field in **Client** attribute for Event Log Proxy from client certificate that presents server TrueCM for connection to Event Log Proxy (from parameter `allowedCertificateThumbprints` of `appsettings.json` application Event Log Proxy).

</details>
<details>
    <summary>Use Log Server</summary>

If you deploy several TrueCM Servers in your environment, then use the Indeed Log Server application to all TrueCM servers write logs into a single Windows SysLog, database of Microsoft SQL or PostgreSQL.
1. Install and configure the application Indeed Log Server. [<u>Indeed Log Server Installation</u>](server/event-log.md#log-server)
2. Specify URL connection to Indeed Log Server. For example, `https://server.domain.loc/ls/api` for Windows OS, `https://server.domain.loc/api` for Linux OS.

</details>

### Certificate Authority Settings {#certificate-authority}

Configure integration with trusted certificate authorities:
- Microsoft Enterprise CA
- Aladdin Enterprise CA
- SafeTech CA
- CryptoPro 2.0 Trust Center
- CryptoPro DSS
- Validatator Trust Center (VTC)

For CryptoPro 2.0, there is an option **Publish User Certificates in Certificate Registry**. Specify the URL connection to the application of the Certificate Registry.

If you need to specify information about the location of users, use the certificate center for the registration:
1. Click **Add**.
2. Enter name Center that displays in Console of Trusted Certification Centers in **Trust Center**.
3. In the field **ID of folder** identify of the user ID directory, the identifier is displayed in the Center of Trusted Certification Centers in column **ID**.

### AirCard Enterprise Integration {#aircard}

Configure integration with Indeed AirCard Enterprise:
1. Enable option **Enable integration with Indeed AirCard Enterprise**.
2. Specify URL connection to server AirCard Enterprise for example, `https://aircard.domain.loc:3002`. Ensure that the specified port is open for incoming connections on the AirCard server.
3. Specify client certificate to establish secure connection between TrueCM server and server AirCard Enterprise.
4. Specify existence time of unregistered smart cards AirCard (in seconds). The default value – 120 seconds.

[Learn more in Indeed AirCard Enterprise documentation](https://docs.indeed-company.ru/aircard-enterprise/2.0/intro/)

### Client Agent {#client-agent}

Configure agent settings of Indeed CM:
1. Install and configure indeed CM Agent. [Installation Instructions for Indeed CM Agent](server/client-agent.md)
1. Enable option **Allow usage of client agents**.
2. Select detection method for agents in domain and not in domain for registration in TrueCM:
   - Not specified. The default value.
   - Use MachineGuid as workstation identifier.
   - Generate new GUID. Select this option if several workstations have the same MachineGuid value.
   - Use Domain SID of computer.
   - Use Computer SID. Select this option, if the agent is installed on not-domain workstation. And the ID of Agent is assigned a string Value `MachineGuid` from the branch `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\` workstation.

<details>
    <summary>Moving to changing strategy for generating agent identifier after initial configuration</summary>

To change strategy for generating identifier of agent after initial configuration TrueCM:
1. Stop services agents `agentregistrationapi` and `agentserviceapi` on server TrueCM.
2. Remove all clients in section **Agents** Console or perform query in database TrueCM to remove registered agents and their sessions.
3. Apply changes in Wizard and spread the modified file of config service `agentregistrationapi` to server TrueCM.
4. Launch services agents `agentregistrationapi` and `agentserviceapi`.

</details>

5. To register without administrator confirmation, enable option **Automatic Agent Registration**. After installation and configuration agent will be displayed in section **Agents** Console TrueCM with status *Registered*.
6. Load certificate of the agent – file root of the service agent certificate with closed key in format JSON `agent_root_ca.json`.
7. Select the **Event logging level of agents** dropdown to indicate which events the agents appear in the system logs – all, only errors, only warnings and errors.
8. Fill in fields **Periodicity of getting data from server** and **Frequency of execution of deferred task**.
9. Header HTTP request identifier for certificate agent is specified by default. If Indeed CM is used with load balancing, enable option **Only send 'Subj' attribute value of the certificate agent in HTTP request headers** to reduce traffic.

</details>

## User Catalog {#user-catalog}

Configure connection to user catalog. You can use several user catalogs.

[How to create user catalog](/environment/users-catalog/users-catalog.md)

### LDAP Catalog {#ldap}

Click **Add** and select the type of user catalog: Active Directory, Samba AD DC, FreeIPA or ALD Pro.

#### Active Directory {#active-directory}

1. Specify username with account which has rights to access user catalog: name in format DOMAIN\UserName or UserName@DNSDomainName and password.
2. Specify NetBIOS-domain name and DNS-domain name or domain controller name.

 ::- tip How to find DNS-domain name and NetBIOS-domain name
 Run in command prompt `set USERDNSDOMAIN`, to obtain DNS-domain name.  
 `set USERDOMAIN`, to obtain NetBIOS-domain name.
 :::

4. Specify path of folder with users in the format Distinguished Name. For working with all users select root domain.
5. If you use LDAPS for access to user catalogs, enable option **Use LDAPS**.
6. To display a photograph of a user in the Indeed CM interface or on smart card, select attribute which contains photograph of user.
7. Click **Save**.

#### Samba AD DC {#samba-ad}

1. Specify username with account which has rights to access user catalog: name in format DOMAIN\UserName or UserName@DNSDomainName and password.
2. Specify NetBIOS-domain name and DNS-domain name or domain controller name.

 ::- tip How to find DNS-domain name and NetBIOS-domain name
 Run in command prompt `set USERDNSDOMAIN`, to obtain DNS-domain name.  
 `set USERDOMAIN`, to obtain NetBIOS-domain name.
 :::

4. Specify path of folder with users in the format Distinguished Name. For working with all users select root domain.
5. If you use LDAPS for access to user catalogs, enable option **Use LDAPS**.
6. To display a photograph of a user in the Indeed CM interface or on smart card, select attribute which contains photograph of user.
7. Click **Save**.

:::caution For existing configuration of TrueCM
If TrueCM was configured previously for connection to user catalogs in Active Directory, and domain controller was reconfigured from Active Directory to Samba AD DC, then you should not change the configuration parameters of user catalog.
:::


#### Red Domain Admin {#red-domain-admin}

1. Specify username with account which has rights to access user catalog: name in format DOMAIN\UserName or UserName@DNSDomainName and password.
2. Specify NetBIOS-domain name and DNS-domain name or domain controller name.

 ::- tip How to find DNS-domain name and NetBIOS-domain name
 Run in command prompt `set USERDNSDOMAIN`, to obtain DNS-domain name.  
 `set USERDOMAIN`, to obtain NetBIOS-domain name.
 :::

4. Specify path of folder with users in the format Distinguished Name. For working with all users select root domain.
5. If you use LDAPS for access to user catalogs, enable option **Use LDAPS**.
6. To display a photograph of a user in the Indeed CM interface or on smart card, select attribute which contains photograph of user.
7. Click **Save**.

:::caution For existing configuration of TrueCM
If TrueCM was previously configured for connection to user catalogs in Active Directory, and domain controller was reconfigured from Active Directory to RED Domain Admin, then you should not change the configuration parameters of user catalog.
:::


#### FreeIPA {#freeipa}

1. Specify username with account which has rights to access user catalog: name in format Distinguished Name and password.
2. Specify NetBIOS-domain name and DNS-domain name or domain controller name.

 ::- tip How to find DNS-domain name and NetBIOS-domain name
 Run in command prompt `set USERDNSDOMAIN`, to obtain DNS-domain name.  
 `set USERDOMAIN`, to obtain NetBIOS-domain name.
 :::

4. Specify path of folder with users in the format Distinguished Name. We recommend specifying root domain or accounts catalog.
5. If you use LDAPS for access to user catalogs, enable option **Use LDAPS**.
6. Click **Save**.

#### ALD Pro {#ald-pro}

1. Specify username with account which has rights to access user catalog: name in format Distinguished Name and password.
2. Specify NetBIOS-domain name and DNS-domain name or domain controller name.

 ::- tip How to find DNS-domain name and NetBIOS-domain name
 Run in command prompt `set USERDNSDOMAIN`, to obtain DNS-domain name.  
 `set USERDOMAIN`, to obtain NetBIOS-domain name.
 :::

4. Specify path of folder with users in the format Distinguished Name. We recommend specifying root domain or accounts catalog.
5. If you use LDAPS for access to user catalogs, enable option **Use LDAPS**.
6. Click **Save**.

</Tabs>


#### CryptoPro {#cryptopro}

1. Click **Add**.
2. In dropdown select attribute name of user that determines its uniqueness when authentication in TrueCM web applications:
   - **E-mail**
   - **Common Name**
   - **User Principal Name**
   - **User**. Enter OID attribute name of user.
3. Select integration API with user catalog CryptoPro 2.0 Trust Center: REST or SOAP.
4. Specify client certificate of service account, which will be used for connection to CryptoPro 2.0 Trust Center for viewing list of users.
5. Specify URL connection to Certificate Registry. For example, `https://cryptopro.domain.loc/RA/RegAuthLegacyService.svc`.
6. Click **Save**.


#### Internal Catalog {#internal-catalog}

As an internal user catalog use Microsoft SQL or PostgreSQL database.
1. Click **Add**.
2. Select storage type.
3. Configure connection to the storage. Specify username, machine instance (for Microsoft SQL), port number and database name.
4. Select authentication method for connection to server:
   - Microsoft SQL: authentication Windows or SQL Server. To connect SQL Server enter user name and password.
   - PostgreSQL: enter user name and password.
5. Click **Save**.


### Additional User Attributes {#user-catalog-add-attributes}

To configure additional attributes of internal user catalog:
1. Click **Add**.
2. Specify attribute name in the catalogs and displayable attribute name.
3. To be visible when creating/editing a user in TrueCM, enable option **Visible when creating and editing a user**.
4. To make attribute mandatory for entry creation or edit on TrueCM, enable option **Must be entered for creation**.
5. Select attribute type:
- **Text**  
Specify the following settings:
  - maximum length text – maximum number of characters.
  - format of text – regular expression, with which will be checked correct nature of text attributes value. For example, check the correctness of entering surnames, for example in allowed Russian letters, space and dash: `^[А-ЯЁ][а-яё]{0,30}(( |)([а-яё]{0,30})){0,2}$`.
  - message about incorrect format – text message that will be displayed when inputting text value that does not correspond to the requirements of regular expression.
- **Integer**  
Specify minimum and maximum value. For example, for entering information about age.
- **Logical**  
Attribute can take values `true` or `false`.
- **Lookup table values**  
Specify a lookup table which will be used when choosing attribute values. Format: `<value attribute#1>, <displayable attribute#1>; <value attribute#2>, <displayable attribute#2>;...`. For example, `red, Red color; green, Green color`.
6. Click **Save**.


</Tabs>

### Attribute Matching {#user-catalog-link-attributes}

You can configure matching between attributes from Trusted Certification Center and user attributes in the catalog.

If you are configured attributes, you can register a new user when releasing device for this user in TrueCM.

### Updateable Attributes {#user-catalog-update-attributes}

You can configure list of user attributes Active Directory, when changing which is necessary to update certificate on device.

Changes can be monitored only for attributes from Subject (Subject) and **User Alternative Name** (SAN) certificate.

:::info
In parameters of Microsoft CA and CryptoPro 2.0 default values are monitored attributes General name, E-mail and UPN username.
:::

To monitor an attribute:
1. Click **Add**.
2. Specify attribute name in user catalog.
3. Specify displayable attribute name.
4. Specify OID or X.500 attribute name in certificate. According to the identified value search attributes in certificate.
5. Click **Save**.


## Access Control {#access-control}

Select authentication method for access to Indeed CM services:
- **Windows Authentication**  
This option allows authenticating through user credentials of a Windows OS and is used for installation of TrueCM on domain workstation under OS Windows.

- **OpenID Connect**  
This option allows authenticating through OpenID server TrueCM and is used for installation of TrueCM on domain or not-domain workstation under OS Windows or Linux.

:::caution
Ensure you selected that authentication method when installing the TrueCM server on OS Windows.
:::


### OAuth/ OpenID Connect Authentication {#oauth-oidc}

1. Specify the following settings:
   - URL connection to [TrueCM OpenID Server](server/openid-connect.md).
   - Complete domain name (FQDN) of the TrueCM server. For configuration with several servers, specify their complete domain names using comma.
   - Certificate signatory certificate.
2. Generate client certificates if necessary.


## Roles {#roles}

Administrator roles are user accounts with rights to manage [roles](admin-guide/configuration/roles.md) in TrueCM.

Specify username in the format DOMAIN\UserName or UserName@DNSDomainName. When first start is login in TrueCM console account as specified user login.

:::caution
Ensure that the administrator of roles user account is included in the user catalog.
:::


## Data Storage {#database}

Configure connection to the database storage. [How to create data storage](/environment/data-storage.md)

1. Select storage type depending on environment where TrueCM deployed: Microsoft SQL or PostgreSQL.
2. Configure connection to the storage. Specify username, instance (for Microsoft SQL), port number and database name.
3. Select authentication method for connection to server:
   - Microsoft SQL: authentication Windows or SQL Server. For connection SQL Server enter user name and password.
   - PostgreSQL: enter user name and password.
4. Configure additional parameters:
   - minimum size of pool
   - maximum size of pool
   - wait time before connection
   - life time of connection
   - number of connections to repeat
   - interval of connection repetition


### Database Encryption {#database-encryption}

Data TrueCM is stored and sent in encrypted form. In the dropdown select encryption algorithm and generate it. Save backup of the encryption key.

:::caution
Create backup of the key. This will allow access to encrypted data when recovering or if main key is lost or damaged. Copy of key can be saved with [encryption copy of TrueCM](#results).
:::


#### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption files configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\TrueCM CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\TrueCM CM\CardMonitor\appsettings.json"
  ```

</Tabs>


#### Decryption on Linux {#encryption-unprotect-linux}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Open Linux Bash.
3. Execute one or more of commands:
  - encryption all configuration files that are located in standard directories (*/opt/indeed/cm/<component>/appsettings.json*):

 ```bash
 dotnet Cm.Config.DataProtector.dll protect
 ```
  - encryption file configuration files of individual components:

  ```bash
  dotnet Cm.Config.DataProtector.dll protect --app <component name>
  ```

  ```bash title="Example command"
  dotnet Cm.Config.DataProtector.dll protect --app ManagementConsole
  ```

<details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption decryption file configuration outside standard directory:

  ```bash
  dotnet Cm.Config.DataProtector.dll protect --app <component name> --file "path to file appsettings.json"
  ```

  ```bash title="Example command"
  dotnet Cm.Config.DataProtector.dll protect --app ManagementConsole --file "/opt/indeed/cm/mc/appsettings.json"
  ```

</TabItem>


## Card Monitor {#card-monitor}

Define settings for the Card Monitor service for auditing device usage.

<details>
    <summary>Learn more about operation of the TrueCM Card Monitor</summary>

CardMonitor is installed with the server Indeed CM and performs the following operations:
- retrieval and withdrawal of user devices, account which is removed from user catalog
- withdrawal temporary devices with expiration time expired
- disable device users, account which was switched off
- removal accounts from user catalog, account which was switched off
- installation or reset status content of device
- record event *Long absence connection agent* in journal logs
- remove agents that are inactive for period of time to set
- email notifications administrators and users on the following events:
    - expiration of certificate of users who are stored on devices
    - approval/rejection release of device
    - approval/rejection update certificates on device
    - approval/rejection replacement devices
    - change policy that applies to a user

</details>

1. Specify the administrator account, for which will be started card monitor service, in the format DOMAIN\UserName or UserName@DNSDomainName. Requirements:
    - included in user catalog TrueCM
    - is a group of Administrators (Administrators) on the server TrueCM
    - has permission to **Log on as a batch job** in Active Directory policy.
2. Configure when service will be started.
3. In the section **User operations** you can set the following:
   - **Disable devices for disabled users**. CardMonitor will disable device users, account which was switched off in user catalog. If in template parameters of certificates to be released or switch off device additional option **Withdraw certificate upon withdrawal or disable of device**, then the expiration of certificates on devices will be paused in TrueCM, and certificates will be withdrawn.
   - **Filter disabled users as removed**. Accounts that are disabled by condition filter is considered removed from user catalog. Devices for removed users withdraw.  
   Specify attribute username and value. For example, the Distinguished Name with value `OU=Fired users,DC=domain,DC=loc`.
   - **Withdrew devices of removed users**. Devices withdrawn from remote users are extracted and transition to state *Empty*. When extraction device does not clean up.
4. In section **Agents** you can set the following:
   - **Record event in journal if agent inactive for longer than (minutes)**. When absence connection agent with the server TrueCM records this event in the system log after the specified period of time.
   - **Remove agent if agent inactive for more than (days)**. When absence connection agent with the server TrueCM removes agent from database after the specified period of time.

:::info 

For operation of the Card Monitor service requires a separate services role. [Learn more about the role for the operation of Card Monitor](/admin-guide/configuration/roles.md#card-monitor)
:::


## Confirmation {#confirm}

1. Verify settings of all Wizard sections.
2. Click **Apply**.

All configured parameters are saved in application config files and are stored in *C:\inetpub\wwwroot\cm\wizard*\configs for Windows OS and */opt/indeed/cm/wizard/configs/* for Linux OS. The configuration files need to be [applied on the TrueCM server](#configure).

## Results {#results}

Enable option **Save file configuration** to export configurations in archive.

If you install TrueCM first time, we recommend saving a copy of configured parameters. Enable option **Save backup of configuration parameters** and specify password from file.

Backup set includes all parameters specified when installation for all services, as well as encryption algorithm and key hash of the database. Store the file backup in a protected location.

## Backup Restore {#backup}

You can restore settings of configuration from backup if you need:
- update server TrueCM
- move server to new workstation
- install additional servers

To restore configuration from file:
1. Navigate to Wizard **Restore Settings**.
2. Click **Restore parameters of configuration from backup**.
3. Upload file.
4. If the backup was encrypted, enter password.

## Apply Configuration Files {#configure}

Apply files configured by the Wizard of Settings on the server TrueCM.

<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

1. Open PowerShell as administrator account from your computer.
2. Navigate to directory `C:\inetpub\wwwroot\cm\wizard\configs`.
3. Run PowerShell script `deploy_configuration.ps1`:

```
.\deploy_configuration.ps1
```
4. During execution PowerShell script specify password the service account being used for running the card monitor service.

:::tip
It is recommended to specify local user account, with which other web applications TrueCM are launched.
:::

TrueCM configuration files of all services TrueCM are located in the root of the web application folder IIS at path `C:\inetpub\wwwroot\cm`. Files of card monitor service are located in the directory `%ProgramFiles%\Indeed CM\CardMonitor`.


</TabItem>
<TabItem value="linux" label="Linux (OC Linux)">

1. Open emulator terminal.
2. Navigate to path `*/opt/indeed/cm/wizard/configs*.`
3. Ensure that script file has execution permissions, and run bash script `deploy_configuration.sh`:

```bash
sh ./deploy_configuration.sh
```

4. During execution bash script specify account being used for running the card monitor service.

:::tip
It is recommended to specify local user account, with which other web applications TrueCM are launched.
:::

If in the infrastructure deployed multiple TrueCM Servers, apply configuration files on each server. Configuration files of all services TrueCM are located in the path `*/opt/indeed/cm*.`

</TabItem>
</Tabs>

## Encryption/Decryption Files {#encryption}

To ensure security, it is recommended to encrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Unencryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>
<TabItem value="linux" label="Linux (OC Linux)">

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Open Linux Bash.
3. Execute one or more of commands:
  - encryption all configuration files that are located in standard directories (*/opt/indeed/cm/<component>/appsettings.json*):

 ```bash
 dotnet Cm.Config.DataProtector.dll protect
 ```
  - encryption file configuration files of individual components:

  ```bash
  dotnet Cm.Config.DataProtector.dll protect --app <component name>
  ```

  ```bash title="Example command"
  dotnet Cm.Config.DataProtector.dll protect --app ManagementConsole
  ```

<details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption decryption file configuration outside standard directory:

  ```bash
  dotnet Cm.Config.DataProtector.dll protect --app <component name> --file "path to file appsettings.json"
  ```

  ```bash title="Example command"
  dotnet Cm.Config.DataProtector.dll protect --app ManagementConsole --file "/opt/indeed/cm/mc/appsettings.json"
  ```

</TabItem>


## Stop the Wizard of Settings {#stop}

To ensure security, it is recommended to disable TrueCM Wizard after the configuration process.

<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

1. Open IIS Services Manager (Internet Information Services Manager) and in the left menu select **IIS Application Pools** (Application pools).
2. Select TrueCM Wizard application and in the right menu click **Stop**.

</TabItem>
<TabItem value="linux" label="Linux (OC Linux)">

1. Open emulator terminal.
2. Run command: 
```bash
sudo systemctl stop cm-wizard.service
```

</TabItem>
</Tabs>

## Application Configuration Files {#config-file}

Configure configuration files of all services TrueCM by the Wizard of Settings for application configuration on server TrueCM.

<details>
    <summary>See the full list of TrueCM Configuration Files for the Wizard of Settings.</summary>

TrueCM configuration files are in the following locations:

- **Windows OS:** `C:\inetpub\wwwroot\cm`
- **Linux OS:** */opt/indeed/cm/.*

</details>

## Application Configuration File Application {#config-file-app}

For each component of TrueCM, it is recommended to apply the configuration files created by the Wizard of Settings to the server.

<details>
    <summary>How to Apply the Configuration Files</summary>

To apply the configuration files on the TrueCM server:

1. Navigate to the path of the folder that contains all TrueCM configuration file, which is `C:\inetpub\wwwroot\cm`.
2. Open PowerShell as administrator account from your computer.
3. Run PowerShell script `deploy_configuration.ps1`.
4. During execution PowerShell script specify password the service account being used for running the card monitor service.

</details>

### File Locations

- **TrueCM Server** configuration files are located in the path `%SystemDrive%\inetpub\wwwroot\cm`. Files of card monitor service are located in `C:\ProgramFiles\Indeed CM\CardMonitor`.

<details>
    <summary>How to Apply the Configuration Files on Several TrueCM Servers</summary>

To apply the configuration files on multiple TrueCM servers:

1. Navigate to the path of the folder that contains all TrueCM configuration file, which is `C:\inetpub\wwwroot\cm`.
2. Open PowerShell as administrator account from your computer.
3. Run PowerShell script `deploy_configuration.ps1` for each server.
4. During execution PowerShell script specify password the service account being used for running the card monitor service.

</details>

## Encryption/Decryption Files {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration Files {#config-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Apply Configuration File to the TrueCM Server {#configure-app}

Apply configuration file to the server TrueCM created by the Wizard of Settings.

<details>
    <summary>How to Apply the Configuration Files</summary>

To apply the configuration files on the TrueCM server:

1. Navigate to the path of the folder that contains all TrueCM configuration file, which is `C:\inetpub\wwwroot\cm`.
2. Open PowerShell as administrator account from your computer.
3. Run PowerShell script `deploy_configuration.ps1`.
4. During execution PowerShell script specify password the service account being used for running the card monitor service.

</details>

## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Encryption/Decryption File {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Encryption/Decryption File {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Encryption/Decryption File {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Encryption/Decryption File {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Encryption/Decryption File {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Encryption/Decryption File {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Encryption/Decryption File {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Encryption/Decryption File {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Encryption/Decryption File {#encryption-file}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


## Application Configuration File Application {#config-file-app}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- decryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>


### Linux {#encryption-unprotect-linux}

To ensure security, it is recommended to encrypt and decrypt files configuration applications Indeed CM with a utility Cm.Config.DataProtector. The utility supports AES encryption algorithm with effective key length 256 bits. Key for encryption is kept on TrueCM server.

Key for encryption is at the path:
- Windows OS: `C:\ProgramData\Indeed\cm\keys`
- Linux OS: `*/etc/indeed/cm/keys*.`

:::caution
Create backup of the key for encryption. This will allow access to encrypted data in case of lost or damaged primary key. Backup of the key can be saved with copy of TrueCM configuration.
:::


<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows (OC Windows)" default>

### Encryption {#encryption-protect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - encrypt all configuration files that are located in standard directory (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardCleaner – AirCardCleaner
    - Agent registration API – AgentRegistrationApi
    - Agent service API – AgentServiceApi
    - TrueCM server OpenID Connect – Oidc

 </details>

- encryption file configuration outside standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to file appsettings.json"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to disk from distribution server of TrueCM in path *Misc\dataprotector*.
2. Run PowerShell as administrator account.
3. Execute one or more of commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decryption file configuration files of individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Names of Components TrueCM</summary>

    - Console administrator – ManagementConsole
    - SelfService – SelfService
    - CardMonitor – CardMonitor
    - Device unlock and disable – CredentialProvider
    - Remote service – RemoteService
    - API service – Api
    - AirCardClean
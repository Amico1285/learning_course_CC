---
title: Setup Wizard
description: Configuring Indeed CM service configuration files in the Setup Wizard
sidebar_position: 2
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

The Setup Wizard allows you to automatically populate configuration files for each Indeed CM service.

## Installation and authentication {#authentication}

The Setup Wizard is an independent component and is installed separately. Choose the instructions depending on the OS where the Indeed CM Server is installed.

<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows OS" default>

1. Run the *IndeedCM.Wizard-&lt;version number&gt;.x64.ru-ru.msi* file from the *IndeedCM.WindowsServer* directory of the Indeed CM distribution package and complete the installation. The Setup Wizard is installed in the *C:\inetpub\wwwroot\cm\wizard* directory.
2. Obtain the authentication code. Start the IIS application pool IndeedCM Wizard; the code will be saved to the *wizard\_authentication\_code.txt* file in the *C:\inetpub\wwwroot\cm\wizard\logs* directory.
3. Open the *wizard\_authentication\_code.txt* file and copy the authentication code.
4. Open a browser and navigate to *https://&lt;Indeed CM Server FQDN&gt;/cm/wizard*.
5. Enter the code in the **Authentication code** field and click **Log in**.

:::info
If you were unable to obtain the authentication code by starting the IndeedCM Wizard application pool, restart the IIS service.
:::


</TabItem>
  <TabItem value="linux" label="Linux OS">

1. Install the Setup Wizard.

 ```bash title="Debian"
 sudo dpkg -i cm.wizard-<version number>_amd64.deb
 ```

 ```bash title="RHEL"
 sudo rpm -i cm.wizard-<version number>.x86_64.rpm
 ```

2. Run the bash script *start-cm-wizard.sh* located in the directory with the Indeed CM Server distribution package.

 ```
 sudo bash ./start-cm-wizard.sh
 ```

3. Obtain the authentication code. The authentication code is available in the output of the *start-cm-wizard.sh* script startup.
3. Open a browser and navigate to `https://&lt;Indeed CM Server FQDN&gt;/cm/wizard`.
4. Enter the code in the **Authentication code** field and click **Log in**.

<details>
<summary>Other ways to obtain the authentication code</summary>

**Method 1.** Start the cm-wizard.service service. The code will be saved to the *wizard\_authentication\_code.txt* file in the */opt/indeed/cm/wizard/logs* directory.
**Method 2.** Run the `systemctl status` command:

```bash
sudo systemctl status cm-wizard.service | grep AuthenticationCode
```

**Method 3.** Obtain the code from the systemd application log of the cm-wizard.service unit using the command:

```bash
sudo journalctl -u cm-wizard.service | grep AuthenticationCode
```

The authentication code is displayed on the terminal screen.

</details>


</TabItem>
</Tabs>

## System features {#settings}

In the **General features** section, select the settings for the Management Console and the Self-Service Portal.

### Event log {#settings-log}

Configure the event log settings:
1. Specify the attribute by which users are searched in the event log. Default value: CN (Common Name).
2. Select an option:
- **Use local Windows event log** to write events from one or more servers to a single Windows event log.
- **Use Log Server** to write events from multiple Indeed CM Servers to a single Windows event log, SysLog, Microsoft SQL database, or PostgreSQL database.

<details>
    <summary>Use local Windows event log</summary>

Events will be written to the local Windows event log.

If multiple Indeed CM Servers are deployed in the infrastructure, use the Indeed CM Event Log Proxy component so that all servers write events to a single Windows event log:
1. Install and configure the Indeed CM Event Log Proxy application. [<u>Indeed CM Event Log Proxy installation guide</u>](server/event-log.md#event-log-proxy)
2. Enable the **Enable Event Log Proxy** option.
3. Specify the connection URL for Event Log Proxy. For example, `https://server.domain.loc/cm/eventlogproxy`.
4. If the Indeed CM Server is installed on Windows OS, enter the credentials of an account with access rights to the unified event log (from the `authorization` section of the Event Log Proxy *Web.config* file).
   If the Indeed CM Server is installed on Linux OS, in the **Certificate thumbprint** field, specify the thumbprint of the client certificate that the Indeed CM Server presents when connecting to Event Log Proxy (from the `allowedCertificateThumbprints` parameter of the Event Log Proxy *appsettings.json* file).

</details>
<details>
    <summary>Use Log Server</summary>

If multiple Indeed CM Servers are deployed in the infrastructure, use the Indeed Log Server application so that all servers write events to a single Windows event log, SysLog, Microsoft SQL database, or PostgreSQL database.
1. Install and configure the Indeed Log Server application. [<u>Indeed Log Server installation guide</u>](server/event-log.md#log-server)
2. Specify the connection URL for Indeed Log Server. For example, `https://server.domain.loc/ls/api` for Windows OS, `https://server.domain.loc/api` for Linux OS.

</details>

### CIPF accounting log {#settings-skzi}

If your organization maintains CIPF records, enable the **Maintain CIPF accounting log** option.

If necessary, specify additional attributes for the fields that will be displayed in the CIPF accounting log.

### Certification Authorities {#settings-ca}

Configure the integration with Certification Authorities:
- Microsoft Enterprise CA
- Aladdin Enterprise CA
- SafeTech CA
- CryptoPro CA 2.0
- CryptoPro DSS
- Validata CA

For CryptoPro CA 2.0, the **Publish CryptoPro CA 2.0 user certificates to the CFT application database** option is available. Specify the connection string to the CFT application database.

If necessary, specify information about user locations in the Registration Center:
1. Click **Add**.
2. Enter the CA name that is displayed in the Registration Center Management Console in the **Certification Authorities** section.
3. Enter the folder identifier. The identifier is displayed in the Registration Center Management Console in the **Folder identifier** column.

### AirCard Enterprise {#settings-aircard}

Configure the integration with Indeed AirCard Enterprise:
1. Enable the **Enable integration with Indeed AirCard Enterprise** option.
2. Enter the connection URL for the AirCard Enterprise server, for example, `https://aircard.domain.loc:3002`. Make sure the specified port is open for incoming connections on the AirCard server.
3. Specify the client certificate thumbprint to establish a secure connection between the Indeed CM Server and the AirCard Enterprise server.
4. Specify the lifetime of unregistered AirCard smart cards (in seconds). After the specified time expires, the Card Monitor service will automatically delete unregistered AirCard smart cards. Default value: 120 seconds.

[Learn more in the Indeed AirCard Enterprise documentation](https://docs.indeed-company.ru/aircard-enterprise/2.0/intro/)

### Client agent {#settings-agent}

Configure the Indeed CM client agent settings:
1. Install and configure the Indeed CM Agent component. [Indeed CM Agent installation guide](server/client-agent.md)
1. Enable the **Allow use of client agents** option.
2. Select the agent identification method in the domain and outside the domain for registration in Indeed CM:
    - **Not set**. Default value.
    - **Use machine GUID**. Use the `MachineGuid` value of the workstation.
    - **Generate new GUID**. Select this option if multiple workstations share the same `MachineGuid` value.
    - **Use domain computer SID**.
    - **Use computer SID**. Select this option if the agent is installed on a non-domain workstation. The agent identifier is assigned the string value of `MachineGuid` from the *\[HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Cryptography\]* registry key of the workstation.

    <details>
    <summary>Changing the agent identifier generation strategy</summary>

    To change the agent identifier generation strategy after the initial Indeed CM configuration:
    1. Stop the agent services `agentregistrationapi` and `agentserviceapi` on the Indeed CM Server.
    2. Delete all client agents in the **Agents** section of the Management Console or execute a query to the Indeed CM database to delete registered agents and their sessions.
    3. Apply the changes in the Setup Wizard and distribute the updated configuration file for the `agentregistrationapi` service on the Indeed CM Server.
    4. Start the agent services `agentregistrationapi` and `agentserviceapi`.

    </details>

3. To register agents without administrator approval, enable the **Automatic Agent Registration** option. After the agent is installed and configured on a workstation, it will appear in the **Agents** section of the Indeed CM Management Console with the *Registered* status.
5. Upload the agent certificate -- the root certificate file for agent services with the private key in JSON format *agent\_root\_ca.json*.
6. In the **Agent event logging level** drop-down list, select which agent events are recorded in the event log -- all, errors only, or warnings and errors only.
7. Fill in the **Data retrieval frequency from server** and **Retry interval for user-canceled tasks** fields.
8. The HTTP request header name for the certificate is set by default. If Indeed CM is used with a load balancer, enable the **Send only the 'Subject' field of the agent certificate in HTTP request headers** option to reduce traffic.

## User directory {#user-catalog}

Configure the connection to the Indeed CM user directory. You can use multiple user directories.

[How to create a user directory](/environment/users-catalog/users-catalog.md)

<Tabs queryString="catalog">
  <TabItem value="ldap" label="LDAP" default>

Click **Add** and select the user directory type: Active Directory, Samba AD DC, FreeIPA, or ALD Pro.

<Tabs queryString="ldap-type">
  <TabItem value="ad" label="Active Directory" default>

1. Specify the credentials of an account with access rights to the user directory: name in the format DOMAIN\UserName or UserName@DNSDomainName and password.
2. Specify the domain NetBIOS name and the DNS name of the domain or domain controller.

 :::tip how to find the DNS name and NetBIOS name of the domain
 Run in the command line:

 `set USERDNSDOMAIN` to find out the DNS name of the domain.
 `set USERDOMAIN` to find out the NetBIOS name of the domain.
 :::

4. Specify the path to the container with users in Distinguished Name format. To work with all users, select the domain root.
5. If you use the LDAPS protocol to access directories, enable the **Use LDAPS** option.
6. To display a user's photo in the Indeed CM interface or print it on a smart card, select the attribute that contains the user's photo.
7. Click **Save**.


  </TabItem>
  <TabItem value="samba" label="Samba AD DC">

1. Specify the credentials of an account with access rights to the user directory: name in the format DOMAIN\UserName or UserName@DNSDomainName and password.
2. Specify the domain NetBIOS name and the DNS name of the domain or domain controller.

 :::tip how to find the DNS name and NetBIOS name of the domain
 Run in the command line:

 `set USERDNSDOMAIN` to find out the DNS name of the domain.
 `set USERDOMAIN` to find out the NetBIOS name of the domain.
 :::

4. Specify the path to the container with users in Distinguished Name format. To work with all users, select the domain root.
5. If you use the LDAPS protocol to access directories, enable the **Use LDAPS** option.
6. To display a user's photo in the Indeed CM interface or print it on a smart card, select the attribute that contains the user's photo.
7. Click **Save**.

:::caution For an existing Indeed CM configuration
If Indeed CM was previously configured to work with a user directory in Active Directory, and the domain controller was reconfigured from Active Directory to Samba AD DC, you do not need to change the user directory configuration parameters.
:::


  </TabItem>
  <TabItem value="red" label="RED ADM">

1. Specify the credentials of an account with access rights to the user directory: name in the format DOMAIN\UserName or UserName@DNSDomainName and password.
2. Specify the domain NetBIOS name and the DNS name of the domain or domain controller.

 :::tip how to find the DNS name and NetBIOS name of the domain
 Run in the command line:

 `set USERDNSDOMAIN` to find out the DNS name of the domain.
 `set USERDOMAIN` to find out the NetBIOS name of the domain.
 :::

4. Specify the path to the container with users in Distinguished Name format. To work with all users, select the domain root.
5. If you use the LDAPS protocol to access directories, enable the **Use LDAPS** option.
6. To display a user's photo in the Indeed CM interface or print it on a smart card, select the attribute that contains the user's photo.
7. Click **Save**.

:::caution For an existing Indeed CM configuration
If Indeed CM was previously configured to work with a user directory in Active Directory, and the domain controller was reconfigured from Active Directory to RED ADM, you do not need to change the user directory configuration parameters.
:::


  </TabItem>
  <TabItem value="freeipa" label="FreeIPA">

1. Specify the credentials of an account with access rights to the user directory: name in Distinguished Name format and password.
2. Specify the domain NetBIOS name and the DNS name of the domain or domain controller.

 :::tip how to find the DNS name and NetBIOS name of the domain
 Run in the command line:

 `set USERDNSDOMAIN` to find out the DNS name of the domain.
 `set USERDOMAIN` to find out the NetBIOS name of the domain.
 :::

4. Specify the path to the object with users in Distinguished Name format. We recommend specifying the domain root or the accounts directory.
5. If you use the LDAPS protocol to access directories, enable the **Use LDAPS** option.
6. Click **Save**.


  </TabItem>
  <TabItem value="aldpro" label="ALD Pro">

1. Specify the credentials of an account with access rights to the user directory: name in Distinguished Name format and password.
2. Specify the domain NetBIOS name and the DNS name of the domain or domain controller.

 :::tip how to find the DNS name and NetBIOS name of the domain
 Run in the command line:

 `set USERDNSDOMAIN` to find out the DNS name of the domain.
 `set USERDOMAIN` to find out the NetBIOS name of the domain.
 :::

4. Specify the path to the object with users in Distinguished Name format. We recommend specifying the domain root or the accounts directory.
5. If you use the LDAPS protocol to access directories, enable the **Use LDAPS** option.
6. Click **Save**.


  </TabItem>
 </Tabs>
 </TabItem>
  <TabItem value="cryptopro" label="CryptoPro CA 2.0 Registration Center">

1. Click **Add**.
2. In the drop-down list, select the user name attribute that determines uniqueness during authentication in Indeed CM web applications:
   - **E-mail**
   - **Common Name**
   - **User Principal Name**
   - **Custom**. Specify the OID of the user name attribute.
3. Select the API integration type with the CryptoPro CA 2.0 Registration Center user directory: REST or SOAP.
3. Specify the thumbprint of the service account certificate that will be used to connect to the CryptoPro CA 2.0 Registration Center to view the list of users.
4. Specify the connection URL for the Registration Center. For example, `https://cryptopro.domain.loc/RA/RegAuthLegacyService.svc`.
7. Click **Save**.


  </TabItem>
  <TabItem value="db" label="Internal directory">

Use a Microsoft SQL or PostgreSQL database as the internal user directory.
1. Click **Add**.
2. Select the storage type.
3. Configure the connection to the storage. Enter the server name, instance name (for Microsoft SQL), port number, and database name.
4. Select the authentication method for connecting to the database server:
   - Microsoft SQL: Windows authentication or SQL Server authentication. To connect to SQL Server, enter the user name and password.
   - PostgreSQL: enter the user name and password.
5. Click **Save**.

### Additional attributes of the internal directory {#user-catalog-add-attributes}

To configure additional attributes for the internal user directory:
1. Click **Add**.
2. Enter the attribute name in the user directory and the attribute display name.
3. To display the attribute when creating and editing a user in Indeed CM, enable the **Display in user creation/editing form** option.
4. To make the attribute mandatory when creating and editing a user in Indeed CM, enable the **Required** option.
5. Select the attribute type:
- **Text**
For a text attribute, specify the following settings:
  - maximum text length -- the maximum number of characters.
  - text format -- a regular expression used to validate the text value of the attribute. For example, a validation for patronymic input that allows Russian letters, spaces, and hyphens: `^[A-ZA][a-za]{0,30}(( |-)([a-za]{0,30})){0,2}$`.
  - invalid format message -- the message text that will be displayed when a text value is entered that does not meet the regular expression requirements.
- **Integer**
Specify the minimum and maximum values. For example, for entering age information.
- **Boolean**
The attribute can have a value of `true` or `false`.
- **Value lookup**
Specify the lookup that will be used when selecting attribute values. Format: `<attribute value #1>, <display value #1>; <attribute value #2>, <display value #2>;...`. For example, `red, Red color; green, Green color`.
6. Click **Save**.


  </TabItem>
</Tabs>

### Attribute mapping {#user-catalog-link-attributes}

You can configure the mapping between Certification Authority attributes and user attributes in the directory.

If attribute mapping is configured, you can register a new user in the Certification Authority when issuing a device for that user in Indeed CM.

### Updatable attributes {#user-catalog-update-attributes}

You can configure the list of Active Directory user attributes whose changes should trigger a certificate renewal on the device.

Changes can be tracked only for attributes from the **Subject** and **Subject Alternative Name (SAN)** fields of the certificate.

:::info
In the certificate template settings of Microsoft CA and CryptoPro CA 2.0, the Common Name, E-mail, and User Principal Name attributes are tracked by default.
:::

To track an attribute:
1. Click **Add**.
2. Specify the attribute name in the user directory.
3. Specify the attribute display name.
4. Specify the X.500 name or OID of the attribute in the certificate. The specified value is used to search for the attribute in the certificate.
5. Click **Save**.

## Access control {#access-control}

Select the access control method for Indeed CM services:
- **Windows authentication**
This method allows authentication through Windows OS user credentials and is used for Indeed CM installations on a domain workstation running Windows OS.

- **OpenID Connect authentication**
This method allows authentication through an OpenID Connect server and is used for Indeed CM installations on a domain or non-domain workstation running Windows or Linux OS.

:::caution
Make sure you selected the same authentication method when [installing the Indeed CM Server on Windows OS](/server/components.md?os=windows).
:::

### Configuring OpenID Connect authentication {#access-control-oidc}

1. Specify the following settings:
   - Connection URL for the [OpenID Connect Server](server/openid-connect.md).
   - Fully Qualified Domain Name (FQDN) of the Indeed CM Server. For a multi-server configuration, specify their fully qualified domain names separated by commas.
   - Signing certificate thumbprint.
2. If necessary, generate client secrets.

### Role Administrator {#access-control-roles}

The Role Administrator is an account with rights to manage [roles](admin-guide/configuration/roles.md) in Indeed CM.

Specify the Role Administrator name in the format DOMAIN\UserName or UserName@DNSDomainName. When starting Indeed CM for the first time, log in to the Management Console using the specified account.

:::caution
Make sure the Role Administrator account is included in the user directory.
:::

## Data storage {#database}

Configure the connection to the data storage. [How to create a data storage](/environment/data-storage.md)

1. Select the data storage type depending on the environment where Indeed CM is deployed: Microsoft SQL or PostgreSQL.
2. Configure the connection to the storage. Enter the server name, instance name (for Microsoft SQL), port number, and database name.
3. Select the authentication method for connecting to the database server:
   - Microsoft SQL: Windows authentication or SQL Server authentication. To connect to SQL Server, enter the user name and password.
   - PostgreSQL: enter the user name and password.
4. If necessary, configure additional parameters:
   - minimum pool size
   - maximum pool size
   - connection timeout
   - connection lifetime
   - connection retry count
   - connection retry interval

### Data storage encryption key {#database-encryption}

Indeed CM data is stored and transmitted in encrypted form. In the drop-down list, select the encryption algorithm and click **Generate**. Save a backup of the encryption key.

## Card Monitor service {#card-monitor}

Define the settings for Card Monitor -- a service for monitoring device usage.

<details>
    <summary>More about the Card Monitor service</summary>

Card Monitor is installed automatically together with the Indeed CM Server and performs the following operations:
- revocation and collection of devices belonging to users whose accounts have been deleted from the user directory
- revocation of temporary devices with an expired validity period
- disabling devices belonging to users whose accounts have been disabled
- deleting accounts from the user directory whose accounts have been disabled
- setting or resetting device content status
- registering the *Prolonged loss of agent communication* event in the event log
- deleting agents that have been inactive for a configurable period of time
- sending email notifications to administrators and users about the following events:
    - expiration of user certificates stored on a device
    - approval/rejection of device issuance
    - approval/rejection of certificate renewal on a device
    - approval/rejection of device replacement
    - change of the policy applied to the user

</details>

1. Specify the account under which the Card Monitor service will run, in the format DOMAIN\UserName or UserName@DNSDomainName. Account requirements:
    - is included in the Indeed CM user directory
    - is a member of the Administrators group on the Indeed CM Server
    - has the **Log on as a batch job** permission in the Active Directory policy
2. Configure the Card Monitor service startup time.
3. In the **User operations** section, you can configure the following:
   - **Disable devices of disabled users**. Card Monitor will disable devices belonging to users whose accounts have been disabled in the user directory. If the **Revoke certificate upon device revocation or disable** option is additionally enabled in the certificate template settings of the [CA in use](/admin-guide/configuration/policies/pki-settings/pki-settings.md), the validity of certificates written to devices will be suspended in the CA, and the certificates will be revoked.
   - **Configure behavior filter for disabled users as deleted**. Disabled accounts that match the filter condition are treated as deleted from the user directory. Devices belonging to deleted users are revoked.
   Specify the user attribute and attribute value. For example, the DistinguishedName attribute with the value `OU=Fired users,DC=domain,DC=loc`.
   - **Collect devices from deleted users**. Devices belonging to deleted users are collected and transition to the *Empty* state. During collection, the device is not wiped.
4. In the **Agent operations** section, you can configure the following:
   - **Log event if agent is inactive for more than (min.)**. When the agent loses communication with the server, Card Monitor registers this event in the system log after the specified time elapses.
   - **Delete agent if inactive for more than (days)**. When the agent loses communication with the server, Card Monitor deletes the agent from the database after the specified time elapses.

:::info

A separate service role is required for the Card Monitor service to function. [More about the Card Monitor role](/admin-guide/configuration/roles.md#card-monitor)
:::

## Confirmation {#confirm}

1. Review the settings of all Setup Wizard sections.
2. Click **Apply**.

All configured parameters are written to application configuration files and saved to the *C:\inetpub\wwwroot\cm\wizard\configs* directory for Windows OS and */opt/indeed/cm/wizard/configs/* for Linux OS. The configuration files need to be [applied on the Indeed CM Server](#configure).

## Results {#results}

Enable the **Save configuration files** option to export the files to an archive.

If you are installing Indeed CM for the first time, we recommend saving a copy of the configured parameters. Enable the **Save configuration backup** option and set a password for the file.

The configuration backup contains all parameters defined during installation for all services, as well as the encryption algorithm and database encryption key. Store the backup file in a secure location.

## Configuration restore {#backup}

You can restore the Indeed CM configuration from a backup if you need to:
- update the Indeed CM Server
- migrate the server to a new workstation
- install additional servers

To restore the configuration from a file:
1. Navigate to the **Configuration restore** section of the Setup Wizard.
2. Click **Restore configuration from backup**.
2. Upload the file.
3. If the backup was encrypted, enter the password.

## Applying configuration files on the Indeed CM Server {#configure}

Apply the configuration files created by the Setup Wizard on the Indeed CM Server.

<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows OS" default>

1. Open the PowerShell console as administrator.
2. Navigate to the *C:\inetpub\wwwroot\cm\wizard\configs* directory.
3. Run the PowerShell script *deploy\_configuration.ps1*:

```
.\deploy_configuration.ps1
```
4. During the PowerShell script execution, enter the password for the account used to run the Card Monitor service.

:::tip
It is recommended to specify the local account under which the other Indeed CM web applications are running.
:::

The configuration files for all Indeed CM services are located in the IIS web application root directory at *%SystemDrive%\inetpub\wwwroot\cm*. The configuration files for the Card Monitor service are located in the *%ProgramFiles%\Indeed CM\CardMonitor* directory.


</TabItem>
  <TabItem value="linux" label="Linux OS">

Apply the configuration files created by the Setup Wizard on the Indeed CM Server.

1. Open a terminal emulator.
2. Navigate to the */opt/indeed/cm/wizard/configs* directory.
3. Make sure the script file has execute permissions, and run the bash script *deploy\_configuration.sh*:

```
sh ./deploy_configuration.sh
```

4. During the bash script execution, specify the account under which the Card Monitor service will run.

:::tip
It is recommended to specify the local account under which the other Indeed CM web applications are running.
:::

If multiple Indeed CM Servers are deployed in the infrastructure, apply the configuration files on each server. The configuration files for all Indeed CM services are located in the */opt/indeed/cm* directory.

</TabItem>
</Tabs>

## Encrypting/decrypting configuration files {#encryption}

For security purposes, it is recommended to encrypt Indeed CM application configuration files using the Cm.Config.DataProtector utility. The utility supports the AES encryption algorithm with an effective key length of 256 bits. The encryption key is saved on the Indeed CM Server.

The encryption key is located at:
- Windows OS: *C:\ProgramData\Indeed\cm\keys*
- Linux OS: */etc/indeed/cm/keys*.

:::caution
Create a backup of the encryption key. This will allow you to restore access to encrypted data in case the primary key is lost or damaged. The key backup can be saved together with the [Indeed CM configuration backup](#results).
:::

<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows OS" default>

#### Encryption {#encryption-protect}

1. Navigate to the Indeed CM Server distribution package directory at *Misc\dataprotector*.
2. Run PowerShell as administrator.
3. Execute one of the following commands:
  - encrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component name>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector protect
  ```
  - encrypt configuration files for individual components:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app ManagementConsole
  ```

 <details><summary>Indeed CM component names</summary>

    - Management Console -- ManagementConsole
    - Self-Service Portal -- SelfService
    - Card Monitor service -- CardMonitor
    - Device Unlock and Disable Service -- CredentialProvider
    - Remote Self-Service -- RemoteService
    - API Service -- Api
    - AirCard Cleaner Service -- AirCardCleaner
    - Agent Registration Service -- AgentRegistrationApi
    - Agent Service -- AgentServiceApi
    - OpenID Connect Server -- Oidc

 </details>

- encrypt a configuration file located outside the standard directory:

  ```powershell
  .\Cm.Config.DataProtector protect --app <component name> --file "path to appsettings.json file"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector protect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to the Indeed CM Server distribution package directory at *Misc\dataprotector*.
2. Run PowerShell as administrator.
3. Execute one of the following commands:
  - decrypt all configuration files located in standard directories (*C:\inetpub\wwwroot\<component name>\appsettings.json*):

  ```powershell
  .\Cm.Config.DataProtector unprotect
  ```
  - decrypt configuration files for individual components:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name>
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app ManagementConsole
  ```

 <details><summary>Indeed CM component names</summary>

    - Management Console -- ManagementConsole
    - Self-Service Portal -- SelfService
    - Card Monitor service -- CardMonitor
    - Device Unlock and Disable Service -- CredentialProvider
    - Remote Self-Service -- RemoteService
    - API Service -- Api
    - AirCard Cleaner Service -- AirCardCleaner
    - Agent Registration Service -- AgentRegistrationApi
    - Agent Service -- AgentServiceApi
    - OpenID Connect Server -- Oidc

 </details>

- decrypt a configuration file located outside the standard directory:

  ```powershell
  .\Cm.Config.DataProtector unprotect --app <component name> --file "path to appsettings.json file"
  ```

  ```powershell title="Example command"
  .\Cm.Config.DataProtector unprotect --app CardMonitor --file "C:\Program Files\Indeed CM\CardMonitor\appsettings.json"
  ```

</TabItem>
<TabItem value="linux" label="Linux OS">

#### Encryption {#encryption-protect}

1. Navigate to the Indeed CM Server distribution package directory at *Misc\dataprotector*.
2. Open Linux Bash.
3. Execute one of the following commands:
  - encrypt all configuration files located in standard directories (*/opt/indeed/cm/<component name>/appsettings.json*):

 ```bash
 dotnet Cm.Config.DataProtector.dll protect
 ```
  - encrypt configuration files for individual components:

  ```bash
  dotnet Cm.Config.DataProtector.dll protect --app <component name>
  ```

  ```bash title="Example command"
  dotnet Cm.Config.DataProtector.dll protect --app ManagementConsole
  ```

 <details><summary>Indeed CM component names</summary>

    - Management Console -- ManagementConsole
    - Self-Service Portal -- SelfService
    - Card Monitor service -- CardMonitor
    - Device Unlock and Disable Service -- CredentialProvider
    - Remote Self-Service -- RemoteService
    - API Service -- Api
    - AirCard Cleaner Service -- AirCardCleaner
    - Agent Registration Service -- AgentRegistrationApi
    - Agent Service -- AgentServiceApi
    - OpenID Connect Server -- Oidc

 </details>

  - encrypt a configuration file located outside the standard directory:

  ```bash
  dotnet Cm.Config.DataProtector.dll protect --app <component name> --file "path to appsettings.json file"
  ```

  ```bash title="Example command"
  dotnet Cm.Config.DataProtector.dll protect --app ManagementConsole --file "/opt/indeed/cm/mc/appsettings.json"
  ```


#### Decryption {#encryption-unprotect}

1. Navigate to the Indeed CM Server distribution package directory at *Misc\dataprotector*.
2. Open Linux Bash.
3. Execute one of the following commands:
  - decrypt all configuration files located in standard directories (*/opt/indeed/cm/<component name>/appsettings.json*):

 ```bash
 dotnet Cm.Config.DataProtector.dll unprotect
 ```
  - decrypt configuration files for individual components:

  ```bash
  dotnet Cm.Config.DataProtector.dll unprotect --app <component name>
  ```

  ```bash title="Example command"
  dotnet Cm.Config.DataProtector.dll unprotect --app ManagementConsole
  ```

 <details><summary>Indeed CM component names</summary>

    - Management Console -- ManagementConsole
    - Self-Service Portal -- SelfService
    - Card Monitor service -- CardMonitor
    - Device Unlock and Disable Service -- CredentialProvider
    - Remote Self-Service -- RemoteService
    - API Service -- Api
    - AirCard Cleaner Service -- AirCardCleaner
    - Agent Registration Service -- AgentRegistrationApi
    - Agent Service -- AgentServiceApi
    - OpenID Connect Server -- Oidc

 </details>

- decrypt a configuration file located outside the standard directory:

  ```bash
  dotnet Cm.Config.DataProtector.dll unprotect --app <component name> --file "path to appsettings.json file"
  ```

  ```bash title="Example command"
  dotnet Cm.Config.DataProtector.dll unprotect --app ManagementConsole --file "/opt/indeed/cm/mc/appsettings.json"
  ```

</TabItem>
</Tabs>

## Disabling the Setup Wizard {#stop}

For security purposes, it is recommended to disable the Indeed CM Setup Wizard web application after the configuration process is complete.

<Tabs groupId="os" queryString>
<TabItem value="windows" label="Windows OS" default>

1. Open IIS Manager (Internet Information Services Manager) and in the left menu select **Application pools**.
2. Select the IndeedCM Wizard application and in the right menu click **Stop**.


</TabItem>
<TabItem value="linux" label="Linux OS">

1. Open a terminal emulator.
2. Execute the command:
```bash
sudo systemctl stop cm-wizard.service
```

</TabItem>
</Tabs>
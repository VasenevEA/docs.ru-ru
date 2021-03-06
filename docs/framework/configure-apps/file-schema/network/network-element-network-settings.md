---
title: '&lt;сети&gt; элемент (параметры сети)'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#network
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/network
helpviewer_keywords:
- <network> element
- network element
ms.assetid: 2c2c6ad4-ed11-48ab-b28e-2bc0ba9b42c7
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: e53d39f15a01f751a93c5531b3079d77bf0040e4
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="ltnetworkgt-element-network-settings"></a>&lt;сети&gt; элемент (параметры сети)
Настройка сетевых параметров для внешнего сервера Simple Mail Transport Protocol (SMTP).  
  
 \<configuration>  
\<System.NET >  
\<mailSettings >  
\<SMTP >  
\<сети >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<network  
  clientDomain="string"   
  defaultCredentials="true|false"  
  enableSsl="true|false"  
  host="string"   
  password="string"  
  port="integer"   
  targetName="string"  
  userName="string"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|`clientDomain`|Указывает имя домена клиента для использования в запросом протокола SMTP для подключения к почтовому серверу SMTP. Значение по умолчанию — имя localhost локального компьютера, отправляющего запрос.|  
|`defaultCredentials`|Указывает, следует ли использовать учетные данные пользователя по умолчанию для доступа к почтовому серверу SMTP для SMTP-транзакций. Значение по умолчанию — `false`.|  
|`enableSsl`|Указывает, используется ли протокол SSL для доступа к почтовому серверу SMTP. Значение по умолчанию — `false`.|  
|`host`|Указывает имя узла почтового SMTP-сервера для SMTP-транзакций. Этот атрибут имеет значение по умолчанию отсутствует.|  
|`password`|Указывает пароль, используемый для проверки подлинности на SMTP-сервер. Этот атрибут имеет значение по умолчанию отсутствует.|  
|`port`|Указывает номер порта для подключения к почтовому серверу SMTP. Значение по умолчанию — 25.|  
|`targetName`|Указывает имя поставщика службы (SPN) для проверки подлинности при использовании расширенной защиты для SMTP-транзакций. Этот атрибут имеет значение по умолчанию отсутствует.|  
|`userName`|Указывает имя пользователя для проверки подлинности на SMTP-сервер. Этот атрибут имеет значение по умолчанию отсутствует.|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Отсутствует.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<SMTP > Element (Network Settings)](../../../../../docs/framework/configure-apps/file-schema/network/smtp-element-network-settings.md)|Настраивает параметры отправки сообщений транспортного протокола SMTP (Simple Mail).|  
  
## <a name="remarks"></a>Примечания  
 Некоторые SMTP требуют проверки подлинности на сервере, перед использованием. Если вы хотите пройти проверку подлинности с помощью сетевые учетные данные по умолчанию на узле, задайте `defaultCredentials` атрибут `true`. <xref:System.Net.Configuration.SmtpNetworkElement.DefaultCredentials%2A?displayProperty=nameWithType> Свойство может использоваться для получения текущего значения `defaultCredentials` атрибут из применимые файлы конфигурации.  
  
 Можно также использовать обычную проверку подлинности (имя пользователя и пароль) для проверки подлинности на SMTP-сервер. Чтобы использовать этот параметр, необходимо указать допустимое имя пользователя и пароль для указанного сервера SMTP.  
  
> [!NOTE]
>  Обычная проверка подлинности передает `userName` и `password` значения на сервер без шифрования. Любой пользователь, наблюдение за сетевым трафиком можно просматривать свои учетные данные и использовать их для подключения к серверу. Следует рассмотреть возможность использования более безопасный механизм проверки подлинности, такие как Kerberos и NT LAN Manager (NTLM). Если `defaultCredentials` — `true`, Kerberos или NTLM используется, если сервер поддерживает эти протоколы.  
  
 Основные параметры проверки подлинности и по умолчанию сетевых учетных данных являются взаимоисключающими; Если задать `defaultCredentials` для `true` и укажите имя пользователя и пароль, использовать сетевые учетные данные по умолчанию и данные обычной проверки подлинности, учитываются.  
  
 Для обычной проверки подлинности, при указании `userName`, необходимо также указать `password` для проверки подлинности самостоятельно к почтовому серверу.  
  
 <xref:System.Net.Configuration.SmtpNetworkElement.UserName%2A?displayProperty=nameWithType> Свойство может использоваться для получения текущего значения `userName` атрибут из применимые файлы конфигурации. <xref:System.Net.Configuration.SmtpNetworkElement.Password%2A?displayProperty=nameWithType> Свойство может использоваться для получения текущего значения `password` атрибут из применимые файлы конфигурации. Объект `password` атрибут будет обычно не вносится в файлах конфигурации, по соображениям безопасности.  
  
 `clientDomain` Атрибут изменяет имя домена клиента, используемое запросом протокола SMTP для SMTP-сервера. `clientDomain` Атрибута может быть присвоено полное доменное имя локального компьютера, а не имя localhost, который используется по умолчанию. Это обеспечивает большее соответствие стандартам протокола SMTP. Значение по умолчанию — имя localhost локального компьютера, отправляющего запрос. <xref:System.Net.Configuration.SmtpNetworkElement.ClientDomain%2A?displayProperty=nameWithType> Свойство может использоваться для получения текущего значения `clientDomain` атрибут из применимые файлы конфигурации.  
  
 `targetName` Атрибут используется для проверки подлинности при использовании расширенной защиты. Значение по умолчанию имеет форму «SMTPSVC /\<узла >» где \<узла > — имя узла почтового SMTP-сервера. <xref:System.Net.Configuration.SmtpNetworkElement.TargetName%2A?displayProperty=nameWithType> Свойство может использоваться для получения текущего значения `targetName` атрибут из применимые файлы конфигурации.  
  
 `enableSsl` Атрибут указывает, используется ли протокол SSL для доступа к почтовому серверу SMTP. <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType> Класс поддерживает только расширения службы SMTP для защиты SMTP через протокол TLS как определено в документе RFC 3207. В этом режиме сеанс SMTP начинается в незашифрованном канале, а затем выдает команды STARTTLS клиента на сервере, чтобы переключиться на безопасное соединение с помощью протокола SSL. См. в RFC 3207 публикации по IETF Internet Engineering Task Force () для получения дополнительной информации.  
  
 Альтернативный способ подключения — где сеанс SSL устанавливается заранее перед любой протокол отправки команд. Этот способ подключения иногда называют SMTPS и по умолчанию используется порт 465. Это альтернативный способ подключения с помощью протокола SSL в настоящее время не поддерживается.  
  
 <xref:System.Net.Configuration.SmtpNetworkElement.EnableSsl%2A?displayProperty=nameWithType> Свойство может использоваться для получения текущего значения `enableSsl` атрибут из применимые файлы конфигурации.  
  
## <a name="example"></a>Пример  
 Следующий пример указывает соответствующие параметры SMTP для отправки электронной почты, используя сетевые учетные данные по умолчанию.  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="network">  
        <network  
          clientDomain="www.contoso.com"  
          defaultCredentials="true"  
          enableSsl="false"  
          host="mail.contoso.com"  
          port="25"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>См. также  
 <xref:System.Net.Configuration.SmtpNetworkElement?displayProperty=nameWithType>  
 <xref:System.Net.Configuration.SmtpSection?displayProperty=nameWithType>  
 <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>  
 [Схема параметров сети](../../../../../docs/framework/configure-apps/file-schema/network/index.md)

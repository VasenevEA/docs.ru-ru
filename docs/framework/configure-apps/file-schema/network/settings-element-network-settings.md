---
title: '&lt;Параметры&gt; элемент (параметры сети)'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#settings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings
helpviewer_keywords:
- settings element
- <settings> element
ms.assetid: 189ce989-c39b-427d-b004-6b82a668b931
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: 3f717705a6cd4cc29fe333f5012c7fec466d350b
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="ltsettingsgt-element-network-settings"></a>&lt;Параметры&gt; элемент (параметры сети)
Настраивает основные параметры сети для пространства имен <xref:System.Net?displayProperty=nameWithType>.  
  
 \<configuration>  
\<System.NET >  
\<Параметры >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<settings>  
  <httpListener> … </httpListener>  
  <httpWebRequest> … </httpWebRequest>  
  <ipv6> … </ipv6>  
  <performanceCounters> … </performanceCounters>  
  <servicePointManager> … </servicePointManager>  
  <socket> … </socket>  
  <webProxyScript> … </webProxyScript>  
</settings>  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
 Отсутствует.  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[HttpListener](../../../../../docs/framework/configure-apps/file-schema/network/httplistener-element-network-settings.md)|Настраивает параметры, используемые <xref:System.Net.HttpListener> класса.|  
|[HttpWebRequest](../../../../../docs/framework/configure-apps/file-schema/network/httpwebrequest-element-network-settings.md)|Настраивает параметры веб-запроса.|  
|[IPv6](../../../../../docs/framework/configure-apps/file-schema/network/ipv6-element-network-settings.md)|Протокол IP версии 6 (IPv6) позволяет поддерживать.|  
|[\<performanceCounter > Element (Network Settings)](../../../../../docs/framework/configure-apps/file-schema/network/performancecounter-element-network-settings.md)|Включает счетчики производительности сети.|  
|[servicePointManager](../../../../../docs/framework/configure-apps/file-schema/network/servicepointmanager-element-network-settings.md)|Настраивает подключения к сетевым ресурсам.|  
|[Сокет](../../../../../docs/framework/configure-apps/file-schema/network/socket-element-network-settings.md)|Указывает, используют ли операции сокета порты завершения.|  
|[\<webProxyScript > Element (Network Settings)](../../../../../docs/framework/configure-apps/file-schema/network/webproxyscript-element-network-settings.md)|Настраивает характеристики сценария для обнаружения веб-прокси.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[System.NET](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|Содержит параметры сети, определяющие способ подключения .NET Framework к Интернету.|  
  
## <a name="remarks"></a>Примечания  
  
## <a name="configuration-files"></a>Файлы конфигурации  
 Этот элемент может использоваться в файле конфигурации приложения или в файле конфигурации компьютера (Machine.config).  
  
## <a name="see-also"></a>См. также  
 <xref:System.Net?displayProperty=nameWithType>  
 [Схема параметров сети](../../../../../docs/framework/configure-apps/file-schema/network/index.md)

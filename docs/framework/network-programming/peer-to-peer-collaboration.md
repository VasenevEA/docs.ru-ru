---
title: "Одноранговая совместная работа"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b6216d88-bccb-4a59-9f1c-9f751708e811
caps.latest.revision: 
author: mcleblanc
ms.author: markl
manager: markl
ms.workload:
- dotnet
ms.openlocfilehash: 5060e12fb6a9fcc1bac1dfe6ccdcbaea9f2e6385
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2018
---
# <a name="peer-to-peer-collaboration"></a>Одноранговая совместная работа
Одноранговая сеть предусматривает использование относительно производительных компьютеров (ПК), которые размещаются на границе Интернета, для выполнения других вычислительных задач, помимо клиентских. Современные персональных компьютеров (ПК) имеет очень быстрый процессор, vast памяти и диск большого размера, ни один из которых полностью используются при выполнении обычных вычислительных задач, например электронной почты и просмотра веб-страниц. В большинстве случаев современные ПК могут с легкостью выступать в качестве как клиента, так и сервера (одноранговый узел).  
  
-   Инфраструктура одноранговой совместной работы представляет собой упрощенную реализацию инфраструктуры одноранговой сети Microsoft Windows, в которой используется служба соседних пользователей из ОС Windows Vista и более поздних платформ. Она оптимально подходит для приложений с поддержкой однорангового взаимодействия в подсети, в которой работает служба соседних пользователей, однако также может применяться для работы с конечными точками или контактами. В ее состав входит общий диспетчер контактов, который используется в Live Messenger и других программах на основе технологии Live для определения конечных точек контакта, а также сведений о доступности и присутствии.  
  
-  
  
## <a name="collaboration-applications"></a>Приложения для совместной работы  
 Типовое приложение для одноранговой совместной работы выполняет следующие шаги:  
  
-   Одноранговый узел определяет удостоверение однорангового узла, которому требуется разместить сеанс совместной работы.  
  
-   Соответствующим способом отправляется запрос на размещение сеанса, и одноранговый узел ведущего приложения принимает запрос на управление совместной работой.  
  
-   Ведущее приложение приглашает в сеанс контакты, входящие в подсеть, включая запрашивающую сторону.  
  
-   Все одноранговые узлы, которые будут участвовать в сеансе совместной работы, добавляют ведущее приложение в свои диспетчеры контактов.  
  
-   Большинство одноранговых узлов в установленное время отправляют на одноранговый узел ведущего приложения ответы на приглашения, в которых принимают и отклоняют его.  
  
-   Все одноранговые узлы, которые будут участвовать в сеансе совместной работы, подписываются на одноранговый узел ведущего приложения.  
  
-   В ходе сеанса совместной работы одноранговый узел ведущего приложения может добавлять в диспетчер контактов другие удаленные одноранговые узлы. Также он обрабатывает все ответы на приглашения, определяя узлы, которые приняли, отклонили приглашение или не ответили на него.  Если узел не принял приглашение, оно может быть отменено. Также могут предприниматься другие действия.  
  
-   В этот момент времени одноранговый узел ведущего приложения может начать сеанс совместной работы со всеми приглашенными одноранговыми узлами или зарегистрировать приложение в инфраструктуре совместной работы.  P2P-приложения используют инфраструктуру одноранговой совместной работы и пространство имен <xref:System.Net.PeerToPeer.Collaboration> для координации взаимодействия в играх, досках объявлений, конференциях и других приложениях управления присутствием без использования сервера.  
  
-  
  
## <a name="peer-to-peer-networking-security"></a>Безопасность одноранговой сети  
 В домене Active Directory контроллеры домена реализуют службы проверки подлинности на основе Kerberos. В одноранговой среде без серверов одноранговые узлы должны использовать собственные функции проверки подлинности. В одноранговой сети в роли центра сертификации может выступать любой узел, благодаря чему не требуется наличие корневого сертификата в доверенном корневом хранилище каждого однорангового узла. Проверка подлинности реализуется с использованием самозаверяющих сертификатов формата X.509. Эти сертификаты создаются каждым одноранговым узлом, который создает пару открытого и закрытого ключа и сертификат, подписанный закрытым ключом. Самозаверяющий сертификат используется для проверки подлинности и предоставления сведений о сущности однорангового узла. Как и в случае с проверкой подлинности X.509, в одноранговой сети проверка подлинности реализуется с использованием цепочки сертификатов, которая может прослеживаться обратно к доверенному открытому ключу.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Net.PeerToPeer.Collaboration>  
 [О пространстве имен System.Net.PeerToPeer.Collaboration](../../../docs/framework/network-programming/about-the-system-net-peertopeer-collaboration-namespace.md)

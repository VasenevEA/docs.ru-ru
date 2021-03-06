---
title: Отслеживание действий при обеспечении безопасности сообщений
ms.date: 03/30/2017
ms.assetid: 68862534-3b2e-4270-b097-8121b12a2c97
author: BrucePerlerMS
manager: mbaldwin
ms.openlocfilehash: 31882dfff746aa8e0e45698f70b0f19ae413d66a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="activity-tracing-in-message-security"></a>Отслеживание действий при обеспечении безопасности сообщений
В данном разделе описывается трассировка действий для обработки событий безопасности, которая осуществляется в три этапа (см. ниже).  
  
-   Согласование и обмен маркерами SCT. Это может происходить на транспортном уровне (посредством обмена двоичными данными) или на уровне сообщений (посредством обмена сообщениями SOAP).  
  
-   Зашифровывание и расшифровывание сообщений с проверкой подписи и проверкой подлинности. Трассировки создаются во внешнем действии (обычно "Обработать действие").  
  
-   Авторизация и проверка. Это может происходить локально или при обмене данными между конечными точками.  
  
## <a name="negotiationsct-exchange"></a>Согласование и обмен маркерами SCT  
 В ходе этапа согласования и обмена маркерами SCT на клиенте создается два типа действий: "Установить безопасный сеанс" и "Закрыть безопасный сеанс". "Установить безопасный сеанс" охватывает трассировки для обмена сообщениями RST/RSTR/SCT, а "Закрыть безопасный сеанс" включает трассировки для сообщения отмены.  
  
 На сервере каждый запрос или ответ RST/RSTR/SCT происходит в собственном действии. Если `propagateActivity` = `true` на сервер и клиент, действия на сервере с одинаковыми идентификаторами и появляются вместе в «установить безопасный сеанс» при просмотре через Service Trace Viewer.  
  
 Данная модель трассировки действий применяется для проверки подлинности по имени пользователя и паролю, проверки подлинности сертификатов и проверки подлинности NTLM.  
  
 В следующей таблице перечислены действия и трассировки для согласования и обмена маркерами SCT.  
  
||Время начала согласования и обмена маркерами SCT|Действия|Трассировки|  
|-|-------------------------------------------------|----------------|------------|  
|Безопасный транспорт<br /><br /> (HTTPS, SSL)|При получении первого сообщения.|Трассировки создаются во внешнем действии.|-Трассировки обмена<br />-Безопасный канал<br />-Общие секретные данные получены.|  
|Уровень защищенных сообщений<br /><br /> (WSHTTP)|При получении первого сообщения.|На клиенте:<br /><br /> -«Установить безопасный сеанс» из «Обработать действие» первого сообщения, для каждого запроса или ответа RST/RSTR/SCT.<br />-«Закрыть безопасный сеанс» для exchange "Отмена", «операциями закрыть прокси». В зависимости от времени закрытия безопасного сеанса данное действие может произойти из другого внешнего действия.<br /><br /> На сервере:<br /><br /> -Одно действие «Обработать действие» для каждого запроса или ответа RST/SCT/Cancel на сервере. Если `propagateActivity` = `true`, действия RST/RSTR/SCT объединяются с «Установить безопасный сеанс» и "Отмена" объединяется с действием «Закрыть» от клиента.<br /><br /> Для действия "Установить безопасный сеанс" предусмотрено два этапа:<br /><br /> 1.  Согласование проверки подлинности. Этот этап не является обязательным, если у клиента уже есть надлежащие учетные данные. Этот этап можно выполнить посредством безопасного транспорта или обмена сообщениями. В последнем случае может осуществляться 1 или 2 операции обмена маркерами RST/RSTR. В случае этих операций обмена трассировки создаются в новых действиях запроса или ответа, как описано выше.<br />2.  Установление безопасного сеанса (SCT), при котором выполняется одна операция обмена маркерами RST/RSTR. Внешние действия аналогичны описанным выше.|-Трассировки обмена<br />-Безопасный канал<br />-Общие секретные данные получены.|  
  
> [!NOTE]
>  В смешанном режиме безопасности согласование проверки подлинности происходит при обмене двоичными данными, но SCT происходит при обмене сообщениями. В чистом режиме передачи согласование происходит только в процессе передачи без каких-либо дополнительных действий.  
  
## <a name="message-encryption-and-decryption"></a>Зашифровывание и расшифровывание сообщений  
 В следующей таблице перечислены действия и трассировки для зашифровывания и расшифровывания сообщений, а также проверки подписи.  
  
||Безопасный транспорт<br /><br /> (HTTPS, SSL) и уровень защищенных сообщений<br /><br /> (WSHTTP)|  
|-|---------------------------------------------------------------------------------|  
|Время начала зашифровывания или расшифровывания сообщения либо проверки подписи|При получении сообщения|  
|Действия|Трассировки создаются в действии ProcessAction на клиенте и сервере.|  
|Трассировки|-sendSecurityHeader (отправитель):<br />-Подпись сообщения<br />-Зашифровать данные запроса<br />-receiveSecurityHeader (получатель):<br />-Проверка подписи<br />-Расшифровать данные ответа<br />-Проверка подлинности|  
  
> [!NOTE]
>  В чистом режиме передачи зашифровывание или расшифровывание сообщения происходит только в процессе передачи без каких-либо дополнительных действий.  
  
## <a name="authorization-and-verification"></a>Авторизация и проверка  
 В следующей таблице перечислены действия и трассировки для авторизации.  
  
||Время начала авторизации|Действия|Трассировки|  
|-|-------------------------------------|----------------|------------|  
|Локальный (по умолчанию)|После расшифровывания сообщения на сервере|Трассировки создаются в действии ProcessAction на сервере.|Пользователь авторизован.|  
|Remote|После расшифровывания сообщения на сервере|Трассировки создаются в новом действии, вызываемом действием ProcessAction.|Пользователь авторизован.|

---
title: Использование привязок для настройки служб и клиентов
ms.date: 03/30/2017
helpviewer_keywords:
- bindings [WCF], using
ms.assetid: c39479c3-0766-4a17-ba4c-97a74607f392
ms.openlocfilehash: 8271f51885c0d7800d26018b94942a7d832bf4a5
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2018
---
# <a name="using-bindings-to-configure-services-and-clients"></a>Использование привязок для настройки служб и клиентов
Привязки - это объекты, которые указывают подробные сведения о связи, требуемые для подключения к конечной точке. В частности, привязки содержат информацию о конфигурации, используемую для создания среды выполнения клиента или службы путем определения подробной информации о транспорте, форматах подключения (кодировка сообщения) и протоколах, используемых для соответствующей конечной точки или канала клиента. Чтобы создать работоспособную службу Windows Communication Foundation (WCF), каждая конечная точка в службе требует привязки. В настоящем разделе описывается, что такое привязки, как они определяются и как для конечной точки указывается конкретная привязка.  
  
## <a name="what-a-binding-defines"></a>Что определяет привязка  
 Информация в привязке может быть очень простой или очень сложной. Самые простые привязки указывают только транспортный протокол (такой как HTTP), который должен использоваться для подключения к конечной точке. В общем случае, информация в привязке указывает на то, как подключиться к конечной точке, и попадает в одну из категорий, указанных в таблице ниже.  
  
 Протоколы  
 Определяет используемый механизм безопасности: способность надежного обмена сообщениями или настройки потока контекста транзакции.  
  
 Transport  
 Определяет основной используемый транспортный протокол (например, TCP или HTTP).  
  
 кодировка  
 Определяет кодирование сообщения, например кодирование text/XML, двоичное кодирование или кодирование подсистемы оптимизации передачи сообщений (MTOM), которое определяет, каким образом сообщения представляются в байтовых потоках в сети.  
  
## <a name="system-provided-bindings"></a>Привязки, предоставляемые системой  
 WCF содержит ряд предоставляемых системой привязок, которые разработаны для удовлетворения большинства требований и сценариев приложения. В следующих классах представлены некоторые примеры привязок, предоставляемых системой.  
  
-   <xref:System.ServiceModel.BasicHttpBinding>: привязка по протоколу HTTP, которая подходит для взаимодействия с веб-службами, совместимыми со спецификацией WS-I Basic Profile 1.1 (например, службами, основанными на веб-службах ASP.NET Web (ASMX).  
  
-   <xref:System.ServiceModel.WSHttpBinding>: привязка по протоколу HTTP, которая подходит для взаимодействия с конечными точками, которые соответствуют протоколам спецификаций веб-служб.  
  
-   <xref:System.ServiceModel.NetNamedPipeBinding>: Использует .NET двоичное кодирование и технологии формирования кадров совместно с транспортом именованных каналов Windows для подключения к другим конечным точкам WCF на том же компьютере.  
  
-   <xref:System.ServiceModel.NetMsmqBinding>: Использует .NET двоичное кодирование и технологии формирования кадров совместно с очередью сообщений (MSMQ) для создания подключений очередей сообщений с другими конечными точками WCF.  
  
 Полный список системных привязок с описаниями, см. [привязка, предоставляемая системой](../../../docs/framework/wcf/system-provided-bindings.md).  
  
## <a name="custom-bindings"></a>Пользовательские привязки  
 Если в коллекции привязок, поставляемой в составе системы, нет нужного для приложения службы сочетания функций, можно создать привязку <xref:System.ServiceModel.Channels.CustomBinding>. Дополнительные сведения об элементах <xref:System.ServiceModel.Channels.CustomBinding> привязки, в разделе [ \<customBinding >](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) и [пользовательские привязки](../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## <a name="using-bindings"></a>Использование привязок  
 Использование привязок включает два основных этапа.  
  
1.  Выбор или определение привязки. Самый простой способ - выбрать одну из предоставляемых системой привязок и использовать ее настройки по умолчанию. Также можно выбрать предоставляемую системой привязку и сбросить значения ее свойств таким образом, чтобы они соответствовали нужным требованиям. Кроме того, можно создать пользовательскую привязку и задать как требуется каждое свойство.  
  
2.  Создать конечную точку, которая использует данную привязку.  
  
## <a name="code-and-configuration"></a>Код и конфигурация  
 Определить и настроить привязки можно посредством кода или конфигурации. Эти два подхода не зависят от типа используемой привязки, например, при использовании привязки, предоставляемой системой, или привязки <xref:System.ServiceModel.Channels.CustomBinding>. Как правило, использование кода дает полный контроль над определением привязки при компиляции. С другой стороны, использование конфигурации позволяет системному администратору или пользователю службы WCF или клиента, чтобы изменить параметры привязок. Такая гибкость часто является предпочтительным, так как нет способа предугадать требования конкретного компьютера и сети, условия, в которых будет развертываться приложения WCF. Отделение информации о привязке (и адресации) от кода позволяет администраторам изменять информацию о привязке без повторной компиляции или повторного развертывания приложения. Обратите внимание, что, если привязка определена в коде, он заменяет любые определения, основанные на конфигурации, выполненные в файле конфигурации. Примеры таких подходов см. в следующих разделах.  
  
-   [Как: размещение службы WCF в приложениях, управляемых](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md) примером является создание привязки в коде.  
  
-   [Как: Настройка клиента](../../../docs/framework/wcf/how-to-configure-a-basic-wcf-client.md) примером является создание клиента с помощью конфигурации.  
  
## <a name="see-also"></a>См. также  
 [Общие сведения о создании конечных точек](../../../docs/framework/wcf/endpoint-creation-overview.md)  
 [Практическое руководство. Указание привязки службы в конфигурации](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)  
 [Практическое руководство. Указание привязки службы в коде](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-code.md)  
 [Практическое руководство. Указание привязки клиента в конфигурации](../../../docs/framework/wcf/how-to-specify-a-client-binding-in-configuration.md)  
 [Практическое руководство. Указание привязки клиента в коде](../../../docs/framework/wcf/how-to-specify-a-client-binding-in-code.md)

---
title: Поддержка запросов
ms.date: 03/30/2017
ms.assetid: 093c22f5-3294-4642-857a-5252233d6796
ms.openlocfilehash: 5c46ed5ae2fc2cc2275bfa7251fe5f8fa346c1f4
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="support-for-queries"></a>Поддержка запросов
Хранилище экземпляров рабочих процессов SQL записывает набор известных свойств в хранилище. Пользователи могут выполнить запрос экземпляров на основе этих свойств. В следующем списке приведены некоторые из этих известных свойств.  
  
-   **Имя сайта.** Имя веб-узла, содержащего службу.  
  
-   **Путь относительно приложения.** Путь приложения относительно веб-узла.  
  
-   **Служба относительный путь.** Путь службы относительно приложения.  
  
-   **Имя службы.** Имя службы.  
  
-   **Пространство имен службы.** Имя пространства имен, которое использует служба.  
  
-   **Текущий компьютер.**  
  
-   **Последний компьютер**. Компьютер, на котором экземпляр службы рабочего процесса был запущен последний раз.  
  
> [!NOTE]
>  Для резидентных сценариев, использующих узел службы рабочего процесса, заполняются только последние четыре свойства. Для сценариев приложения рабочего процесса заполняется только последнее свойство.  
  
 Среда выполнения рабочего процесса предоставляет значения для первых трех свойств. Узел службы рабочего процесса предоставляет значения для **Причина приостановки** свойство. Хранилище экземпляров рабочих процессов SQL сама предоставляет значения для **последний обновленный компьютер** свойство.  
  
 Возможность хранилища экземпляров рабочих процессов SQL также позволяет указать пользовательские свойства, значения которых требуется сохранять в базе данных сохраняемости и которые будут в дальнейшем использованы в запросах. Дополнительные сведения о пользовательских акции см. в разделе [расширения хранилища](../../../docs/framework/windows-workflow-foundation/store-extensibility.md).  
  
## <a name="views"></a>Представления  
 Хранилище экземпляров содержит следующие представления. В разделе [схемы базы данных сохраняемости](../../../docs/framework/windows-workflow-foundation/persistence-database-schema.md) для получения дополнительных сведений.  
  
### <a name="the-instances-view"></a>Представление экземпляров  
 Представление экземпляров содержит следующие поля:  
  
1.  **Идентификатор**  
  
2.  **PendingTimer**  
  
3.  **CreationTime**  
  
4.  **LastUpdatedTime**  
  
5.  **ServiceDeploymentId**  
  
6.  **SuspensionExceptionName**  
  
7.  **SuspensionReason**  
  
8.  **ActiveBookmarks**  
  
9. **CurrentMachine**  
  
10. **LastMachine**  
  
11. **ExecutionStatus**  
  
12. **IsInitialized.**  
  
13. **IsSuspended**  
  
14. **IsCompleted**  
  
15. **EncodingOption**  
  
16. **ReadWritePrimitiveDataProperties**  
  
17. **WriteOnlyPrimitiveDataProperties**  
  
18. **ReadWriteComplexDataProperties**  
  
19. **WriteOnlyComplexDataProperties**  
  
### <a name="the-servicedeployments-view"></a>Представление ServiceDeployments  
 Представление ServiceDeployments содержит следующие поля:  
  
1.  **Имя сайта**  
  
2.  **RelativeServicePath**  
  
3.  **RelativeApplicationPath**  
  
4.  **ServiceName**  
  
5.  **ServiceNamespace**  
  
### <a name="the-instancepromotedproperties-view"></a>Представление InstancePromotedProperties  
 Представление InstancePromotedProperties содержит следующие поля. Дополнительные сведения о распространенных свойств см. в разделе [расширения хранилища](../../../docs/framework/windows-workflow-foundation/store-extensibility.md) раздела.  
  
1.  **Идентификатор экземпляра**  
  
2.  **EncodingOption**  
  
3.  **Имя PromotionName**  
  
4.  **Значение #** (ряд полей от **значение1** для **Value64**).

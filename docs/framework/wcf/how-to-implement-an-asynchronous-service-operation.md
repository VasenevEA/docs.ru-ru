---
title: Практическое руководство. Асинхронная реализация операции службы
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4e5d2ea5-d8f8-4712-bd18-ea3c5461702c
ms.openlocfilehash: b8e6ce386dc122ba059a18a448239cec7eaae222
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-implement-an-asynchronous-service-operation"></a>Практическое руководство. Асинхронная реализация операции службы
В приложениях Windows Communication Foundation (WCF) операции службы может быть реализована асинхронно или синхронно без жесткого задания клиенту способа вызова. Например, асинхронные операции службы могут вызываться синхронно или синхронные операции службы могут вызываться асинхронно. Пример, демонстрирующий способы асинхронного вызова операции в клиентском приложении см. в разделе [как: асинхронно вызывать операции службы](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md). Дополнительные сведения о синхронных и асинхронных операциях см. в разделе [проектирование контрактов службы](../../../docs/framework/wcf/designing-service-contracts.md) и [синхронной и асинхронной операции](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md). В этом разделе описывается базовая структура асинхронной операции службы, код не завершен. Полный пример клиенту и службе сторон см [асинхронной](http://msdn.microsoft.com/library/833db946-f511-4f64-a26f-2759a11217c7).  
  
### <a name="implement-a-service-operation-asynchronously"></a>Асинхронная реализация операции службы  
  
1.  В контракте службы объявите пару асинхронных методов в соответствии с рекомендациями по асинхронной разработке для платформы .NET. Метод `Begin` принимает параметр, объект обратного вызова и объект состояния, а возвращает <xref:System.IAsyncResult?displayProperty=nameWithType>; соответствующий метод `End` принимает <xref:System.IAsyncResult?displayProperty=nameWithType> и возвращает возвращаемое значение. Дополнительные сведения об асинхронных вызовов см. в разделе [проектные шаблоны асинхронного программирования](http://go.microsoft.com/fwlink/?LinkId=248221).  
  
2.  Пометьте метод `Begin` пары асинхронных методов атрибутом <xref:System.ServiceModel.OperationContractAttribute?displayProperty=nameWithType> и задайте для свойства <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A?displayProperty=nameWithType> значение `true`. Например, приведенный ниже код выполняет шаги 1 и 2.  
  
     [!code-csharp[C_SyncAsyncClient#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#6)]
     [!code-vb[C_SyncAsyncClient#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#6)]  
  
3.  Реализуйте пару методов `Begin/End` в классе своей службы в соответствии с рекомендациями по асинхронной разработке. Например, в следующем примере кода показана реализация, в которой строка записывается в консоль как в части `Begin`, так и в части `End` асинхронной операции службы, и возвращаемое значение операции `End` возвращается клиенту. Полный пример кода см. в подразделе "Пример".  
  
     [!code-csharp[C_SyncAsyncClient#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#3)]
     [!code-vb[C_SyncAsyncClient#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#3)]  
  
## <a name="example"></a>Пример  
 В следующих примерах кода показаны:  
  
1.  Интерфейс контракта службы с:  
  
    1.  Синхронной операцией `SampleMethod`.  
  
    2.  Асинхронной операцией `BeginSampleMethod`.  
  
    3.  Асинхронную `BeginServiceAsyncMethod` / `EndServiceAsyncMethod` пары операции.  
  
2.  Реализацией службы с использованием объекта <xref:System.IAsyncResult?displayProperty=nameWithType>.  
  
 [!code-csharp[C_SyncAsyncClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#1)]
 [!code-vb[C_SyncAsyncClient#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#1)]  
  
## <a name="see-also"></a>См. также  
 [Разработка контрактов службы](../../../docs/framework/wcf/designing-service-contracts.md)  
 [Синхронные и асинхронные операции](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)

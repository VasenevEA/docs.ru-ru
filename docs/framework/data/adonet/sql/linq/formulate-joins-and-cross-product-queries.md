---
title: Практическое руководство. Формулировка запросов-объединений и запросов векторного произведения
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d8072ede-0521-4670-9bec-1778ceeb875b
ms.openlocfilehash: 20b46ce37d93119330e336f583ac68b5c1dc4c4b
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="formulate-joins-and-cross-product-queries"></a>Практическое руководство. Формулировка запросов-объединений и запросов векторного произведения
В следующем примере показано, как объединить результаты из нескольких таблиц.  
  
## <a name="example"></a>Пример  
 В следующем примере используется переходы по внешним ключам в `From` предложение в Visual Basic (`from` предложение в C#) для выбора всех заказов для клиентов в Лондоне.  
  
 [!code-csharp[DLinqQueryExamples#47](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#47)]
 [!code-vb[DLinqQueryExamples#47](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#47)]  
  
## <a name="example"></a>Пример  
 В следующем примере используется переходы по внешним ключам в `Where` предложение в Visual Basic (`where` предложение в C#) для фильтрации из за `Products` которого `Supplier` находится в США.  
  
 [!code-csharp[DLinqQueryExamples#48](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#48)]
 [!code-vb[DLinqQueryExamples#48](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#48)]  
  
## <a name="example"></a>Пример  
 В следующем примере используется переходы по внешним ключам в `From` предложение в Visual Basic (`from` предложение в C#) для фильтрации сотрудников в Сиэтле и получения списка закрепленных за ними регионов.  
  
 [!code-csharp[DLinqQueryExamples#49](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#49)]  
  
## <a name="example"></a>Пример  
 В следующем примере используется переходы по внешним ключам в `Select` предложение в Visual Basic (`select` предложение в C#) для фильтрации пар сотрудников, в которых один сотрудник сообщает о другом и оба сотрудника находятся в одном `City`.  
  
 [!code-csharp[DLinqQueryExamples#50](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#50)]
 [!code-vb[DLinqQueryExamples#50](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#50)]  
  
## <a name="example"></a>Пример  
 В следующем примере Visual Basic выполняет поиск всех клиентов и заказов, гарантирует, что совпадение заказы для клиентов и гарантирует, что для каждого клиента в этом списке контактное лицо.  
  
 [!code-vb[DLinqQueryExamples#50v](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#50v)]  
  
## <a name="example"></a>Пример  
 В следующем пример явно соединяются две таблицы и проецируются результаты из обеих таблиц.  
  
 [!code-csharp[DLinqQueryExamples#51](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#51)]
 [!code-vb[DLinqQueryExamples#51](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#51)]  
  
## <a name="example"></a>Пример  
 В следующем пример явно соединяются три таблицы и проецируются результаты из каждой таблицы.  
  
 [!code-csharp[DLinqQueryExamples#52](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#52)]
 [!code-vb[DLinqQueryExamples#52](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#52)]  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как реализовать оператор `LEFT OUTER JOIN` с помощью метода `DefaultIfEmpty()`. Если для сотрудника (`DefaultIfEmpty()`) не имеется заказов (`Order`), метод `Employee` возвращает значение NULL.  
  
 [!code-csharp[DLinqQueryExamples#53](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#53)]
 [!code-vb[DLinqQueryExamples#53](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#53)]  
  
## <a name="example"></a>Пример  
 В следующем примере проецируется выражение `let`, полученное в результате соединения.  
  
 [!code-csharp[DLinqQueryExamples#54](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#54)]
 [!code-vb[DLinqQueryExamples#54](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#54)]  
  
## <a name="example"></a>Пример  
 В следующем примере показан оператор `join` с композитным ключом.  
  
 [!code-csharp[DLinqQueryExamples#55](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#55)]
 [!code-vb[DLinqQueryExamples#55](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#55)]  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как создать оператор `join`, в котором одна сторона может принимать значение NULL, а другая сторона не может.  
  
 [!code-csharp[DLinqQueryExamples#56](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#56)]
 [!code-vb[DLinqQueryExamples#56](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#56)]  
  
## <a name="see-also"></a>См. также  
 [Примеры запросов](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)

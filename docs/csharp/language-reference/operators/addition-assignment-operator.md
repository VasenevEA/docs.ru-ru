---
title: Оператор += (справочник по C#)
ms.date: 07/20/2015
f1_keywords:
- +=_CSharpKeyword
helpviewer_keywords:
- += operator [C#]
- addition assignment operator (+=) [C#]
ms.assetid: 9cdf97e6-331d-492b-85e1-3ec3171484e9
ms.openlocfilehash: 90967dcdccfb71995ac83e0dd52ea7bd86f136be
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="-operator-c-reference"></a>Оператор += (справочник по C#)
Оператор присваивания сложения.  
  
## <a name="remarks"></a>Примечания  
 Выражение, использующее оператор присваивания `+=`, такое как  
  
```  
x += y  
```  
  
 эквивалентно  
  
```  
x = x + y  
```  
  
 за исключением того, что `x` вычисляется только один раз. Значение [оператора +](../../../csharp/language-reference/operators/addition-operator.md) зависит от типов операндов `x` и `y` (сложение для числовых операндов, объединение для строковых операндов и т. д.).  
  
 Оператор `+=` нельзя перегружать напрямую, однако пользовательские типы могут перегружать [оператор +](../../../csharp/language-reference/operators/addition-operator.md) (см. [operator](../../../csharp/language-reference/keywords/operator.md)).  
  
 Оператор `+=` также позволяет указать метод, который будет вызываться в ответ на событие. Такие методы называются обработчиками событий. Использование оператора `+=` в таком контексте называется *подпиской на событие*. Дополнительные сведения см. в разделах [Практическое руководство. Подписка и отмена подписки на события](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md) и [Делегаты](../../../csharp/programming-guide/delegates/index.md).  
  
## <a name="example"></a>Пример  
 [!code-csharp[csRefOperators#35](../../../csharp/language-reference/operators/codesnippet/CSharp/addition-assignment-operator_1.cs)]  
  
## <a name="see-also"></a>См. также  
 [Справочник по C#](../../../csharp/language-reference/index.md)  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
 [Операторы в C#](../../../csharp/language-reference/operators/index.md)

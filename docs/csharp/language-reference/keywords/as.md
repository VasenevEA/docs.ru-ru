---
title: as (Справочник по C#)
ms.date: 07/20/2015
f1_keywords:
- as_CSharpKeyword
- as
helpviewer_keywords:
- type conversion [C#], as keyword
- as keyword [C#]
ms.assetid: a9be126b-cbf4-4990-a70d-d0e1983cad0e
ms.openlocfilehash: 6ea5346119259d70ac1a42f3f72a8b2746b8f536
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="as-c-reference"></a>as (Справочник по C#)
Оператор `as` можно использовать для выполнения определенных типов преобразований между совместимыми ссылочными типами или [типами, допускающими значение NULL](../../../csharp/programming-guide/nullable-types/index.md). Вот пример кода:  
  
 [!code-csharp[csrefKeywordsOperator#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/as_1.cs)]  
  
## <a name="remarks"></a>Примечания  
 Оператор `as` аналогичен операции приведения. Однако, если преобразование невозможно, `as` возвращает `null`, а не вызывает исключение. Рассмотрим следующий пример.  
  
```  
expression as type  
```  
  
 Этот код является эквивалентом следующего выражения, за исключением того, что переменная `expression` вычисляется только один раз.  
  
```  
expression is type ? (type)expression : (type)null  
```  
  
 Обратите внимание, что оператор `as` выполняет только преобразования ссылок, преобразования типов, допускающих значение NULL, и преобразования-упаковки. Оператор `as` не может выполнять другие преобразования, например пользовательские преобразования, которые следует выполнять с помощью выражения приведения.  
  
## <a name="example"></a>Пример  
 [!code-csharp[csrefKeywordsOperator#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/as_2.cs)]  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Справочник по C#](../../../csharp/language-reference/index.md)  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
 [Ключевые слова в C#](../../../csharp/language-reference/keywords/index.md)  
 [is](../../../csharp/language-reference/keywords/is.md)  
 [Оператор ?:](../../../csharp/language-reference/operators/conditional-operator.md)  
 [Ключевые слова операторов](../../../csharp/language-reference/keywords/operator-keywords.md)

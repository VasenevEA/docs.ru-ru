---
title: Нельзя включить ссылку на закрытый объект при вызове свойства или функции в качестве аргумента или возвращаемого значения
ms.date: 07/20/2015
f1_keywords:
- vbrID98
ms.assetid: 059b43e1-202d-4fa2-806b-7bad63c1e7ca
ms.openlocfilehash: 1f36526eab1bc0964bf89398b6e0f3e74d09fdc6
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="a-property-or-method-call-cannot-include-a-reference-to-a-private-object-either-as-an-argument-or-as-a-return-value"></a>Нельзя включить ссылку на закрытый объект при вызове свойства или функции в качестве аргумента или возвращаемого значения
Некоторые из возможных причин этой ошибки:  
  
-   клиент вызвал свойство или метод внепроцессного компонента и предпринял попытку передать ссылку на закрытый объект в качестве одного из аргументов;  
  
-   внепроцессный компонент задействовал для клиента метод обратного вызова и предпринял попытку передать ссылку на закрытый объект;  
  
-   внепроцессный компонент предпринял попытку передать ссылку на закрытый объект в качестве аргумента события, которые он вызывал;  
  
-   клиент предпринял попытку назначить ссылку на закрытый объект для аргумента `ByRef` события, которое он обрабатывал.  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
1.  Удалите ссылку.  
  
## <a name="see-also"></a>См. также  
 [Закрытые](../../../visual-basic/language-reference/modifiers/private.md)

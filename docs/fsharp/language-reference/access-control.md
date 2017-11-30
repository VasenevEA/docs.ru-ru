---
title: "Управление доступом (F#)"
description: "Узнайте, как для управления доступом к элементов программирования, таких как типы, методы и функции в языке F #."
keywords: "visual f#, f#, функциональное программирование"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 955b06fe-d1cd-431d-8db6-93e83b697453
ms.openlocfilehash: a02e20a585a0456577901f2762a0eeb0e3ecd2f0
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="access-control"></a>Управление доступом

*Контроль доступа* понимается объявление того, какие клиенты могут использовать определенные элементы программы, например типы, методы и функции.


## <a name="basics-of-access-control"></a>Основы управления доступом
В языке F # описатели управления доступом `public`, `internal`, и `private` может применяться к модули, типы, методы, определений значений, функций, свойств и явные поля.


- `public`Указывает, что сущность может осуществляться все вызывающие объекты.

- `internal`Указывает, что сущность может осуществляться только из той же сборки.

- `private`Указывает, что сущность может осуществляться только из включающего ее типа или модуля.


>[!NOTE] 
Спецификатор доступа `protected` не используется в F #, хотя это приемлемо, если при использовании типов, созданных на языках, которые поддерживают `protected` доступа. Таким образом Если переопределить защищенный метод, этот метод будет доступен только в пределах класса и его потомков.

Как правило, описатель размещается перед именем сущности, за исключением случаев `mutable` или `inline` используется спецификатор, которые записываются после описателя управления доступом.

Если используется спецификатор доступа, значение по умолчанию — `public`, за исключением `let` привязок в типе, которые всегда являются `private` типу.

Подписи в F # предоставляют еще один механизм для управления доступом к элементам программы на F #. Подписи не являются обязательными для управления доступом. Дополнительные сведения см. в статье [Сигнатуры](signatures.md).


## <a name="rules-for-access-control"></a>Правила управления доступом
Управление доступом — это применяются следующие правила:


- Объявления наследования (то есть, использование `inherit` для указания базового класса для класса), объявления интерфейсов (Указание того, что класс реализует интерфейс) и абстрактные члены всегда имеют тот же уровень доступа, включающего их типа. Таким образом спецификатора контроля доступа не может использоваться на этих конструкций.

- Отдельные варианты в размеченного объединения не может иметь собственные модификаторы управления доступом, отдельно от типа объединения.

- Отдельные поля типа записи не может иметь свои собственные модификаторы управления доступом, отдельные от типа записи.


## <a name="example"></a>Пример
Следующий код иллюстрирует использование описателей управления доступом. Существуют два файла в проекте `Module1.fs` и `Module2.fs`. Каждый файл неявно представляет собой модуль. Таким образом, есть два модуля `Module1` и `Module2`. Закрытый тип и внутренний тип определяются в `Module1`. Закрытый тип нельзя получить доступ из `Module2`, но внутреннему типу.

[!code-fsharp[Main](../../../samples/snippets/fsharp/access-control/snippet1.fs)]
    
Следующий код проверяет доступность типов, созданных в `Module1.fs`.

[!code-fsharp[Main](../../../samples/snippets/fsharp/access-control/snippet2.fs)]
    
## <a name="see-also"></a>См. также
[Справочник по языку F#](index.md)

[Сигнатуры](signatures.md)
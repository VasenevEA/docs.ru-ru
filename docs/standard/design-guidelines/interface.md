---
title: Разработка интерфейса
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- interfaces [.NET Framework], design guidelines
- type design guidelines, interfaces
- class library design guidelines [.NET Framework], interfaces
ms.assetid: a016bd18-6710-4358-9438-9f190a295392
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dea5877f952869d5c84d6019617fcdc52d8ee0a5
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="interface-design"></a>Разработка интерфейса
Несмотря на то, что большинство интерфейсов API, лучше всего моделируются с помощью классов и структур, существуют случаи, когда интерфейсы больше подходят или могут использоваться только.  
  
 Среда CLR не поддерживает множественное наследование (т. е. классов CLR, не может наследовать от более чем одного базового класса), но разрешает типы реализовать один или несколько интерфейсов, помимо наследование от базового класса. Таким образом интерфейсы часто используются для создания эффекта множественного наследования. Например <xref:System.IDisposable> — это интерфейс, позволяющий типы для поддержки disposability независимо от других иерархии наследования, в которой хотите участвовать.  
  
 Ситуации, в какой определение подходит интерфейс находится в создании общий интерфейс, который поддерживает несколько типов, включая некоторые типы значений. Типы значений не может наследовать от типов, отличных от <xref:System.ValueType>, но они могут реализовывать интерфейсы, с помощью интерфейса — единственный доступный вариант, чтобы обеспечить общий базовый тип.  
  
 **✓ СДЕЛАТЬ** Определите интерфейс, если требуется, чтобы некоторые общий API, которые должны поддерживаться набор типов, который включает типы значений.  
  
 **✓ Попробуйте** определять интерфейс, если необходима поддержка его функциональные возможности для типов, являющихся производными от другого типа.  
  
 **X ИЗБЕГАЙТЕ** с помощью маркера интерфейсов (интерфейсы без членов).  
  
 Если необходимо пометить класс как имеющий определенных характеристик (маркер), как правило, используйте настраиваемый атрибут, а не интерфейс.  
  
 **✓ СДЕЛАТЬ** укажите по крайней мере один тип, который является реализацией интерфейса.  
  
 Это помогает проверить дизайн интерфейса. Например <xref:System.Collections.Generic.List%601> — это реализация <xref:System.Collections.Generic.IList%601> интерфейса.  
  
 **✓ СДЕЛАТЬ** предоставляют по крайней мере один API, использующий каждый из определенных интерфейсов (метод, принимающий интерфейс как параметр или свойство с типом интерфейса).  
  
 Это помогает проверить дизайн интерфейса. Например <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType> использует <xref:System.Collections.Generic.IComparer%601?displayProperty=nameWithType> интерфейса.  
  
 **X не** добавление членов в интерфейс, который был доставлен.  
  
 Это может нарушить реализаций интерфейса. Чтобы избежать проблемы управления версиями следует создать новый интерфейс.  
  
 За исключением ситуаций, описанных в следующих рекомендаций как правило, выберите классы, а не интерфейсов в разработке повторно используемых библиотек управляемого кода.  
  
 *Фрагменты © 2005, 2009 корпорации Майкрософт. Все права защищены.*  
  
 *Перепечатываются разрешении Пирсона для образовательных учреждений, Inc. из [Framework рекомендации по проектированию: условные обозначения, стили и шаблоны для библиотеки .NET для повторного использования, 2-е издание](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina и Брэд Абрамс, опубликованные 22 октября 2008 г., Addison-Wesley Professional в составе ряда разработки Microsoft Windows.*  
  
## <a name="see-also"></a>См. также  
 [Рекомендации по разработке типов](../../../docs/standard/design-guidelines/type.md)  
 [Рекомендации по проектированию на основе Framework](../../../docs/standard/design-guidelines/index.md)

---
title: Практическое руководство. Определение автоматического реверса для шкалы времени
ms.date: 03/30/2017
helpviewer_keywords:
- AutoReverse property of timelines [WPF]
- Timelines [WPF], AutoReverse property
ms.assetid: 1648dd90-1bee-409a-ac69-ac729867f557
ms.openlocfilehash: 498aefa16b8a76262c01965b8992ef9a94b7ce28
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-specify-whether-a-timeline-automatically-reverses"></a>Практическое руководство. Определение автоматического реверса для шкалы времени
Временная шкала <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> свойство определяет, является ли он воспроизводится в обратном направлении после завершения прямой итерации. В следующем примере показано несколько анимаций с идентичной длительностью и целевые значения, но различными <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> параметры. Чтобы продемонстрировать как <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> свойство ведет себя с различными <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> , некоторые анимации настроек для повторения. Последняя анимация показывает как <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> свойство работает на вложенных временных шкал.  
  
## <a name="example"></a>Пример  
 [!code-xaml[timingbehaviors_snip#AutoReverseAndRepeatBehaviorExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AutoReverseExample.xaml#autoreverseandrepeatbehaviorexamplewholepage)]

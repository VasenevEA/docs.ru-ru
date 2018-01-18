---
title: "Использование модели рабочей области пакета SDK для .NET Compiler Platform"
description: "Данный обзор описывает тип, используемый для отправки запросов к рабочей области и проектам для вашего кода и управления ими."
author: billwagner
ms.author: wiwagn
ms.date: 10/15/2017
ms.topic: conceptual
ms.prod: .net
ms.devlang: devlang-csharp
ms.custom: mvc
ms.openlocfilehash: d0d4e9c012b025b9393ac34f0833795fca9841d5
ms.sourcegitcommit: d095094e942eedf09530ea5636fbaf9029853027
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="work-with-a-workspace"></a>Использование рабочей области

Слой **Рабочие области** является отправной точкой для анализа кода и рефакторинга в рамках целых решений. В этом слое API рабочей области помогает упорядочить всю информацию о проектах в решении в рамках одной объектной модели, предоставляя вам прямой доступ к объектным моделям слоя компилятора, например тексту исходного кода, деревьям синтаксиса, семантическим моделям и компиляциям, без необходимости анализировать файлы, настраивать параметры или управлять зависимостями между проектами. 

Среды размещения, такие как интегрированная среда разработки, предоставляют рабочую область, соответствующую открытому решению. Эту модель можно использовать и вне интегрированной среды разработки, просто загрузив файл решения.

## <a name="workspace"></a>Рабочая область

Рабочая область является активным представлением вашего решения в виде коллекции проектов, каждый из которых содержит коллекцию документов. Рабочая область обычно привязывается к среде размещения, которая постоянно изменяется по мере того, как пользователь вводит или использует свойства. 

<xref:Microsoft.CodeAnalysis.Workspace> предоставляет доступ к текущей модели решения. При возникновении изменения в среде размещения рабочая область выдает соответствующие события, после чего обновляется свойство <xref:Microsoft.CodeAnalysis.Workspace.CurrentSolution?displayProperty=nameWithType>. Например, когда пользовательские типы в текстовом редакторе соответствуют одному из исходных документов, рабочая область использует событие, чтобы сообщить всей модели об изменении решения и измененном документе. После этого вы можете отреагировать на такие изменения, проанализировав новую модель на корректность, выделив значимые области или внеся предложение по изменению кода. 

Кроме того, вы можете создать автономные рабочие области, которые отключены от среды размещения или используются в приложении без такой среды.

## <a name="solutions-projects-documents"></a>Решения, проекты, документы

Хотя рабочая область может меняться при каждом нажатии клавиши, вы можете работать с моделью решения изолированно. 

Решение представляет собой неизменяемую модель проектов и документов. Это означает, что модель можно использовать совместно без блокировки или дублирования. После получения экземпляра решения из свойства <xref:Microsoft.CodeAnalysis.Workspace.CurrentSolution?displayProperty=nameWithType> этот экземпляр больше не меняется. Однако, как и в случае с деревьями синтаксиса и компиляциями, вы можете изменять решения, создавая экземпляры на основе существующих решений и определенных изменений. Чтобы рабочая область отражала ваши изменения, нужно явным образом применить измененное решение обратно к ней.

Проект является частью общей неизменяемой модели решения. Он представляет все документы исходного кода, параметры синтаксического анализа и компиляции, а также ссылки на сборки и ссылки между проектами. Из проекта вы можете обратиться к соответствующей компиляции без необходимости определять зависимости проекта или анализировать исходные файлы.

Документ также является частью общей неизменяемой модели решения. Он представляет один исходный файл, из которого можно обратиться к тексту файла, дереву синтаксиса и семантической модели.

Следующая схема показывает, как рабочая область связана со средой размещения, средствами и способом внесения изменений.

![Связи между различными элементами рабочей области, содержащей проекты и исходные файлы](media/workspace-obj-relations.png)

## <a name="summary"></a>Сводка

Roslyn содержит набор API компиляторов и API рабочих областей, предоставляющий подробные сведения об исходном коде и обеспечивающий полную точность для языков C# и Visual Basic.  Пакет SDK для .NET Compiler Platform значительно сокращает требования к созданию средств и приложений, ориентированных на код. Он предоставляет множество возможностей для инноваций в таких областях, как метапрограммирование, создание и преобразование кода, интерактивное использование языков C# и Visual Basic, а также их внедрение в доменные языки.  
---
title: Практическое руководство. Добавление ссылок на библиотеки типов
ms.date: 03/30/2017
helpviewer_keywords:
- importing type library
- interop assemblies, generating
- type libraries
- COM interop, importing type library
ms.assetid: f5cfa6ba-cc25-4017-82cd-ba7391859113
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 03c05e7399e9378751f803ae56dfaf664490e6d8
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-add-references-to-type-libraries"></a>Практическое руководство. Добавление ссылок на библиотеки типов
При добавлении ссылки на библиотеку типов Visual Studio генерирует сборку взаимодействия, в которой содержатся метаданные. Если первичная сборка взаимодействия доступна, Visual Studio обращается к существующей сборке, прежде чем генерировать новую.  
  
### <a name="to-add-a-reference-to-a-type-library-in-visual-studio"></a>Добавление ссылки на библиотеку типов в Visual Studio  
  
1.  Если файл Windows Setup.exe не осуществит установку автоматически, установите DLL- или EXE-файл COM на компьютер.  
  
2.  Выберите **Проект**, **Добавить ссылку**.  
  
3.  В диспетчере ссылок выберите **COM**.  
  
4.  Выберите библиотеку типов из списка или найдите файл с расширением .TLB.  
  
5.  Нажмите кнопку **ОК**.  
  
6.  В обозревателе решений откройте контекстное меню добавленной ссылки и выберите **Свойства**.  
  
7.  Убедитесь, что в окне **Свойства** свойству **Внедрить типы взаимодействия** присвоено значение **True**. Visual Studio внедрит информацию о типах COM в исполняемые файлы, устранив тем самым необходимость развертывать основные сборки взаимодействия в приложении.  
  
> [!NOTE]
>  Пункты меню и параметры диалогового окна зависят от используемой версии Visual Studio.  
  
### <a name="to-add-a-reference-to-a-type-library-for-command-line-compilation"></a>Добавление ссылки на библиотеку типов для компиляции командной строки  
  
1.  Создайте сборку взаимодействия, как описывается в разделе [Практическое руководство. Создание сборок взаимодействия из библиотек типов](how-to-generate-interop-assemblies-from-type-libraries.md).  
  
2.  Для внедрения информации о типах COM в исполняемые файлы используйте параметр компилятора [/link (параметры компилятора C#)](../../csharp/language-reference/compiler-options/link-compiler-option.md) или [/link (Visual Basic)](../../visual-basic/reference/command-line-compiler/link.md) с именем сборки взаимодействия.  
  
## <a name="see-also"></a>См. также  
 [Импорт библиотеки типов в виде сборки](importing-a-type-library-as-an-assembly.md)  
 [Предоставление COM-компонентов платформе .NET Framework](exposing-com-components.md)  
 [Пошаговое руководство. Внедрение данных о типе из сборок для приложений Microsoft Office](https://msdn.microsoft.com/library/85b55e05-bc5e-4665-b6ae-e1ada9299fd3(v=vs.100))  
 [Пошаговое руководство. Внедрение данных о типах из управляемых сборок](https://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)  
 [/link (параметры компилятора C#)](../../csharp/language-reference/compiler-options/link-compiler-option.md)  
 [/link (Visual Basic)](../../visual-basic/reference/command-line-compiler/link.md)

---
title: "Winres.exe (редактор ресурсов Windows Forms) | Документация Microsoft"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Winres.exe
- Windows Forms Resource Editor
- localization
- Windows Forms, localization
- forms, localizing
- resx files
- .resx files
ms.assetid: cb8bc835-9221-4888-af53-1a4f5fad6c48
caps.latest.revision: 23
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 2149e21f82b224e40cc4b2dd80a7decd9988385d
ms.contentlocale: ru-ru
ms.lasthandoff: 06/02/2017

---
# <a name="winresexe-windows-forms-resource-editor"></a>Winres.exe (редактор ресурсов Windows Forms)
Редактор ресурсов Windows Forms (Winres.exe) — это программа визуальной разметки, используемая при локализации ресурсов пользовательского интерфейса Windows Forms. Файлы RESX и RESOURCES, используемые как входные для программы Winres.exe, могут быть созданы с использованием среды визуального проектирования, такой как Microsoft Visual Studio. Информацию о развертывании ресурсов в приложениях .NET Framework см. в разделе [Ресурсы в приложениях для настольных систем](../../../docs/framework/resources/index.md).  
  
 Эта программа автоматически устанавливается вместе с Visual Studio. Чтобы применить этот инструмент, воспользуйтесь командной строкой разработчика (или командной строкой Visual Studio в Windows 7). Дополнительные сведения см. в разделе [Командные строки](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 В командной строке введите следующее.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
winres resourceFile   
winres /?   
```  
  
## <a name="remarks"></a>Примечания  
  
|Аргумент|Описание|  
|--------------|-----------------|  
|`resourceFile`|Файл ресурсов, который требуется локализовать. Это должен быть файл ресурсов Windows Forms с расширением RESX или RESOURCES, созданный с помощью конструктора Visual Studio. Программа Winres.exe не может открывать универсальные RESX-файлы и RESOURCES-файлы.|  
  
|Параметр|Описание|  
|------------|-----------------|  
|**/?**|Отображает синтаксис команд и параметров программы.|  
  
 Состояние элементов пользовательского интерфейса формы в проекте Windows Forms обычно хранится в файлах ресурсов — файлах на основе XML с расширением RESX или соответствующих им скомпилированных двоичных версиях с расширением RESOURCES. Программа Winres.exe предоставляет ограниченные возможности редактирования файлов обоих типов вне среды разработки Visual Studio. В частности, она поддерживает следующие виды операций редактирования.  
  
-   Предусмотрено редактирование файла ресурсов, зависящего или не зависящего от языка и региональных параметров, для изменения свойств пользовательского интерфейса формы или ее элементов управления, например текста, размера или положения.  
  
-   Можно создавать файлы ресурсов, зависящие или не зависящие от языка и региональных параметров, из файла ресурсов по умолчанию.  
  
-   Файл ресурсов определенного языка и региональных параметров можно сохранить в виде файла ресурсов другого языка региональных параметров. Например, файл ресурсов английского языка (США) можно сохранить как файл ресурсов польского языка. Обычно новый файл требует дополнительного редактирования для приведения в соответствие новому языку и региональным параметрам.  
  
 Также см. раздел [Иерархическая организация ресурсов для локализации](http://msdn.microsoft.com/library/756hydy4\(v=vs.110\)) или [Иерархическая организация ресурсов для локализации](http://msdn.microsoft.com/library/756hydy4\(v=vs.120\)).  
  
 Программа Winres.exe не может преобразовать RESX-файл в соответствующий ему RESOURCES-файл, для этого используется программа Resgen.exe. Дополнительные сведения о программе Resgen.exe см. в разделе [Resgen.exe (генератор файлов ресурсов)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md).  
  
 Программа Winres.exe представляет собой графическое приложение, которое воссоздает форму Windows Forms в виде версии этапа разработки, используя лишь файл ресурсов, без доступа к исходному коду. Интерфейс программы Winres.exe включает конструктор форм Windows Forms из Visual Studio и окно свойств. Такой подход позволяет визуально редактировать RESOURCES-файл или RESX-файл, содержащий форму Windows Forms. Обычно программа Winres.exe используется для редактирования подписей элементов управления и настройки их расположения и размера, чтобы они могли вместить подписи на требуемом языке.  
  
 Если программа Winres.exe не может разрешить какой-либо тип элемента управления, она создает его прототип в локализованном файле RESX или RESOURCES. Прототип элемента управления отображается в форме Windows Forms в виде заштрихованного окна. Размер и расположение заштрихованного окна совпадают с размером и расположением самого элемента управления. Все доступные для локализации свойства прототипа элемента управления показаны в окне "Свойства". Все изменения, внесенные в прототип, сохраняются в самом элементе управления.  
  
## <a name="winresexe-versus-visual-studio"></a>Сравнение программы Winres.exe со средой Visual Studio  
 Обычно, прежде чем приступать к локализации форм Windows Forms для приложения, необходимо выбрать инструмент локализации: Visual Studio или программа Winres.exe. Свободное переключение между этими двумя инструментами для локализации может быть невозможно из-за проблем совместимости версий, описанных ниже.  
  
 Преимущество среды Visual Studio заключается в том, что ее можно использовать как для разработки приложения, так и для его локализации. Чтобы локализовать форму после ее разработки, задайте значение `true` для свойства <xref:System.ComponentModel.LocalizableAttribute> (свойство **Localizable** в редакторе свойств) и значение, соответствующее требуемому языку локализации, для свойства **Language**. Затем необходимо отредактировать строки и настроить расположение и размер элементов управления таким образом, чтобы они смогли вместить строки на языке локализации. Среда Visual Studio при сохранении локализованного RESX-файла записывает в него только локализуемые свойства (изменяющиеся на языке локализации). Среда Visual Studio автоматически создает в нужном каталоге вспомогательную сборку для локализованного RESX-файла.  Также см. раздел [Пошаговое руководство. Локализация форм Windows Forms](http://msdn.microsoft.com/library/y99d1cd3\(v=vs.110\)).  
  
 Хотя Visual Studio обеспечивает интегрированную среду разработки и локализации, сторонним локализаторам рекомендуется использовать программу Winres.exe. Так как программа Winres.exe предназначена только для локализации, она позволяет более четко отделить код приложения от локализуемых форм, что лучше подходит для управления большими проектами.  
  
## <a name="using-winresexe"></a>Использование программы Winres.exe  
 Чтобы выполнить локализацию с помощью программы Winres.exe, необходимо сначала разработать приложение с помощью визуального конструктора, такого как конструктор форм Visual Studio. По завершении разработки присвойте свойству <xref:System.ComponentModel.LocalizableAttribute> данной формы (свойство **Localizable`true` в редакторе свойств) значение**  и передайте стороннему локализатору RESX-файл с языком и региональными параметрами по умолчанию. Такой RESX-файл содержит дополнительные сведения, которые программа Winres.exe использует для воссоздания версии исходной формы, соответствующей времени разработки.  
  
> [!CAUTION]
>  Программу Winres.exe нельзя использовать для редактирования файла ресурсов по умолчанию. Программа Winres.exe интерпретирует все измененные свойства как локализованные и сохраняет их в файле ресурсов на языке локализации.  
  
 Окончательные версии файлов ресурсов на языке локализации могут в итоге быть использованы для создания локализованных версий приложения. Дополнительные сведения см. в разделе [Ресурсы в приложениях для настольных систем](../../../docs/framework/resources/index.md).  
  
 Программа Winres.exe версии 2.0 поддерживает следующие возможности и возможности.  
  
-   Программа Winres может работать в режиме одного файла (SFM) или в режиме файлов Visual Studio (VSFM). SFM — это устаревший режим, предусматривающий хранение всей информации о форме и ее содержимом в файле ресурсов. В режиме VSFM в файле ресурсов хранятся только изменения, связанные с языком и региональными параметрами.  
  
-   В интерфейс добавлено окно сообщений об ошибках, находящееся в левом нижнем углу основного окна.  
  
-   С помощью команды **Проверить сочетания клавиш** в меню "Формат" можно проверить наличие дублирующихся сочетаний клавиш.  
  
## <a name="version-compatibility"></a>Совместимость версий  
 Поскольку формат файлов ресурсов Visual Studio 2005 изменился в сравнении с Visual Studio .NET 2002, в программу Winres.exe также были внесены соответствующие изменения для обеспечения совместимости. Поэтому рекомендуется использовать версию Winres.exe, выпущенную вместе с платформой .NET Framework, которая используется для создания приложения. В таблице ниже представлен список совместимых версий.  
  
|Visual Studio|.NET Framework|Winres.exe|  
|-------------------|--------------------|----------------|  
|Visual Studio .NET 2002|1,0|1,0|  
|Visual Studio .NET 2003|1.1|1.1|  
|Visual Studio 2005|2.0|2.0|  
|Visual Studio 2008|3.0 и 3.5|3.0 и 3.5|  
|Visual Studio 2010|4.0|4.0|  
  
 При попытке открыть старый файл ресурсов с помощью Winres.exe 2.0 будет предложено обновить формат файла для совместимости с версией .NET Framework 2.0.  
  
 В версиях .NET Framework, предшествовавших версии 2.0, программа Winres.exe и конструктор форм Visual Studio создавали несовместимые файлы ресурсов (как зависящие, так и не зависящие от языка и региональных параметров). Поэтому, после начала локализации приходилось использовать только один инструмент. Однако в программе Winres.exe версии 2.0 была добавлена поддержка режима файлов Visual Studio (VSFM). Как следует из названия, файл ресурсов, сохраненный в этом режиме совместимости, можно редактировать любым из двух инструментов.  
  
> [!NOTE]
>  Режим VSFM обладает преимуществом в плане совместимости с Visual Studio, но поскольку в этом режиме в файле ресурсов хранятся только измененные значения, для программы Winres.exe требуется, чтобы в каталоге текущего файла ресурсов располагались и его родительские файлы. Например, при редактировании немецкоязычного файла ресурсов `TestApp.de-DE.resources` необходимо наличие файла ресурсов по умолчанию `TestApp.resx`, а также, возможно, не зависящего от языка файла ресурсов `TestApp.de.resources`.  
  
## <a name="examples"></a>Примеры  
  
#### <a name="to-localize-a-resx-or-resources-file-associated-with-a-form"></a>Локализация файла RESX или RESOURCES, связанного с формой  
  
1.  Чтобы запустить программу Winres.exe, введите в командной строке разработчика `winres`.  
  
2.  Чтобы открыть ресурсы по умолчанию для локализуемой формы, выберите команду **Открыть** в меню **Файл** и найдите нужный файл.  
  
     -или-  
  
     При запуске программы Winres.exe в командной строке укажите файл, который требуется открыть.  
  
     Следующая команда запускает программу Winres.exe и загружает форму, связанную с файлом `TestApp.resx`, в конструктор форм.  
  
    ```  
    winres TestApp.resx  
    ```  
  
     Следующая команда запускает программу Winres.exe и загружает форму, связанную с файлом `TestApp.resources`, в конструктор форм.  
  
    ```  
    winres TestApp.resources  
    ```  
  
    > [!NOTE]
    >  Если форма, ресурсы которой редактируются, является унаследованной, необходимо, чтобы и сборка, содержавшая исходную форму, и сборка, содержащая наследующую (производную) форму, были зарегистрированы в глобальном кэше сборок или располагались в том же каталоге, что и программа WinRes.exe. Дополнительные сведения об установке компонентов .NET Framework в глобальный кэш сборок см. в разделе [Глобальный кэш сборок](../../../docs/framework/app-domains/gac.md).  
  
3.  Выберите элементы управления в форме и измените значения их свойства <xref:System.Windows.Forms.Control.Text%2A> и других свойств в соответствии с языком локализации и региональными параметрами. Переместите элементы управления или измените их размер, чтобы вместить локализованный текст.  
  
4.  Чтобы сохранить локализованную версию файла RESX или RESOURCES, щелкните значок **Сохранить** или выберите команду с тем же именем в меню **Файл**. Откроется окно **Выбор языка и региональных параметров**.  
  
5.  Выберите нужный язык и файловый режим и нажмите кнопку **ОК**. Программа сохранит файл, используя правила присвоения имен, которые среда выполнения требует применять к локализованным файлам ресурсов. Например, при локализации файла `TestApp.resources` на немецкий язык (Германия) этот файл будет сохранен как `TestApp.de-DE.resources`. При локализации файла `TestApp.resx` на немецкий язык (Германия) файл сохраняется как `TestApp.de-DE.resx`. Подробнее о соглашениях об именовании ресурсов см. в разделе [Упаковка и развертывание ресурсов](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md). Список предварительно определенных названий языков, используемых средой выполнения, см. в разделе [Класс CultureInfo](https://msdn.microsoft.com/en-us/library/system.globalization.cultureinfo.aspx).  
  
## <a name="see-also"></a>См. также  
 <xref:System.ComponentModel.LocalizableAttribute>   
 <xref:System.Globalization.CultureInfo>   
 <xref:System.Resources.ResourceManager>   
 <xref:System.Resources.ResourceReader>   
 <xref:System.Resources.ResourceWriter>   
 [Инструменты](../../../docs/framework/tools/index.md)   
 [Ресурсы в приложениях для настольных систем](../../../docs/framework/resources/index.md)   
 [Глобализация и локализация](../../../docs/standard/globalization-localization/index.md)
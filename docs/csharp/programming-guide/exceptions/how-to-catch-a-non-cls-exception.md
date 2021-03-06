---
title: Практическое руководство. Перехват несовместимого с CLS исключения
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions [C#], non-CLS
ms.assetid: db4630b3-5240-471a-b3a7-c7ff6ab31e8d
ms.openlocfilehash: 6169f4b6de2efdfed0dbf43272d708c47b46dbca
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-catch-a-non-cls-exception"></a>Практическое руководство. Перехват несовместимого с CLS исключения
Некоторые языки .NET, включая C++/CLI, позволяют объектам вызывать исключения, которые не являются производными от <xref:System.Exception>. Такие исключения называются *несовместимыми с CLS исключениями* или *необработанными исключениями*. В Visual C# невозможно вызвать несовместимые с CLS исключения, однако можно перехватить их следующими двумя способами.  
  
-   В блоке `catch (Exception e)` как <xref:System.Runtime.CompilerServices.RuntimeWrappedException>.  
  
     По умолчанию сборка Visual C# перехватывает несовместимые с CLS исключения как заключенные в оболочку. Этот метод следует использовать, если требуется доступ к исходному исключению, который можно получить с помощью свойства <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A>. Далее в этом разделе описывается процедура перехвата исключений таким способом.  
  
-   В общем блоке перехвата (блоке перехвата, для которого не указан тип исключения), который помещается после блока `catch (Exception)` или `catch (Exception e)`.  
  
     Используйте этот способ, если требуется выполнить какое-либо действие (например, запись в файл журнала) в ответ на несовместимые с CLS исключения, и вам не нужен доступ к сведениям об исключении. По умолчанию среда CLR создает оболочку для всех исключений. Чтобы отключить этот режим, добавьте этот атрибут уровня сборки в код, как правило, в файле AssemblyInfo.cs: `[assembly: RuntimeCompatibilityAttribute(WrapNonExceptionThrows = false)]`.  
  
### <a name="to-catch-a-non-cls-exception"></a>Перехват несовместимого с CLS исключения  
  
1.  В `catch(Exception e) block` используйте ключевое слово `as`, чтобы проверить, может ли `e` приводиться к <xref:System.Runtime.CompilerServices.RuntimeWrappedException>.  
  
2.  Для доступа к исходному исключению используйте свойство <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A>.  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как перехватить несовместимое с CLS исключение, которое было вызвано из библиотеки классов, написанной на C++/CLR. Обратите внимание, что в этом примере клиентскому коду Visual C# заранее известно, что тип вызываемого исключения — <xref:System.String?displayProperty=nameWithType>. Можно привести свойство <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A> к его исходному типу, если этот тип доступен из кода.  
  
```  
// Class library written in C++/CLR.  
   ThrowNonCLS.Class1 myClass = new ThrowNonCLS.Class1();  
  
   try  
   {  
    // throws gcnew System::String(  
    // "I do not derive from System.Exception!");  
    myClass.TestThrow();   
   }  
  
   catch (Exception e)  
   {  
    RuntimeWrappedException rwe = e as RuntimeWrappedException;  
    if (rwe != null)      
    {  
      String s = rwe.WrappedException as String;  
      if (s != null)  
      {  
        Console.WriteLine(s);  
      }  
    }  
    else  
    {  
       // Handle other System.Exception types.  
    }  
   }             
```  
  
## <a name="see-also"></a>См. также  
 <xref:System.Runtime.CompilerServices.RuntimeWrappedException>  
 [Исключения и обработка исключений](../../../csharp/programming-guide/exceptions/index.md)

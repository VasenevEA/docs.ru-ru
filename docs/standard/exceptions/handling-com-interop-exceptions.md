---
title: Обработка исключений COM-взаимодействия
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- unmanaged code, exceptions
- exceptions, unmanaged code
- HRESULTs
- exceptions, COM interop
- COM interop, exceptions
ms.assetid: e6104aa8-8e5f-4069-b864-def85579c96c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9f4429d50f6b7646cb75fad44957a98812282928
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="handling-com-interop-exceptions"></a>Обработка исключений COM-взаимодействия
При обработке исключений управляемый и неуправляемый код может работать совместно. Если метод вызывает исключение в управляемом коде, то среда CLR может передать значение HRESULT в COM-объект. Если сбой метода происходит в неуправляемом коде и возвращается значение HRESULT, указывающее на сбой, то среда выполнения создает исключение, которое может быть перехвачено управляемым кодом.  
  
 Среда выполнения автоматически сопоставляет значение HRESULT из COM-взаимодействия с более конкретными исключениями. Например, E_ACCESSDENIED становится <xref:System.UnauthorizedAccessException>, E_OUTOFMEMORY становится <xref:System.OutOfMemoryException> и т. д.  
  
 Если значение HRESULT является пользовательским результатом или неизвестно среде выполнения, то она передает клиенту универсальное исключение <xref:System.Runtime.InteropServices.COMException>. Свойство **ErrorCode** исключения **COMException** содержит значение HRESULT.  
  
## <a name="working-with-ierrorinfo"></a>Работа с IErrorInfo  
 При передаче ошибки из COM в управляемый код среда выполнения заносит в объект исключения сведения об ошибке. COM-объекты, поддерживающие IErrorInfo и возвращающие HRESULTS, предоставляют эти сведения в исключения управляемого кода. Например, среда выполнения сопоставляет описание из ошибки COM со свойством <xref:System.Exception.Message%2A> исключения. Если HRESULT не предоставляет дополнительных сведений об ошибке, то среда выполнения заполняет значительную часть свойств исключения значениями по умолчанию.  
  
 Если сбой метода произошел в неуправляемом коде, то исключение может быть передано в сегмент управляемого кода. В разделе [Сопоставление значений HRESULT и исключений](../../../docs/framework/interop/how-to-map-hresults-and-exceptions.md) представлена таблица, в которой показано сопоставление значений HRESULT с объектами исключений среды выполнения.  

## <a name="see-also"></a>См. также
[Исключения](index.md) 

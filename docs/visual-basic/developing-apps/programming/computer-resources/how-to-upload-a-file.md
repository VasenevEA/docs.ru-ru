---
title: "Практическое руководство. Передача файла в Visual Basic"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- networks, uploading files
- files [Visual Basic], uploading
- uploading files [Visual Basic]
- UploadFile method [Visual Basic]
- My.Computer.Network.UploadFile method
ms.assetid: a8b37924-c523-4fd3-b5ca-cb0074df29cd
caps.latest.revision: "22"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 8a0fab9b812ddff1f56e9fa203bd297fd70bc47d
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-upload-a-file-in-visual-basic"></a>Практическое руководство. Передача файла в Visual Basic
Метод <xref:Microsoft.VisualBasic.Devices.Network.UploadFile%2A> можно использовать для отправки файла и сохранения его в удаленном расположении. Если для параметра `ShowUI` установлено значение `True`, отображается диалоговое окно, показывающее ход загрузки и позволяющее пользователю отменить операцию.  
  
### <a name="to-upload-a-file"></a>Передача файла  
  
-   Для передачи файла используйте метод `UploadFile`, указав расположение исходного файла и каталога назначения в виде строки или URI. В этом примере файл `Order.txt` передается на веб-узел `http://www.cohowinery.com/uploads.aspx`.  
  
     [!code-vb[VbResourceTasks#6](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-upload-a-file_1.vb)]  
  
### <a name="to-upload-a-file-and-show-the-progress-of-the-operation"></a>Передача файла с отображением хода выполнения операции  
  
-   Для передачи файла используйте метод `UploadFile`, указав расположение исходного файла и каталога назначения в виде строки или URI. В этом примере файл `Order.txt` передается на веб-узел `http://www.cohowinery.com/uploads.aspx` без указания имени пользователя или пароля, при этом отображается ход передачи. Время ожидания равно 500 миллисекундам.  
  
     [!code-vb[VbResourceTasks#7](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-upload-a-file_2.vb)]  
  
### <a name="to-upload-a-file-supplying-a-user-name-and-password"></a>Передача файла с указанием имени пользователя и пароля  
  
-   Для передачи файла используйте метод `UploadFile`, указав расположение исходного файла и каталога назначения в виде строки или URI, а также имя пользователя и пароль. В этом примере файл `Order.txt` передается на веб-узел `http://www.cohowinery.com/uploads.aspx` с указанием имени пользователя `anonymous` и пустого пароля.  
  
     [!code-vb[VbResourceTasks#8](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-upload-a-file_3.vb)]  
  
## <a name="robust-programming"></a>Отказоустойчивость  
 Исключение может возникнуть при следующих условиях:  
  
-   Недопустимый путь к локальному файлу (<xref:System.ArgumentException>).  
  
-   Сбой проверки подлинности (<xref:System.Security.SecurityException>).  
  
-   Время ожидания соединения истекло (<xref:System.TimeoutException>).  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.VisualBasic.Devices.Network?displayProperty=nameWithType>  
 <xref:Microsoft.VisualBasic.Devices.Network.UploadFile%2A>  
 [Практическое руководство. Скачивание файла](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-download-a-file.md)  
 [Практическое руководство. Анализ путей к файлам](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)

---
title: Практическое руководство. Создание новых параметров во время разработки
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], design time
- application settings [Windows Forms], creating
ms.assetid: c5d60a66-6507-462f-a81f-e3bc0a804e16
ms.openlocfilehash: 618355948578bd8f15e8cf7bec6f599e3169b77a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-create-a-new-setting-at-design-time"></a>Практическое руководство. Создание новых параметров во время разработки
Можно создать новый параметр во время разработки с помощью конструктора параметров. Конструктор параметров является интерфейсом стиль сетки, который позволяет создавать новые параметры и указывать свойства для этих параметров. Необходимо указать имя, значение, тип и область для новых параметров. После создания параметр становится доступен в коде.  
  
### <a name="to-create-a-new-setting-at-design-time-in-c"></a>Чтобы создать новый параметр во время разработки в C#  
  
1.  В **обозревателе решений**, разверните **свойства** узле проекта.  
  
2.  Дважды щелкните файл с расширением Settings, в которой требуется добавить новый параметр. Является именем по умолчанию для этого файла Settings.settings.  
  
3.  В конструкторе параметров задайте имя, значение, тип и область для этого параметра. Каждая строка представляет один параметр.  
  
### <a name="to-create-a-new-setting-at-design-time-in-visual-basic"></a>Чтобы создать новый параметр во время разработки в Visual Basic  
  
1.  В **обозревателе решений**, щелкните правой кнопкой мыши узел проекта и выберите **свойства**.  
  
2.  В **свойства** выберите **параметры** вкладки.  
  
3.  В конструкторе параметров задайте имя, значение, тип и область для этого параметра. Каждая строка представляет один параметр.  
  
## <a name="see-also"></a>См. также  
 [Использование параметров приложения и параметров пользователя](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)  
 [Общие сведения о параметрах приложений](../../../../docs/framework/winforms/advanced/application-settings-overview.md)  
 [Практическое руководство. Изменение значения существующего параметра во время разработки](../../../../docs/framework/winforms/advanced/how-to-change-the-value-of-an-existing-setting-at-design-time.md)

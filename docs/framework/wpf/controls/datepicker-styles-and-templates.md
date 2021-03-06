---
title: DatePicker стили и шаблоны
ms.date: 03/30/2017
helpviewer_keywords:
- ControlTemplate [WPF], DatePicker
- DatePicker [WPF], styles and templates
- templates [WPF], DatePicker
- parts [WPF], DatePicker
- styles [WPF], DatePicker
- states [WPF], DatePicker
ms.assetid: c430a657-692f-44bd-a549-2341f92d6115
ms.openlocfilehash: 5123cf0ef78d46f5cec30109a34c17eaabe13b38
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="datepicker-styles-and-templates"></a>DatePicker стили и шаблоны
В этом разделе описываются стили и шаблоны для <xref:System.Windows.Controls.DatePicker> элемента управления. Можно изменить значение по умолчанию <xref:System.Windows.Controls.ControlTemplate> для предоставления уникального внешнего вида элемента управления. Подробнее см. в разделе [Настройка внешнего вида существующего элемента управления путем создания объекта ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## <a name="datepicker-parts"></a>DatePicker частей  
 В следующей таблице перечислены именованные части <xref:System.Windows.Controls.DatePicker> элемента управления.  
  
|Отделение|Тип|Описание|  
|-|-|-|  
|PART_Root|<xref:System.Windows.Controls.Grid>|Корневой элемент управления.|  
|PART_Button|<xref:System.Windows.Controls.Button>|Кнопки, которая открывает и закрывает <xref:System.Windows.Controls.Calendar>.|  
|PART_TextBox|<xref:System.Windows.Controls.Primitives.DatePickerTextBox>|Текстовое поле для ввода даты.|  
|PART_Popup|<xref:System.Windows.Controls.Primitives.Popup>|Контекстное меню для <xref:System.Windows.Controls.DatePicker> элемента управления.|  
  
## <a name="datepicker-states"></a>DatePicker состояний  
 В следующей таблице перечислены визуальные состояния <xref:System.Windows.Controls.DatePicker> элемента управления.  
  
|Имя VisualState|Имя VisualStateGroup|Описание|  
|-|-|-|  
|Норм.|CommonStates|Состояние по умолчанию.|  
|Отключено|CommonStates|<xref:System.Windows.Controls.DatePicker> Отключена.|  
|Valid|ValidationStates|Элемент управления использует <xref:System.Windows.Controls.Validation> класса и <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> вложенное свойство `false`.|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Вложенное свойство `true` имеет элемент управления имеет фокус.|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Вложенное свойство `true` имеет элемент управления имеет фокус.|  
  
## <a name="datepickertextbox-parts"></a>DatePickerTextBox частей  
 В следующей таблице перечислены именованные части <xref:System.Windows.Controls.Primitives.DatePickerTextBox> элемента управления.  
  
|Отделение|Тип|Описание|  
|-|-|-|  
|PART_Watermark|<xref:System.Windows.Controls.ContentControl>|Элемент, который содержит исходный текст в <xref:System.Windows.Controls.DatePicker>.|  
|PART_ContentElement|<xref:System.Windows.FrameworkElement>|Визуальный элемент, который может содержать <xref:System.Windows.FrameworkElement>. Текст <xref:System.Windows.Controls.TextBox> отображается в этом элементе.|  
  
## <a name="datepickertextbox-states"></a>DatePickerTextBox состояний  
 В следующей таблице перечислены визуальные состояния <xref:System.Windows.Controls.Primitives.DatePickerTextBox> элемента управления.  
  
|Имя VisualState|Имя VisualStateGroup|Описание|  
|-|-|-|  
|Норм.|CommonStates|Состояние по умолчанию.|  
|Отключено|CommonStates|<xref:System.Windows.Controls.Primitives.DatePickerTextBox> Отключена.|  
|MouseOver|CommonStates|Указатель мыши наведен на <xref:System.Windows.Controls.Primitives.DatePickerTextBox>.|  
|ReadOnly|CommonStates|Пользователь не может изменить текст в <xref:System.Windows.Controls.Primitives.DatePickerTextBox>.|  
|Focused|FocusStates|Элемент управления имеет фокус.|  
|Без фокуса ввода|FocusStates|Элемент управления не имеет фокуса.|  
|Водяные знаки|WatermarkStates|Элемент управления отображает начальный текст.  <xref:System.Windows.Controls.Primitives.DatePickerTextBox> Находится в состоянии, когда пользователь не ввел текст и не выбрал дату.|  
|Unwatermarked|WatermarkStates|Пользователь ввел текст в <xref:System.Windows.Controls.Primitives.DatePickerTextBox> или выбрал дату в <xref:System.Windows.Controls.DatePicker>.|  
|Valid|ValidationStates|Элемент управления использует <xref:System.Windows.Controls.Validation> класса и <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> вложенное свойство `false`.|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Вложенное свойство `true` имеет элемент управления имеет фокус.|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Вложенное свойство `true` имеет элемент управления имеет фокус.|  
  
## <a name="datepicker-controltemplate-example"></a>Пример шаблона элемента управления DatePicker  
 В следующем примере показан способ определения <xref:System.Windows.Controls.ControlTemplate> для <xref:System.Windows.Controls.DatePicker> элемента управления.  
  
 [!code-xaml[ControlTemplateExamples#DatePicker](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datepicker.xaml#datepicker)]  
  
 В предыдущем примере используется один или несколько из следующих ресурсов.  
  
 [!code-xaml[ControlTemplateExamples#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 Полный пример см. в разделе [Пример задания стиля с помощью ControlTemplates](http://go.microsoft.com/fwlink/?LinkID=160041).  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.FrameworkElement.Style%2A>  
 <xref:System.Windows.Controls.ControlTemplate>  
 [Стили и шаблоны элемента управления](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)  
 [Настройка элементов управления](../../../../docs/framework/wpf/controls/control-customization.md)  
 [Стилизация и использование шаблонов](../../../../docs/framework/wpf/controls/styling-and-templating.md)  
 [Настройка внешнего вида существующего элемента управления путем создания объекта ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)

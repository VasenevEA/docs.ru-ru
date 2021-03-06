---
title: ICorDebugClass интерфейс1
ms.date: 03/30/2017
api_name:
- ICorDebugClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass
helpviewer_keywords:
- ICorDebugClass interface [.NET Framework debugging]
ms.assetid: 03a6facb-f12f-49be-9839-e73b9c791cd5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bec35babec96da5ca5d527b19f853b4ce1c384e8
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugclass-interface1"></a>ICorDebugClass интерфейс1
Представляет тип, который может быть базовым или сложным (иными словами, пользовательским). Если тип универсальный, `ICorDebugClass` представляет универсальный тип, у которого отсутствуют экземпляры.  
  
## <a name="methods"></a>Методы  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод GetModule](../../../../docs/framework/unmanaged-api/debugging/icordebugclass-getmodule-method.md)|Возвращает модуль, в котором определен этот класс.|  
|[Метод GetStaticFieldValue](../../../../docs/framework/unmanaged-api/debugging/icordebugclass-getstaticfieldvalue-method.md)|Получает значение указанного статического поля.|  
|[Метод GetToken](../../../../docs/framework/unmanaged-api/debugging/icordebugclass-gettoken-method.md)|Возвращает `TypeDef` токен метаданных для этого класса.|  
  
## <a name="remarks"></a>Примечания  
 `ICorDebugClass` Интерфейс представляет универсальный тип, у которого отсутствуют экземпляры. Интерфейс ICorDebugType представляет экземпляр универсального типа. Например `Hashtable<K, V>` будут представлены в `ICorDebugClass`, тогда как `Hashtable<Int32, String>` будут представлены в `ICorDebugType`.  
  
 Неуниверсальные типы представлены как `ICorDebugClass` и `ICorDebugType`. Последний интерфейс впервые появился в .NET Framework версии 2.0 для создания экземпляров типов.  
  
> [!NOTE]
>  Этот интерфейс не поддерживает удаленные вызовы между компьютерами или между процессами.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Интерфейсы отладки](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)

---
title: Функция CreateAssemblyEnum
ms.date: 03/30/2017
api_name:
- CreateAssemblyEnum
api_location:
- fusion.dll
- clr.dll
- mscorwks.dll
api_type:
- DLLExport
f1_keywords:
- CreateAssemblyEnum
helpviewer_keywords:
- CreateAssemblyEnum function [.NET Framework fusion]
ms.assetid: 3506df38-6cea-42f6-946e-4287863bcfb3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b2098d5d9ce1c01f232cf2904c1fd3e990dfbe2e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="createassemblyenum-function"></a>Функция CreateAssemblyEnum
Возвращает указатель на [IAssemblyEnum](../../../../docs/framework/unmanaged-api/fusion/iassemblyenum-interface.md) экземпляр, предназначенный для перечисления объектов в сборке с указанным [IAssemblyName](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-interface.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT CreateAssemblyEnum (  
    [out] IAssemblyEnum  **pEnum,  
    [in]  IUnknown       *pUnkReserved,  
    [in]  IAssemblyName  *pName,  
    [in]  DWORD          dwFlags,  
    [in]  LPVOID         pvReserved  
 );  
```  
  
#### <a name="parameters"></a>Параметры  
 `pEnum`  
 [out] Указатель на область памяти, содержащей запрошенный `IAssemblyEnum` указателя.  
  
 `pUnkReserved`  
 [in] Зарезервировано для будущего расширения. `pUnkReserved` должен быть пустой ссылкой.  
  
 `pName`  
 [in] `IAssemblyName` Запрошенной сборки. Это имя используется для фильтрации перечисления. Он может быть null для перечисления всех сборок в глобальном кэше сборок.  
  
 `dwFlags`  
 [in] Флаги для изменения поведения перечислителя. Этот параметр содержит ровно один бит из [ASM_CACHE_FLAGS](../../../../docs/framework/unmanaged-api/fusion/asm-cache-flags-enumeration.md) перечисления.  
  
 `pvReserved`  
 [in] Зарезервировано для будущего расширения. `pvReserved` должен быть пустой ссылкой.  
  
## <a name="remarks"></a>Примечания  
 `dwFlags` Параметр содержит ровно один бит из `ASM_CACHE_FLAGS` перечисления.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** Fusion.h  
  
 **Библиотека:** включена как ресурс в MsCorEE.dll  
  
 **Версии платформы .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Интерфейс IAssemblyEnum](../../../../docs/framework/unmanaged-api/fusion/iassemblyenum-interface.md)  
 [Интерфейс IAssemblyName](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-interface.md)  
 [Глобальные статические функции Fusion](../../../../docs/framework/unmanaged-api/fusion/fusion-global-static-functions.md)

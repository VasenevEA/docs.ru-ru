---
title: Функция FunctionEnter2
ms.date: 03/30/2017
api_name:
- FunctionEnter2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionEnter2
helpviewer_keywords:
- FunctionEnter2 function [.NET Framework profiling]
ms.assetid: ce7a21f9-0ca3-4b92-bc4b-bb803cae3f51
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d79249a2540adbd7f1b7e9bf36c899ba94d71e2e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="functionenter2-function"></a>Функция FunctionEnter2
Уведомляет профилировщик, что элемент управления передается в функцию и содержит сведения о стеке кадра и аргументов функции. Эта функция замещает [FunctionEnter](../../../../docs/framework/unmanaged-api/profiling/functionenter-function.md) функции.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
void __stdcall FunctionEnter2 (  
    [in]  FunctionID                       funcId,   
    [in]  UINT_PTR                         clientData,   
    [in]  COR_PRF_FRAME_INFO               func,   
    [in]  COR_PRF_FUNCTION_ARGUMENT_INFO  *argumentInfo  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `funcId`  
 [in] Идентификатор функции, в которую передается элемента управления.  
  
 `clientData`  
 [in] Идентификатор повторно сопоставленной функции, который ранее указанный профилировщик с помощью [FunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/functionidmapper-function.md) функции.  
  
 `func`  
 [in] Объект `COR_PRF_FRAME_INFO` значение, которое указывает на сведения о кадре стека.  
  
 Профилировщик должен интерпретировать его как непрозрачный дескриптор, который может быть передан обратно в ядро выполнения в [ICorProfilerInfo2::GetFunctionInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md) метод.  
  
 `argumentInfo`  
 [in] Указатель на [COR_PRF_FUNCTION_ARGUMENT_INFO](../../../../docs/framework/unmanaged-api/profiling/cor-prf-function-argument-info-structure.md) структуру, которая задает расположение в памяти из аргументов функции.  
  
 Чтобы получить доступ к информации аргумент `COR_PRF_ENABLE_FUNCTION_ARGS` должен быть установлен флаг. Можно использовать профилировщик [ICorProfilerInfo::SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md) метод, чтобы задать флаги событий.  
  
## <a name="remarks"></a>Примечания  
 Значения `func` и `argumentInfo` параметры не допускаются после `FunctionEnter2` функция возвращает, так как значения, могут быть изменены или удалены.  
  
 `FunctionEnter2` Функция является обратным вызовом, необходимо произвести его. В реализации должен использоваться `__declspec`(`naked`) атрибут класса хранения.  
  
 Перед вызовом этой функции ядро выполнения не сохраняет значения регистров.  
  
-   При входе необходимо сохранить все используемые регистры, включая те, в единицах измерения с плавающей запятой (FPU).  
  
-   При выходе необходимо восстановить стек путем выталкивания из всех параметров, переведенных вызывающим кодом.  
  
 Реализация `FunctionEnter2` не должен блокироваться, поскольку это приведет к задержке сборки мусора. Реализация не должны предпринимать попытки сбора мусора, так как стек может находиться в состоянии понятного имени сбора мусора. При попытке сбора мусора, среда выполнения будет блокироваться до `FunctionEnter2` возвращает.  
  
 Кроме того `FunctionEnter2` функции не следует вызывать управляемый код или каким-либо образом вызывать управляемое распределение памяти.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorProf.idl  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Функция FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)  
 [Функция FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)  
 [Метод SetEnterLeaveFunctionHooks2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md)  
 [Глобальные статические функции профилирования](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)

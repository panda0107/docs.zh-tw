---
title: FunctionTailcall3 函式
ms.date: 03/30/2017
api_name:
- FunctionTailcall3
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionTailcall3
helpviewer_keywords:
- FunctionTailcall3 function [.NET Framework profiling]
ms.assetid: 1e48243f-5de6-4bd6-a1d0-e1d248bca4b8
topic_type:
- apiref
ms.openlocfilehash: 3bedb2c5f55f608b1153272437c0f55b730c2dfc
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2020
ms.locfileid: "76866852"
---
# <a name="functiontailcall3-function"></a>FunctionTailcall3 函式
通知分析工具，目前正在執行的函式即將對另一個函式執行 tail 呼叫。  
  
## <a name="syntax"></a>語法  
  
```cpp  
void __stdcall FunctionTailcall3 (FunctionOrRemappedID functionOrRemappedID);  
```  
  
## <a name="parameters"></a>參數

- `functionOrRemappedID`

  \[in]）目前正在執行之函式的識別碼，即將進行 tail 呼叫。

## <a name="remarks"></a>備註  
 `FunctionTailcall3` 回呼函式會通知分析工具，因為已呼叫函式。 請使用[ICorProfilerInfo3：： SetEnterLeaveFunctionHooks3 方法](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)來註冊此函式的實作為。  
  
 `FunctionTailcall3` 函數是回呼;您必須加以執行。 此執行必須使用 `__declspec(naked)` 儲存類別屬性。  
  
 在呼叫此函式之前，執行引擎不會儲存任何暫存器。  
  
- 輸入時，您必須儲存您所使用的所有暫存器，包括浮點單位（FPU）中的暫存器。  
  
- 結束時，您必須透過關閉其呼叫者推送的所有參數來還原堆疊。  
  
 `FunctionTailcall3` 的執行不應該封鎖，因為它會延遲垃圾收集。 執行不應嘗試垃圾收集，因為堆疊可能不會處於垃圾收集的唯讀狀態。 如果嘗試垃圾收集，執行時間將會封鎖，直到 `FunctionTailcall3` 傳回為止。  
  
 `FunctionTailcall3` 函式不得呼叫 managed 程式碼，或以任何方式造成 managed 記憶體配置。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Corprof.idl .idl  
  
 **程式庫：** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [FunctionEnter3](functionenter3-function.md)
- [FunctionLeave3](functionleave3-function.md)
- [FunctionEnter3WithInfo](functionenter3withinfo-function.md)
- [FunctionLeave3WithInfo](functionleave3withinfo-function.md)
- [FunctionTailcall3WithInfo 函式](functiontailcall3withinfo-function.md)
- [SetEnterLeaveFunctionHooks3](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)
- [SetEnterLeaveFunctionHooks3WithInfo](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)
- [SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md)
- [SetFunctionIDMapper2](icorprofilerinfo3-setfunctionidmapper2-method.md)
- [分析全域靜態函式](profiling-global-static-functions.md)

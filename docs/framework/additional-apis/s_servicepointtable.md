---
title: ServicePointManager。 s_ServicePointTable 欄位
ms.date: 05/01/2017
topic_type:
- apiref
api_name:
- System.Net.ServicePointManager.s_ServicePointTable
api_location:
- System.dll
api_type:
- Assembly
ms.assetid: 24459679-291c-401a-9def-e42b29466fcf
ms.openlocfilehash: 272a0c113fd70d804c763ba0e7e6e9a4a4ee04ce
ms.sourcegitcommit: 9c54866bcbdc49dbb981dd55be9bbd0443837aa2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2020
ms.locfileid: "77214925"
---
# <a name="servicepointmanagers_servicepointtable-field"></a>ServicePointManager\_ServicePointTable 欄位

`ServicePointManager.s_ServicePointTable` 是一個 <xref:System.Collections.Hashtable>，其中包含 <xref:System.AppDomain>中的作用中 HTTP 連線（<xref:System.Net.ServicePoint>s）清單。

## <a name="syntax"></a>語法
  
```csharp  
private static Hashtable s_ServicePointTable
```

> [!WARNING]
> [`ServicePointManager.s_ServicePointTable`] 欄位是私用的，不適合直接在程式碼中使用。
> 
> 在任何情況下，Microsoft 不支援在生產應用程式中使用此欄位。

## <a name="requirements"></a>需求

**命名空間：** <xref:System.Net>

**元件：** 系統（在 System .dll 中）

**.NET Framework 版本：** 自2.0 開始提供。

---
title: IXCLRDataProcess::EnumModule 方法
ms.date: 01/16/2019
api.name:
- IXCLRDataProcess::EnumModule Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataProcess::EnumModule Method
helpviewer.keywords:
- IXCLRDataProcess::EnumModule Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: fa1e41985444324627c6b66a109b4619d85fc57f
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2019
ms.locfileid: "54416458"
---
# <a name="ixclrdataprocessenummodule-method"></a><span data-ttu-id="0b87e-102">IXCLRDataProcess::EnumModule 方法</span><span class="sxs-lookup"><span data-stu-id="0b87e-102">IXCLRDataProcess::EnumModule Method</span></span>

<span data-ttu-id="0b87e-103">列舉此程序的模組。</span><span class="sxs-lookup"><span data-stu-id="0b87e-103">Enumerates the modules of this process.</span></span>

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a><span data-ttu-id="0b87e-104">語法</span><span class="sxs-lookup"><span data-stu-id="0b87e-104">Syntax</span></span>

```
HRESULT EnumModule(
    [in, out] CLRDATA_ENUM  *handle,
    [out] IXCLRDataModule  **mod
);
```

### <a name="parameters"></a><span data-ttu-id="0b87e-105">參數</span><span class="sxs-lookup"><span data-stu-id="0b87e-105">Parameters</span></span>

<span data-ttu-id="0b87e-106">`handle` [in、 out]列舉模組控制代碼。</span><span class="sxs-lookup"><span data-stu-id="0b87e-106">`handle` [in, out] A handle for enumerating the modules.</span></span>

<span data-ttu-id="0b87e-107">`mod` [out]列舉的模組中。</span><span class="sxs-lookup"><span data-stu-id="0b87e-107">`mod` [out] The enumerated module.</span></span>

## <a name="remarks"></a><span data-ttu-id="0b87e-108">備註</span><span class="sxs-lookup"><span data-stu-id="0b87e-108">Remarks</span></span>

<span data-ttu-id="0b87e-109">提供的方法是一部分`IXCLRDataProcess`介面，並對應至的虛擬方法表 25 的位置。</span><span class="sxs-lookup"><span data-stu-id="0b87e-109">The provided method is part of the `IXCLRDataProcess` interface and corresponds to the 25th slot of the virtual method table.</span></span>

## <a name="requirements"></a><span data-ttu-id="0b87e-110">需求</span><span class="sxs-lookup"><span data-stu-id="0b87e-110">Requirements</span></span>

<span data-ttu-id="0b87e-111">**平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="0b87e-111">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
<span data-ttu-id="0b87e-112">**標頭：** 無</span><span class="sxs-lookup"><span data-stu-id="0b87e-112">**Header:** None</span></span>  
<span data-ttu-id="0b87e-113">**程式庫：** 無</span><span class="sxs-lookup"><span data-stu-id="0b87e-113">**Library:** None</span></span>  
<span data-ttu-id="0b87e-114">**.NET framework 版本：**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span><span class="sxs-lookup"><span data-stu-id="0b87e-114">**.NET Framework Versions:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span></span>  

## <a name="see-also"></a><span data-ttu-id="0b87e-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0b87e-115">See Also</span></span>

- [<span data-ttu-id="0b87e-116">CLRDataSourceType 列舉</span><span class="sxs-lookup"><span data-stu-id="0b87e-116">CLRDataSourceType Enumeration</span></span>](../../../../docs/framework/unmanaged-api/debugging/clrdatasourcetype-enumeration.md)
- [<span data-ttu-id="0b87e-117">偵錯</span><span class="sxs-lookup"><span data-stu-id="0b87e-117">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [<span data-ttu-id="0b87e-118">IXCLRDataModule 介面</span><span class="sxs-lookup"><span data-stu-id="0b87e-118">IXCLRDataModule Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/ixclrdatamodule-interface.md)
- [<span data-ttu-id="0b87e-119">IXCLRDataProcess 介面</span><span class="sxs-lookup"><span data-stu-id="0b87e-119">IXCLRDataProcess Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/ixclrdataprocess-interface.md)
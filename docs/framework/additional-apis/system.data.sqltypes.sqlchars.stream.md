---
title: SqlChars.Stream 屬性 (System.Data.SqlTypes)
author: douglaslMS
ms.author: douglasl
ms.date: 12/19/2018
ms.technology:
- dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlChars.Stream
- System.Data.SqlTypes.SqlChars.get_Stream
- System.Data.SqlTypes.SqlChars.set_Stream
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: d756b78a7cdbc12562e474ca3d2c9a1f3529f6bf
ms.sourcegitcommit: a36cfc9dbbfc04bd88971f96e8a3f8e283c15d42
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/11/2019
ms.locfileid: "54223048"
---
# <a name="sqlcharsstream-property"></a><span data-ttu-id="d0403-102">SqlChars.Stream 屬性</span><span class="sxs-lookup"><span data-stu-id="d0403-102">SqlChars.Stream Property</span></span>

<span data-ttu-id="d0403-103">取得或設定字元資料流。</span><span class="sxs-lookup"><span data-stu-id="d0403-103">Gets or sets the character stream.</span></span> <span data-ttu-id="d0403-104">包含此屬性的組件有 SQLAccess.dll friend 關聯性。</span><span class="sxs-lookup"><span data-stu-id="d0403-104">The assembly that contains this property has a friend relationship with SQLAccess.dll.</span></span> <span data-ttu-id="d0403-105">它適用於 SQL server。</span><span class="sxs-lookup"><span data-stu-id="d0403-105">It's intended for use by SQL Server.</span></span> <span data-ttu-id="d0403-106">其他資料庫，請使用該資料庫所提供的主控機制。</span><span class="sxs-lookup"><span data-stu-id="d0403-106">For other databases, use the hosting mechanism provided by that database.</span></span>

```csharp
internal SqlStreamChars Stream { get; set; }
```

## <a name="property-value"></a><span data-ttu-id="d0403-107">屬性值</span><span class="sxs-lookup"><span data-stu-id="d0403-107">Property value</span></span>

`System.Data.SqlTypes.SqlStreamChars`\
<span data-ttu-id="d0403-108">字元資料流中。</span><span class="sxs-lookup"><span data-stu-id="d0403-108">The character stream.</span></span>

## <a name="remarks"></a><span data-ttu-id="d0403-109">備註</span><span class="sxs-lookup"><span data-stu-id="d0403-109">Remarks</span></span>

> [!WARNING]
> <span data-ttu-id="d0403-110">`SqlChars.Stream`屬性內部，且不適合直接在您的程式碼中使用。</span><span class="sxs-lookup"><span data-stu-id="d0403-110">The `SqlChars.Stream` property is internal and is not meant to be used directly in your code.</span></span>
>
> <span data-ttu-id="d0403-111">在生產環境應用程式中任何情況下，Microsoft 不支援這個屬性的使用。</span><span class="sxs-lookup"><span data-stu-id="d0403-111">Microsoft does not support the use of this property in a production application under any circumstance.</span></span>

## <a name="requirements"></a><span data-ttu-id="d0403-112">需求</span><span class="sxs-lookup"><span data-stu-id="d0403-112">Requirements</span></span>

<span data-ttu-id="d0403-113">**命名空間︰** <xref:System.Data.SqlTypes></span><span class="sxs-lookup"><span data-stu-id="d0403-113">**Namespace:** <xref:System.Data.SqlTypes></span></span>

<span data-ttu-id="d0403-114">**組件：** System.Data （在 System.Data.dll 中)</span><span class="sxs-lookup"><span data-stu-id="d0403-114">**Assembly:** System.Data (in System.Data.dll)</span></span>

<span data-ttu-id="d0403-115">**.NET framework 版本：** 自 2.0 起可用。</span><span class="sxs-lookup"><span data-stu-id="d0403-115">**.NET Framework versions:** Available since 2.0.</span></span>
---
ms.openlocfilehash: f9000b19997201c2d3de0643669f9029ff1ca31c
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74567998"
---
### <a name="envelopedcms-defaults-to-aes-256-encryption"></a><span data-ttu-id="e471d-101">EnvelopedCms 預設為 AES-256 加密</span><span class="sxs-lookup"><span data-stu-id="e471d-101">EnvelopedCms defaults to AES-256 encryption</span></span>

<span data-ttu-id="e471d-102">`EnvelopedCms` 所使用的預設對稱式加密演算法已從 TripleDES 變更為 AES-256。</span><span class="sxs-lookup"><span data-stu-id="e471d-102">The default symmetric encryption algorithm used by `EnvelopedCms` has changed from TripleDES to AES-256.</span></span>

#### <a name="change-description"></a><span data-ttu-id="e471d-103">變更描述</span><span class="sxs-lookup"><span data-stu-id="e471d-103">Change description</span></span>

<span data-ttu-id="e471d-104">在 .NET Core Preview 7 和舊版中，當 <xref:System.Security.Cryptography.Pkcs.EnvelopedCms> 用來加密資料，而不透過函式多載指定對稱式加密演算法時，會使用 TripleDES/3DES/3DEA/DES3-EDE 演算法來加密資料。</span><span class="sxs-lookup"><span data-stu-id="e471d-104">In .NET Core Preview 7 and earlier versions, when <xref:System.Security.Cryptography.Pkcs.EnvelopedCms> is used to encrypt data without specifying a symmetric encryption algorithm via a constructor overload, the data was encrypted with the TripleDES/3DES/3DEA/DES3-EDE algorithm.</span></span>

<span data-ttu-id="e471d-105">從 .NET Core 3.0 Preview 8 開始（透過[4.6.0 的版本](https://www.nuget.org/packages/System.Security.Cryptography.Pkcs/)），預設演算法已變更為 AES-256 以進行演算法現代化，並改善預設選項的安全性。</span><span class="sxs-lookup"><span data-stu-id="e471d-105">Starting with .NET Core 3.0 Preview 8 (via version 4.6.0 of the [System.Security.Cryptography.Pkcs](https://www.nuget.org/packages/System.Security.Cryptography.Pkcs/) NuGet package), the default algorithm has been changed to AES-256 for algorithm modernization and to improve the security of default options.</span></span> <span data-ttu-id="e471d-106">如果訊息收件者憑證具有（非 EC） Diffie-hellman 公開金鑰，加密作業可能會因基礎平臺的限制而失敗並出現 <xref:System.Security.Cryptography.CryptographicException>。</span><span class="sxs-lookup"><span data-stu-id="e471d-106">If a message recipient certificate has a (non-EC) Diffie-Hellman public key, the encryption operation may fail with a <xref:System.Security.Cryptography.CryptographicException> due to limitations in the underlying platform.</span></span>

<span data-ttu-id="e471d-107">在下列範例程式碼中，如果在 .NET Core 3.0 Preview 7 或更早版本上執行，則會使用 TripleDES 來加密資料。</span><span class="sxs-lookup"><span data-stu-id="e471d-107">In the following sample code, the data is encrypted with TripleDES if running on .NET Core 3.0 Preview 7 or earlier.</span></span> <span data-ttu-id="e471d-108">如果在 .NET Core 3.0 Preview 8 或更新版本上執行，則會使用 AES-256 進行加密。</span><span class="sxs-lookup"><span data-stu-id="e471d-108">If running on .NET Core 3.0 Preview 8 or later, it is encrypted with AES-256.</span></span>

```csharp
EnvelopedCms cms = new EnvelopedCms(content);
cms.Encrypt(recipient);
return cms.Encode();
```

#### <a name="version-introduced"></a><span data-ttu-id="e471d-109">引進的版本</span><span class="sxs-lookup"><span data-stu-id="e471d-109">Version introduced</span></span>

<span data-ttu-id="e471d-110">3.0 Preview 8</span><span class="sxs-lookup"><span data-stu-id="e471d-110">3.0 Preview 8</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="e471d-111">建議的動作</span><span class="sxs-lookup"><span data-stu-id="e471d-111">Recommended action</span></span>

<span data-ttu-id="e471d-112">如果您對變更有負面影響，您可以藉由在 <xref:System.Security.Cryptography.Pkcs.EnvelopedCms> 的程式中明確指定加密演算法識別碼（其中包含 <xref:System.Security.Cryptography.Pkcs.AlgorithmIdentifier>類型的參數）來還原 TripleDES 加密，例如：</span><span class="sxs-lookup"><span data-stu-id="e471d-112">If you are negatively impacted by the change, you can restore TripleDES encryption by explicitly specifying the encryption algorithm identifier in an <xref:System.Security.Cryptography.Pkcs.EnvelopedCms> constructor that includes a parameter of type <xref:System.Security.Cryptography.Pkcs.AlgorithmIdentifier>, such as:</span></span>

```csharp
Oid tripleDesOid = new Oid("1.2.840.113549.3.7", null);
AlgorithmIdentifier tripleDesIdentifier = new AlgorithmIdentifier(tripleDesOid);
EnvelopedCms cms = new EnvelopedCms(content, tripleDesIdentifier);

cms.Encrypt(recipient);
return cms.Encode()l
```

#### <a name="category"></a><span data-ttu-id="e471d-113">Category</span><span class="sxs-lookup"><span data-stu-id="e471d-113">Category</span></span>

<span data-ttu-id="e471d-114">密碼編譯</span><span class="sxs-lookup"><span data-stu-id="e471d-114">Cryptography</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="e471d-115">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="e471d-115">Affected APIs</span></span>

- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor(System.Security.Cryptography.Pkcs.ContentInfo)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor(System.Security.Cryptography.Pkcs.SubjectIdentifierType,System.Security.Cryptography.Pkcs.ContentInfo)?displayProperty=nameWithType>

<!--

### Affected APIs

- `M:System.Security.Cryptography.Pkcs.EnvelopedCms.#ctor`
- `M:System.Security.Cryptography.Pkcs.EnvelopedCms.#ctor(System.Security.Cryptography.Pkcs.ContentInfo)`
- `M:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor(System.Security.Cryptography.Pkcs.SubjectIdentifierType,System.Security.Cryptography.Pkcs.ContentInfo)`

-->
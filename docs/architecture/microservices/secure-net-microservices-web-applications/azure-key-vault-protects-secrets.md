---
title: 使用 Azure Key Vault 以在生產階段保護密碼
description: .NET 微服務和 Web 應用程式中的安全性 - Azure Key Vault 是可讓系統管理員完全掌控應用程式祕密處理的絕佳方式。 系統管理員甚至可以指派和撤銷開發值，而不需要開發人員來處理它們。
author: mjrousos
ms.date: 01/30/2020
ms.openlocfilehash: cc95d491136c945255408cec2bd49d4d6579e29a
ms.sourcegitcommit: f38e527623883b92010cf4760246203073e12898
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2020
ms.locfileid: "77501759"
---
# <a name="use-azure-key-vault-to-protect-secrets-at-production-time"></a>使用 Azure Key Vault 在生產階段保護祕密

儲存為環境變數或由密碼管理員工具所儲存的密碼仍然會儲存在本機，而且在電腦上未加密。 儲存密碼的更安全選項是 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/)，以提供安全且集中的位置來儲存金鑰和密碼。

**Microsoft.Extensions.Configuration.AzureKeyVault** 套件允許 ASP.NET Core 應用程式從 Azure Key Vault 中讀取設定資訊。 若要開始使用 Azure Key Vault 中的密碼，您可以遵循下列步驟：

1. 將應用程式註冊為 Azure AD 應用程式。 （金鑰保存庫的存取權是由 Azure AD 管理）。這可以透過 Azure 管理入口網站來完成。

   或者，如果您想要應用程式使用憑證進行驗證，而不是使用密碼或用戶端密碼，則可以使用 [New-AzADApplication](/powershell/module/az.resources/new-azadapplication) PowerShell Cmdlet。 您向 Azure Key Vault 註冊的憑證只需要公開金鑰 您的應用程式將會使用私密金鑰。

2. 建立新的服務主體，以提供已註冊應用程式對金鑰保存庫的存取。 您可以使用下列 PowerShell 命令執行這項作業：

   ```powershell
   $sp = New-AzADServicePrincipal -ApplicationId "<Application ID guid>"
   Set-AzKeyVaultAccessPolicy -VaultName "<VaultName>" -ServicePrincipalName $sp.ServicePrincipalNames[0] -PermissionsToSecrets all -ResourceGroupName "<KeyVault Resource Group>"
   ```

3. 在建立 <xref:Microsoft.Extensions.Configuration.AzureKeyVaultConfigurationExtensions.AddAzureKeyVault%2A?displayProperty=nameWithType> 執行個體時呼叫 <xref:Microsoft.Extensions.Configuration.IConfigurationRoot> 擴充方法，以包含金鑰保存庫作為應用程式中的設定來源。 請注意，呼叫 `AddAzureKeyVault` 時需要已註冊並提供先前步驟中金鑰保存庫存取權的應用程式識別碼。

   您也可以藉由包含 `AddAzureKeyVault`Microsoft.IdentityModel.Clients.ActiveDirectory[ 套件的參考，使用採用憑證來取代用戶端祕密的 ](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) 多載。

> [!IMPORTANT]
> 我們建議您註冊 Azure Key Vault 做為最後的設定提供者，因此它可以覆寫先前提供者的設定值。

## <a name="additional-resources"></a>其他資源

- **使用 Azure Key Vault 保護應用程式祕密** \
  [https://docs.microsoft.com/azure/guidance/guidance-multitenant-identity-keyvault](/azure/guidance/guidance-multitenant-identity-keyvault)

- **在開發期間安全儲存應用程式祕密** \
  [https://docs.microsoft.com/aspnet/core/security/app-secrets](/aspnet/core/security/app-secrets)

- **設定資料保護** \
  [https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/overview](/aspnet/core/security/data-protection/configuration/overview)

- **ASP.NET Core 中的資料保護金鑰管理和存留期** \
  [https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/default-settings](/aspnet/core/security/data-protection/configuration/default-settings)

- **Microsoft.Extensions.Configuration.KeyPerFile** GitHub 存放庫。 \
  <https://github.com/dotnet/extensions/tree/master/src/Configuration/Config.KeyPerFile>

>[!div class="step-by-step"]
>[上一頁](developer-app-secrets-storage.md)
>[下一頁](../key-takeaways.md)

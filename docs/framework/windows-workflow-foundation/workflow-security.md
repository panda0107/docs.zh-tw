---
title: 工作流程安全性
ms.date: 03/30/2017
helpviewer_keywords:
- programming [WF], workflow security
ms.assetid: d712a566-f435-44c0-b8c0-49298e84b114
ms.openlocfilehash: 36d03a2fca8f143b98338050fc9da4490960bda9
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "74837515"
---
# <a name="workflow-security"></a>工作流程安全性
Windows Workflow Foundation （WF）與數種不同的技術整合，例如 Microsoft SQL Server 和 Windows Communication Foundation （WCF）。 如果與這些技術互動的方式不適當，可能會造成工作流程上的安全性問題。

## <a name="persistence-security-concerns"></a>持續性安全性考量

1. 使用 <xref:System.Activities.Statements.Delay> 活動和持續性的工作流程需要由服務重新啟動。 Windows AppFabric 使用工作流程管理服務 (WMS) 來重新啟動具有過期計時器的工作流程。 WMS 會建立 <xref:System.ServiceModel.WorkflowServiceHost> 以裝載重新啟動的工作流程。 如果 WMS 服務停止，當工作流程的計時器過期，保存的工作流程將不會重新啟動。

2. 永久性執行個體的存取應受到保護，免受惡意的外部實體存取應用程式定義域。 此外，開發人員應確保惡意程式碼不能與永久性執行個體程式碼在同一個應用程式定義域中執行。

3. 不應該以更高 (管理員) 權限執行永久性執行個體。

4. 應該保護位於應用程式定義域之外，正在接受處理的資料。

5. 需要安全性隔離的應用程式不應共用結構描述抽象的同一執行個體。 此類應用程式應使用不同的存放區提供者，或是已設定要使用不同存放區具現化的存放區提供者。

## <a name="sql-server-security-concerns"></a>SQL Server 安全性考量

- 當使用大量子活動、位置、書籤、主機延伸或範圍時，或當使用有大量承載的書籤時，可能會耗盡記憶體，或在持續性期間過度配置不當的資料庫空間。 可使用物件層級與資料庫層級的安全性來減少這種情況。

- 使用 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 時，必須保護執行個體存放區的安全。

- 應加密執行個體存放區中的敏感資料。 如需詳細資訊，請參閱 [SQL Server 加密](/sql/relational-databases/security/encryption/sql-server-encryption)。

- 因為資料庫連接字串通常包含在組態檔中，應該使用 Windows 層級的安全性 (ACL) 以確保組態檔 (通常為 Web.Config) 是安全的，且登入和密碼資訊沒有包含在連接字串中。 資料庫和 Web 伺服器之間應改用 Windows 驗證。

## <a name="considerations-for-workflowservicehost"></a>WorkflowServiceHost 的考量

- 應保護工作流程中使用的 Windows Communication Foundation （WCF）端點。 如需詳細資訊，請參閱[WCF 安全性總覽](../wcf/feature-details/security-overview.md)。

- 可使用 <xref:System.ServiceModel.ServiceAuthorizationManager> 實作主機層級授權。 如需詳細資訊，請參閱[如何：建立服務的自訂授權管理員](../wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md)。

- 傳入訊息的 ServiceSecurityContext 也可在工作流程內取得，方法是存取 OperationContext。

## <a name="wf-security-pack-ctp"></a>WF Security Pack CTP
 Microsoft WF Security Pack CTP 1 是一組活動的第一個「社區技術預覽」（CTP）版本，也是以[.NET Framework 4](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w0x726c2(v=vs.100)) （WF 4）和[Windows IDENTITY Foundation （WIF）](../security/index.md)中的[Windows Workflow Foundation](index.md)為基礎的實施。  Microsoft WF Security Pack CTP 1 包含活動及其設計工具，說明如何使用工作流程輕鬆進行各種安全性相關的案例，包括：

1. 在工作流程中模擬用戶端身分識別

2. 工作流程中的授權，例如 PrincipalPermission 和宣告的驗證

3. 通過驗證的傳訊，其使用工作流程中指定的 ClientCredentials，例如使用者名稱/密碼或從安全性權杖服務 (STS) 擷取的權杖。

4. 使用 WS-Trust ActAs 將用戶端安全性權杖傳到後端服務 (以宣告為基礎的委派)

如需詳細資訊和下載 WF Security Pack CTP，請參閱： [Wf Security PACK ctp](https://archive.codeplex.com/?p=wf)

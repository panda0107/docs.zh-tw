---
title: 發出使用者程式碼追蹤
ms.date: 03/30/2017
ms.assetid: fa54186a-8ffa-4332-b0e7-63867126fd49
ms.openlocfilehash: 93da2eb74705a0581923d0317315e628f374be3e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "61998111"
---
# <a name="emitting-user-code-traces"></a>發出使用者程式碼追蹤

除了啟用追蹤來收集檢測資料產生 Windows Communication Foundation (WCF) 組態中的，您也可以發出使用者程式碼中以程式設計方式追蹤。 如此一來，您就可以主動建立供日後深入診斷之用的檢測資料。 本主題將討論如何完成這項工作。

颾魤 ㄛ[擴充追蹤](../../../../../docs/framework/wcf/samples/extending-tracing.md)範例包含下列各節所示的程式碼。

## <a name="creating-a-trace-source"></a>建立追蹤來源

您可以使用下列程式碼來建立使用者追蹤來源。

```csharp
TraceSource ts = new TraceSource("myUserTraceSource");
```

## <a name="creating-activities"></a>建立活動

活動是處理的邏輯單位。 您可以為每個主要處理單位建立一個活動，而這些處理單位是您要在其中將追蹤聚集成群組的地方。 例如，您可以為每一個針對服務發出的要求建立一個活動。 若要這麼做，請執行下列步驟。

1. 儲存範圍內的活動識別碼。

2. 建立新的活動識別碼。

3. 從範圍內的活動傳輸到新活動、設定範圍內的新活動，然後發出該活動的「開始追蹤」。

下列程式碼會示範如何執行此項作業。

```csharp
Guid oldID = Trace.CorrelationManager.ActivityId;
Guid traceID = Guid.NewGuid();
ts.TraceTransfer(0, "transfer", traceID);
Trace.CorrelationManager.ActivityId = traceID; // Trace is static
ts.TraceEvent(TraceEventType.Start, 0, "Add request");
```

## <a name="emitting-traces-within-a-user-activity"></a>在使用者活動內發出追蹤

下列程式碼會在使用者活動內發出追蹤。

```csharp
double value1 = 100.00D;
double value2 = 15.99D;
ts.TraceInformation("Client sends message to Add " + value1 + ", " + value2);
double result = client.Add(value1, value2);
ts.TraceInformation("Client receives Add response '" + result + "'");
```

## <a name="stopping-the-activities"></a>停止活動

若要停止活動，請傳輸回到舊活動、停止目前的活動識別碼，然後重設範圍內的舊活動識別碼。

下列程式碼會示範如何執行此項作業。

```csharp
ts.TraceTransfer(0, "transfer", oldID);
ts.TraceEvent(TraceEventType.Stop, 0, "Add request");
Trace.CorrelationManager.ActivityId = oldID;
```

## <a name="propagating-the-activity-id-to-a-service"></a>將活動識別碼傳播至服務

如果同時在用戶端和服務的組態檔中，將其 `propagateActivity` 追蹤來源的 `true` 屬性設定為 `System.ServiceModel`，則會在用戶端定義的同一個活動中進行「加法」要求的服務處理。 如果服務定義了本身的活動和傳輸，服務追蹤就不會出現在用戶端傳播的活動中， 而會出現在和用戶端傳播的識別碼所代表之活動相互關聯的活動中 (此相互關聯是由傳輸追蹤建立)。

> [!NOTE]
> 如果`propagateActivity`屬性設為`true`WCF 用戶端與服務上，設定環境活動中的服務作業範圍。

您可以使用下列程式碼來檢查活動是否已由 WCF 所設定範圍中。

```csharp
// Check if an activity was set in scope by WCF, if it was
// propagated from the client. If not, ( ambient activity is
// equal to Guid.Empty), create a new one.
if(Trace.CorrelationManager.ActivityId == Guid.Empty)
{
    Guid newGuid = Guid.NewGuid();
    Trace.CorrelationManager.ActivityId = newGuid;
}
// Emit your Start trace.
ts.TraceEvent(TraceEventType.Start, 0, "Add Activity");

// Emit the processing traces for that request.
serviceTs.TraceInformation("Service receives Add "
                            + n1 + ", " + n2);
// double result = n1 + n2;
serviceTs.TraceInformation("Service sends Add result" + result);

// Emit the Stop trace and exit the method scope.
ts.TraceEvent(TraceEventType.Stop, 0, "Add Activity");
// return result;
```

## <a name="tracing-exceptions-thrown-in-code"></a>追蹤程式碼中擲回的例外狀況

當您在程式碼中擲回例外狀況時，您也可以使用下列程式碼來追蹤警告層級 (含) 以上的例外狀況。

```csharp
ts.TraceEvent(TraceEventType.Warning, 0, "Throwing exception " + "exceptionMessage");
```

## <a name="viewing-user-traces-in-the-service-trace-viewer-tool"></a>在服務追蹤檢視器工具中檢視使用者追蹤

本節包含執行所產生的追蹤的螢幕擷取畫面[擴充追蹤](../../../../../docs/framework/wcf/samples/extending-tracing.md)取樣，請使用檢視時[Service Trace Viewer Tool (SvcTraceViewer.exe)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)。

在下列圖表中，左面板上選取先前建立的 「 加法要求 」 活動。 它和構成應用程式用戶端程式的另外三個「數學運算」活動 (除法、減法、乘法) 列在一起。 使用者程式碼為每項作業各定義了一個新活動，以便隔離不同要求中可能發生的錯誤。

示範如何使用傳輸中的[擴充追蹤](../../../../../docs/framework/wcf/samples/extending-tracing.md)範例中，也建立封裝四個作業要求的計算機 」 活動。 每個要求都有往返於「計算機」活動和要求活動之間的傳輸 (本圖的右上方面板中會反白顯示追蹤)。

當您選取左面板上的活動時，這個活動所包含的追蹤會顯示在右上方面板中。 如果`propagateActivity`是`true`中每個端點的要求路徑，則要求活動中的追蹤會從所有參與要求的處理序。 在這個範例中，您可以在面板的第 4 欄中看見來自用戶端和服務兩方的追蹤。

這個活動會顯示下列處理順序：

1. 用戶端傳送訊息至「加法」。

2. 服務接收「加法」要求訊息。

3. 服務傳送「加法」回應。

4. 用戶端接收「加法」回應。

所有這些追蹤都是在資訊層級發出。 按一下右上方面板中的追蹤，就會在右下方面板中顯示該追蹤的詳細資訊。

在下列圖表中，也會看到往返「計算機」活動的傳輸追蹤，以及每個要求活動各兩對的「開始」和「停止」追蹤，一對屬於用戶端，另一對屬於服務 (亦即，每個追蹤來源各有一對追蹤)。

![追蹤檢視器：發出使用者&#45;程式碼追蹤](../../../../../docs/framework/wcf/diagnostics/tracing/media/242c9358-475a-4baf-83f3-4227aa942fcd.gif "242c9358-475a-4baf-83f3-4227aa942fcd")依據建立時間 （左面板） 的活動和其巢狀的活動 （右上角面板） 的清單

如果服務程式碼擲回連帶導致用戶端擲回的例外狀況 (例如，用戶端未獲得其要求的回應時)，服務和用戶端的警告或錯誤訊息都會因為直接的相互關聯而在同一個活動中產生。 在下圖中，服務會擲回例外狀況，指出 「 服務拒絕處理此要求在使用者程式碼 」。 用戶端也會擲回的例外狀況，指出 「 伺服器無法處理要求，因為發生內部錯誤 」。

下圖顯示是否要求活動識別碼已傳播跨端點指定的要求錯誤將會出現相同的活動：

![如果螢幕擷取畫面顯示給定要求的端點之間的錯誤。](./media/emitting-user-code-traces/trace-viewer-endpoint-errors.gif)

按兩下左面板上的「乘法」活動時，會顯示下圖，其中包含每個相關處理序的「乘法」活動追蹤。 我們可以看到警告先發生在服務 (擲回例外狀況)，接著會因為無法處理要求而在用戶端產生警告和錯誤。 因此，我們可以看出端點間發生錯誤的因果關係，從而得知錯誤的根本原因。

下圖顯示錯誤相互關聯的圖形檢視：

![如果螢幕擷取畫面會顯示錯誤相互關聯的圖形檢視。](./media/emitting-user-code-traces/trace-viewer-error-correlation.gif)

為了取得前述的追蹤，我們將使用者追蹤來源設定為 `ActivityTracing`，而將 `propagateActivity=true` 追蹤來源設定為 `System.ServiceModel`。 我們並未將 `ActivityTracing` 設定給 `System.ServiceModel` 追蹤來源，來讓使用者程式碼使用使用者程式碼活動傳播  （當 ServiceModel 活動追蹤開啟時，用戶端中所定義的活動識別碼不會傳播到服務使用者程式碼;傳輸，不過，相互關聯的用戶端和服務使用者程式碼活動的中繼的 WCF 活動。）

定義活動和傳播活動識別碼可讓我們在端點之間執行直接錯誤相互關聯。 如此一來，就可以更迅速地找到錯誤的根本原因。

## <a name="see-also"></a>另請參閱

- [擴充追蹤](../../../../../docs/framework/wcf/samples/extending-tracing.md)

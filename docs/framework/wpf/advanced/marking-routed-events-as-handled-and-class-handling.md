---
title: 將路由事件標記為已處理以及類別處理
ms.date: 03/30/2017
helpviewer_keywords:
- tunneling events [WPF]
- class listeners [WPF]
- listeners [WPF]
- Preview routed events [WPF]
- instance listeners [WPF]
- events [WPF], bubbling
- suppressing events [WPF]
- routed events [WPF], Preview
- composited controls [WPF]
- events [WPF], tunneling
- routed events [WPF], marking as handled
- controls [WPF], compositing
- events [WPF], suppressing
- bubbling events [WPF]
ms.assetid: 5e745508-4861-4b48-b5f6-5fc7ce5289d2
ms.openlocfilehash: 6e3f314de07948e53ffed13ddc1289c1de115edd
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401639"
---
# <a name="marking-routed-events-as-handled-and-class-handling"></a>將路由事件標記為已處理以及類別處理
路由事件的處理常式可以將事件資料內的事件標記為已處理。 處理事件時，即可有效地縮短路由。 類別處理是一種程式設計概念，此概念與路由事件相輔相成。 類別處理常式有機會在類別層級上使用處理常式來處理特定的路由事件 (此處理常式會優先叫用，之後才輪到在該類別任何執行個體上的任何執行個體處理常式)。  

<a name="prerequisites"></a>   
## <a name="prerequisites"></a>必要條件  
 本主題將詳細說明[路由事件概觀](routed-events-overview.md)中介紹的概念。  
  
<a name="When_to_Mark_Events_as_Handled"></a>   
## <a name="when-to-mark-events-as-handled"></a>標示已處理事件的時機  
 當您在路由事件的事件<xref:System.Windows.RoutedEventArgs.Handled%2A>資料中`true` , 將屬性的值設定為時, 這就稱為「將事件標示為已處理」。 不論您是應用程式作者，或控制項作者 (回應現有路由事件或實作新路由事件者)，對於何時應該將路由的事件標記為已處理，都沒有絕對的規則。 在大部分的情況下, 在路由事件的事件資料中, 「已處理」的概念應該做為您自己應用程式的有限通訊協定, 以供您自己的應用程式對[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] api 中公開的各種路由事件, 以及任何自訂路由事件的回應使用。 另一個要考慮使用「已處理」的情況為：如果您的程式碼是以重要且相對完整的方式回應路由事件，通常就應該將此路由事件標示為「已處理」。 一般而言，任何單一路由事件發生時，應該只有一個重要回應需要實作個別的處理常式。 如需更多回應，必要程式碼就必須透過在單一處理常式內鏈結的應用程式邏輯來實作，而不是使用路由的事件系統來轉送。 至於哪些項目算「重要」，這個概念也很主觀，並取決於您的應用程式或程式碼而定。 一般來說，「重要回應」範例包括：設定焦點、修改公用狀態、設定足以影響視覺化表示法的屬性，以及引發其他新的事件。 「不重要回應」的範例則包括︰修改私用狀態 (不含任何視覺效果或程式設計表示法)、記錄事件，或查看事件的引數並選擇不回應。  
  
 路由事件系統行為[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] <xref:System.Windows.UIElement.AddHandler%2A>會針對使用路由事件的已處理狀態, 強調此「重大回應」模型, 因為在中新增的處理常式或的一般簽章, 不會在回應路由事件時叫用, 其中事件資料已標示為已處理。 您必須完成以`handledEventsToo`參數版本 (<xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>) 新增處理常式的額外工作, 才能處理由事件路由中的先前參與者所標示的路由事件。  
  
 在某些情況下，控制項本身即會將特定路由事件標記為已處理。 已處理的路由事件代表 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控制項作者的控制項動作決策，以在控制項實作中回應重要或完整的路由事件，以及不需要進一步處理的事件。 通常，您可以新增事件的類別處理常式，或是覆寫其中一個基底類別上既有的類別處理常式視覺效果，來執行上述作業。 若有必要，您仍可以處理這種事件處理作業；請參閱本主題稍後的[處理控制項的事件隱藏項目](#WorkingAroundEventSuppressionByControls)。  
  
<a name="Preview_Events_vs__Bubbling_Events_and_Handling"></a>   
## <a name="preview-tunneling-events-vs-bubbling-events-and-event-handling"></a>比較「預覽」(通道) 事件、事件反昇事件和事件處理  
 預覽路由事件是一種會沿著通道路由通過項目樹狀結構的事件。 命名慣例中的「預覽」表示輸入事件的一般原則：預覽 (通道) 路由事件會在對等的事件反昇路由事件之前引發。 此外，具有通道和事件反昇組的輸入路由事件都有不同的處理邏輯。 如果事件接聽程式將通道/預覽路由事件標示為已處理，則事件反昇路由事件也會標示為已處理 (即使任何事件反昇路由事件的接聽程式尚未接收到該事件亦同)。 通道路由事件和事件反昇路由事件技術上來說是個別事件，但兩者刻意共用相同的事件資料執行個體，以造成上述行為。  
  
 通道路由事件和事件反昇路由事件之間的連線方式如下：透過內部實作任何特定 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 類別引發本身的宣告路由事件方式來完成；而成對的輸入路由事件的情況也是如此。 但除非此類別層級實作已存在，否則通道路由事件和事件反昇路由事件之間不會有任何共用命名配置的連線：若沒有上述實作，它們就是兩個完全不同的路由事件，既不會循序引發，也不會共用事件資料。  
  
 如需如何在自訂類別中實作通道/事件反昇輸入路由事件組的詳細資訊，請參閱[建立自訂路由事件](how-to-create-a-custom-routed-event.md)。  
  
<a name="Class_Handlers_and_Instance_Handlers"></a>   
## <a name="class-handlers-and-instance-handlers"></a>類別處理常式和執行個體處理常式  
 路由事件可使用兩種不同的事件接聽程式：類別接聽程式和執行個體接聽程式。 類別接聽程式存在的原因是, 類型<xref:System.Windows.EventManager>已在<xref:System.Windows.EventManager.RegisterClassHandler%2A>其靜態的函式中呼叫特定的 API, 或已從 element 基類覆寫類別處理常式虛擬方法。 實例接聽程式是特定的類別實例/元素, 其中的呼叫<xref:System.Windows.UIElement.AddHandler%2A>已附加一或多個處理常式給該路由事件。 現有[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]的路由事件會<xref:System.Windows.UIElement.AddHandler%2A>呼叫做為 common language runtime (CLR) 事件包裝函式的{}一部分,{}以加入和移除事件的執行, 這也是[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]的簡單機制已啟用透過屬性語法附加事件處理常式。 因此, 即使簡單[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]的使用方式最終等同<xref:System.Windows.UIElement.AddHandler%2A>于呼叫。  
  
 系統會檢查視覺化樹狀結構中的項目是否有登錄處理常式實作。 在整個路由中，可能會依據相關路由事件之路由策略型別中既有的順序，來叫用處理常式。 比方說，如果處理常式是附加至引發路由事件的相同元素，則事件反昇路由事件會先叫用這些處理常式。 然後，路由事件即會「事件反昇」至下一個父項目，依此類推，直到抵達應用程式的根項目為止。  
  
 從事件反昇路由中的根項目來看，如果類別處理或任何更接近路由事件來源的項目叫用了處理常式 (其可將事件引數標示為已處理)，則不會叫用根項目的處理常式，並可有效縮短到達該根項目之前的事件路由。 不過，路由並不會完全中止，因為您可以使用特殊的條件來新增處理常式，使其仍可受到叫用 (即使類別處理常式或執行個體處理常式已將路由事件標示為已處理亦同)。 在本主題稍後的[即使在事件標示為已處理時，仍要新增引發的執行個體處理常式](#AddingInstanceHandlersthatAreRaisedEvenWhenEventsareMarkedHandled)中有對此進行說明。  
  
 在比事件路由更深的層級中，也可能有多個類別處理常式在某類別的任何特定執行個體上執行。 這是因為路由事件的類別處理模型，可讓每個類別階層中所有可能的類別，針對為每個路由事件，登錄自己的類別處理常式。 系統會將每個類別處理常式新增至內部存放區，並在建構應用程式的事件路由時，將所有類別處理常式都新增至事件路由。 當類別處理常式新增至路由時，會先叫用最高衍生性類別處理常式，接著再從每個後續基底類別叫用類別處理常式。 一般來說，系統不會登錄類別處理常式，所以它們也會回應標記為已處理的路由事件。 因此，這個類別處理機制可讓您選擇下列兩個選項之一：  
  
- 由於系統會在叫用衍生的類別處理常式一段時間之後叫用基底類別處理常式，因此您可以新增不會將路由事件標記為已處理的處理常式，讓衍生的類別針對繼承自基底類別的類別處理進行補充。  
  
- 您可以新增會將路由事件標記為已處理的類別處理常式，讓衍生的類別取代來自基底類別的類別處理。 您應該謹慎使用這個方法，因為它可能會變更區域中預期的基底控制項設計，例如視覺外觀、狀態邏輯、輸入處理和命令處理。  
  
<a name="Class_Handling_of_Routed_Events"></a>   
## <a name="class-handling-of-routed-events-by-control-base-classes"></a>控制項基底類別的路由事件類別處理  
 在事件路由中每個指定的項目節點上，類別接聽程式可能會比項目上的任何執行個體接聽程式更優先回應路由事件。 基於這個理由，如果特定控制項類別實作不希望進一步傳播某個路由事件，有時候可以使用類別處理常式來隱藏該路由事件，或使用類別處理常式針對該路由事件進行特殊處理 (其為該類別功能之一)。 比方說，類別可能會引發自身類別專屬的事件，這些事件包括該特定類別內容中某些使用者輸入條件含意的詳細特性。 這樣一來，類別實作可能會將較一般的路由事件標示為已處理。 通常會加入類別處理常式, 使其不會針對已標示為已處理之共用事件資料的路由事件叫用, 但在非典型<xref:System.Windows.EventManager.RegisterClassHandler%28System.Type%2CSystem.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>的情況下, 也會註冊要叫用的類別處理常式, 即使路由事件是標示為已處理。  
  
### <a name="class-handler-virtuals"></a>類別處理常式視覺效果  
 某些專案 (尤其是基底元素<xref:System.Windows.UIElement>, 例如) 會公開空的「On * 事件」和「OnPreview\*事件」虛擬方法, 其對應至其公用路由事件的清單。 您可以覆寫這些虛擬方法，以實作相關路由事件的類別處理常式。 基底元素類別會使用<xref:System.Windows.EventManager.RegisterClassHandler%28System.Type%2CSystem.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>如先前所述, 將這些虛擬方法註冊為每個這類路由事件的類別處理常式。 On\*Event 虛擬方法可讓您更輕鬆地實作相關路由事件的類別處理，而不需針對每種類型使用靜態建構函式中的特殊初始化功能。 例如, 您可以藉由覆寫<xref:System.Windows.UIElement.DragEnter> <xref:System.Windows.UIElement.OnDragEnter%2A>虛擬方法, 為任何<xref:System.Windows.UIElement>衍生類別中的事件加入類別處理。 在此覆寫當中，您可以處理路由事件、引發其他事件、初始化類別專屬的邏輯 (其可能會變更執行個體的項目屬性) 或處理這些動作的任意組合。 一般來說，即使您將事件標記為已處理，也應該在這類覆寫中呼叫基底實作。 強烈建議您呼叫基底實作，因為虛擬方法是位於基底類別上。 基本上，系統會取代從每個虛擬方法呼叫基底實作的標準受保護虛擬模式，並平行處理類似的路由事件類別處理原生機制，藉此在任何給定的執行個體上呼叫類別階層架構中所有類別的類別處理常式 (從最高衍生性類別的處理常式開始，繼續往基底類別處理常式進行)。 如果您的類別必須刻意變更基底類別處理邏輯，您就應該省略基底實作呼叫。 要先覆寫程式碼再呼叫基底實作，或先呼叫基底實作再覆寫程式碼，則取決於您實作的性質而定。  
  
#### <a name="input-event-class-handling"></a>輸入事件類別處理  
 系統會登錄所有類別處理常式虛擬方法，因此只有當任何共用的事件資料都尚未標示為已處理的情況下，才會進行叫用。 此外，針對唯一的輸入事件，通道和事件反昇版本通常會循序引發，並共用事件資料。 這項作業需要一組指定的輸入事件處理常式 (其中一個是通道版本，另一個為事件反昇版本)，因此您不用立即將事件標記為已處理。 如果您實作通道類別處理虛擬方法，將事件標記為已處理，就無法叫用事件反昇類別處理常式 (亦無法針對通道或事件反昇事件叫用任何一般登錄的執行個體處理常式)。  
  
 完成節點上的類別處理之後，系統就會考慮採用執行個體接聽程式。  
  
<a name="AddingInstanceHandlersthatAreRaisedEvenWhenEventsareMarkedHandled"></a>   
## <a name="adding-instance-handlers-that-are-raised-even-when-events-are-marked-handled"></a>即使在事件標示為已處理時，仍要新增引發的執行個體處理常式  
 <xref:System.Windows.UIElement.AddHandler%2A>方法會提供特定的多載, 可讓您加入事件系統每次事件到達路由中的處理專案時叫用的處理常式, 即使某個其他處理常式已經調整事件資料以標示事件已處理。 這並不常用。 一般而言，不論事件在項目樹狀結構中的處理位置為何，您都可以寫入處理常式來調整可能會受到事件影響之應用程式程式碼的所有區域 (即使需要多個結果亦可)。 此外，通常需要回應該事件的只有一個項目，而且適當的應用程式邏輯也已經發生。 但您可以針對例外狀況使用 `handledEventsToo` 多載，在這種案例中，項目樹狀結構或複合控制項中的其他項目已將事件標示為已處理，但項目樹狀結構中較高或較低的其他項目 (取決於路由) 仍想叫用自己的處理常式。  
  
#### <a name="when-to-mark-handled-events-as-unhandled"></a>標示未處理事件的時機  
 一般來說, 已標示為已處理的路由事件不應標記為<xref:System.Windows.RoutedEventArgs.Handled%2A>未處理 ( `false`設定回), 即使處理常式`handledEventsToo`是作用於亦然。 不過，有些輸入事件擁有高層級和低層級的事件呈現方式，當高層級的事件在樹狀結構的某個位置，低層級的事件在另一個位置時，其呈現方式可能會重疊。 例如, 請考慮子專案接聽高階索引鍵事件的情況, 例如<xref:System.Windows.UIElement.TextInput> , 當父元素接聽較低層級的事件<xref:System.Windows.UIElement.KeyDown>時 (例如)。 如果父項目處理了低層級的事件，就可能會隱藏子項目中較高層級的事件 (即使子項目直覺上應具有處理事件的優先機會)。  
  
 在這些情況下，可能需要將處理常式新增至低層級事件的父項目和子項目。 子項目處理常式實作可能會將低層級事件標示為已處理，但父項目處理常式實作會再將其設為未處理，以便樹狀結構更上方的項目 (以及高層級的事件) 有機會回應。 這種情況應該相當少見。  
  
<a name="Deliberately_Suppressing_Input_Events_for_Control"></a>   
## <a name="deliberately-suppressing-input-events-for-control-compositing"></a>刻意隱藏複合控制項的輸入事件  
 路由事件類別處理的主要使用案例多是針對輸入事件和複合控制項。 從定義上來看，複合控制項是由多個實用的控制項或控制項基底類別組成。 通常，控制項作者希望能合併每個子元件可能引發之所有可能的輸入事件，以將整個控制項回報為單一的事件來源。 而在某些情況下，控制項作者可能會想要完全隱藏元件的事件，或是換成元件定義的事件，以提供詳細資訊或表示更具體的行為。 任何元件作者立即可以看見的標準範例, 就是如何[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.Button>處理任何滑鼠事件, 最後會解析為<xref:System.Windows.Controls.Primitives.ButtonBase.Click>所有按鈕都具有的直覺事件: 事件。  
  
 <xref:System.Windows.FrameworkElement> <xref:System.Windows.UIElement> <xref:System.Windows.UIElement>基類 (<xref:System.Windows.Controls.Primitives.ButtonBase>)衍生<xref:System.Windows.Controls.Control>自, 而後者又衍生自和, 而控制項輸入處理所需的許多事件基礎結構在層級都有提供。 <xref:System.Windows.Controls.Button> 特別<xref:System.Windows.UIElement>是處理在其<xref:System.Windows.Input.Mouse>界限內處理滑鼠游標之點擊測試的一般事件, 並針對最常見的<xref:System.Windows.UIElement.MouseLeftButtonDown>按鈕動作 (例如) 提供不同的事件。 <xref:System.Windows.UIElement>也提供空的虛擬<xref:System.Windows.UIElement.OnMouseLeftButtonDown%2A>做為的預先註冊類別<xref:System.Windows.UIElement.MouseLeftButtonDown>處理常式, <xref:System.Windows.Controls.Primitives.ButtonBase>並覆寫它。 同樣地<xref:System.Windows.Controls.Primitives.ButtonBase> , 會使用的<xref:System.Windows.UIElement.MouseLeftButtonUp>類別處理常式。 在傳遞事件資料的覆寫中, 此執行會將設定<xref:System.Windows.RoutedEventArgs> <xref:System.Windows.RoutedEventArgs.Handled%2A>為`true`來將該實例標示為已處理, 而相同的事件資料則會沿著其他類別處理常式的其餘路由繼續進行。同時也是實例處理常式或事件 setter。 此外, <xref:System.Windows.Controls.Primitives.ButtonBase.OnMouseLeftButtonUp%2A>覆寫接著會<xref:System.Windows.Controls.Primitives.ButtonBase.Click>引發事件。 大部分接聽程式的最終結果會是<xref:System.Windows.UIElement.MouseLeftButtonDown>和<xref:System.Windows.UIElement.MouseLeftButtonUp>事件「消失」, <xref:System.Windows.Controls.Primitives.ButtonBase.Click>並改為取代, 因為已知此事件是源自 true 按鈕而非部分, 所以有更多意義的事件按鈕的複合部分, 或從某個其他專案中完全移除。  
  
<a name="WorkingAroundEventSuppressionByControls"></a>   
### <a name="working-around-event-suppression-by-controls"></a>處理控制項的事件隱藏項目  
 有時候，在個別控制項當中的這個事件隱藏行為，可能會干擾應用程式事件處理邏輯的部分一般目的。 比方說, 如果您的應用程式有一個<xref:System.Windows.UIElement.MouseLeftButtonDown>位於應用程式根項目的處理常式, 您會注意到在按鈕上按下滑鼠時, <xref:System.Windows.UIElement.MouseLeftButtonDown>不會叫<xref:System.Windows.UIElement.MouseLeftButtonUp>用根層級的或處理常式。 事件本身實際上已經事件反昇 (同樣地，事件路由並未真正結束，但路由事件系統會在標記為已處理之後，變更其處理常式的引動過程行為)。 當路由事件到達按鈕時, <xref:System.Windows.Controls.Primitives.ButtonBase> <xref:System.Windows.Controls.Primitives.ButtonBase.Click>會將類別處理<xref:System.Windows.UIElement.MouseLeftButtonDown>標示為已處理, 因為它想要以更多意義來取代事件。 因此, 將不<xref:System.Windows.UIElement.MouseLeftButtonDown>會叫用路由上進一步的任何標準處理常式。 您可以使用下列兩種技術，確保處理常式在這種情況下仍會受到叫用。  
  
 第一種方法是使用的`handledEventsToo` <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>簽章, 故意加入處理常式。 這個方法的限制是，這項附加事件處理常式的技術僅可以透過程式碼進行，而不能從標記進行。 透過 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，將事件處理常式名稱指定為事件屬性值的簡單語法不會啟用該行為。  
  
 第二個技術只適用於輸入事件，其中路由事件的通道和事件反昇版本是成對的。 針對這些路由事件，您可以改為將處理常式新增至預覽/通道對等路由事件。 假設您在應用程式項目樹狀結構中的某些祖系項目層級附加預覽處理常式，該路由事件會從根目錄開始通過路由，因此按鈕類別處理程式碼不會攔截此事件。 如果您使用這種方式，在將任何預覽事件標示為已處理時，請務必小心。 針對在根項目處理<xref:System.Windows.UIElement.PreviewMouseLeftButtonDown>的所提供的範例, 如果您在處理常式執行中<xref:System.Windows.RoutedEventArgs.Handled%2A>將事件標記為, <xref:System.Windows.Controls.Primitives.ButtonBase.Click>您實際上會隱藏事件。 這通常是不合理的行為。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.EventManager>
- [預覽事件](preview-events.md)
- [建立自訂路由事件](how-to-create-a-custom-routed-event.md)
- [路由事件概觀](routed-events-overview.md)

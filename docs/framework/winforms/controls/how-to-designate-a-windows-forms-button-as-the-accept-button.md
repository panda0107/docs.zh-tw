---
title: 將按鈕指定為 [接受] 按鈕
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- buttons [Windows Forms], default on Windows Forms
- Accept button on Windows Forms
- Button control [Windows Forms], designating as default
- Windows Forms controls, default button on form
ms.assetid: 22cc9da6-b913-4e04-9554-dee443ac5c3a
ms.openlocfilehash: 1063f649768cac2c866390718b261a21e18ec4d3
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2020
ms.locfileid: "76743277"
---
# <a name="how-to-designate-a-windows-forms-button-as-the-accept-button"></a>如何：將 Windows Form 中的 Button 指定為接受按鈕
在任何 Windows Form 上，您都可以將 <xref:System.Windows.Forms.Button> 控制項指定為 [接受] 按鈕，也稱為 [預設] 按鈕。 每當使用者按下 ENTER 鍵時，不論表單上的其他控制項有焦點，都會按一下 [預設] 按鈕。  
  
> [!NOTE]
> 這種情況的例外狀況是當具有焦點的控制項是另一個按鈕時，在此情況下，將會按一下具有焦點的按鈕（或多行文字方塊），或陷印 ENTER 鍵的自訂控制項。  
  
### <a name="to-designate-the-accept-button"></a>若要指定接受按鈕  
  
1. 將表單的 <xref:System.Windows.Forms.Form.AcceptButton%2A> 屬性設定為適當的 <xref:System.Windows.Forms.Button> 控制項。  
  
    ```vb  
    Private Sub SetDefault(ByVal myDefaultBtn As Button)  
      Me.AcceptButton = myDefaultBtn   
    End Sub  
    ```  
  
    ```csharp  
    private void SetDefault(Button myDefaultBtn)  
    {  
       this.AcceptButton = myDefaultBtn;  
    }  
    ```  
  
    ```cpp  
    private:  
       void SetDefault(Button ^ myDefaultBtn)  
       {  
          this->AcceptButton = myDefaultBtn;  
       }  
    ```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Forms.Form.AcceptButton%2A>
- [Button 控制項概觀](button-control-overview-windows-forms.md)
- [選取 Windows Forms Button 控制項的方法](ways-to-select-a-windows-forms-button-control.md)
- [操作說明：回應 Windows Forms Button 按一下動作](how-to-respond-to-windows-forms-button-clicks.md)
- [操作說明：將 Windows Forms 中的 Button 指定為取消按鈕](how-to-designate-a-windows-forms-button-as-the-cancel-button.md)
- [Button 控制項](button-control-windows-forms.md)

---
title: 部分方法
ms.date: 07/20/2015
f1_keywords:
- vb.PartialMethod
- PartialMethod
helpviewer_keywords:
- custom logic into code [Visual Basic]
- partial methods [Visual Basic]
- partial [Visual Basic], methods [Visual Basic]
- methods [Visual Basic], partial methods
- inserting custom logic into code
ms.assetid: 74b3368b-b348-44a0-a326-7d7dc646f4e9
ms.openlocfilehash: 7abf0565a985f1fb44fcf2bb91b9220d57a10f20
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74352629"
---
# <a name="partial-methods-visual-basic"></a>部分方法 (Visual Basic)
部分方法可讓開發人員在程式碼中插入自訂邏輯。 一般來說，程式碼是設計工具產生之類別的一部分。 部分方法定義于程式碼產生器所建立的部分類別中，而且通常用來提供已變更專案的通知。 它們可讓開發人員指定自訂行為，以回應變更。  
  
 程式碼產生器的設計工具只會定義方法簽章，以及一或多個對方法的呼叫。 如果開發人員想要自訂所產生程式碼的行為，則可以提供方法的實作為方式。 當未提供任何執行時，編譯器會移除對方法的呼叫，而不會產生額外的效能負擔。  
  
## <a name="declaration"></a>宣告  
 產生的程式碼會將關鍵字 `Partial` 放在簽章行開頭，以標記部分方法的定義。  
  
```vb  
Partial Private Sub QuantityChanged()  
End Sub  
```  
  
 定義必須符合下列條件：  
  
- 此方法必須是 `Sub`，而不是 `Function`。  
  
- 方法的主體必須保留空白。  
  
- 存取修飾詞必須 `Private`。  
  
## <a name="implementation"></a>實作  
 此實作為主要的部分方法。 此實作為定義的一部分，通常是在不同的部分類別中，而且是由想要擴充所產生程式碼的開發人員所撰寫。  
  
```vb  
Private Sub QuantityChanged()  
'    Code for executing the desired action.  
End Sub  
```  
  
 上一個範例會完全複製宣告中的簽章，但可能會有變化。 特別是，可以加入其他修飾詞，例如 `Overloads` 或 `Overrides`。 只允許一個 `Overrides` 修飾詞。 如需方法修飾詞的詳細資訊，請參閱[Sub 語句](../../../../visual-basic/language-reference/statements/sub-statement.md)。  
  
## <a name="use"></a>用法  
 您可以呼叫部分方法，就像呼叫任何其他 `Sub` 程式一樣。 如果已執行方法，則會評估引數，並執行方法的主體。 不過，請記住，執行部分方法是選擇性的。 如果未執行方法，則呼叫它不會有任何作用，而且不會評估當做引數傳遞至方法的運算式。  
  
## <a name="example"></a>範例  
 在名為 .vb 的檔案中，定義具有 `Quantity` 屬性的 `Product` 類別。  
  
 [!code-vb[VbVbalrPartialMeths#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrPartialMeths/VB/Class1.vb#4)]  
  
 在名為 .vb 的檔案中，提供 `QuantityChanged`的執行。  
  
 [!code-vb[VbVbalrPartialMeths#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrPartialMeths/VB/Class1.vb#5)]  
  
 最後，在專案的 Main 方法中，宣告 `Product` 實例，並為其 `Quantity` 屬性提供初始值。  
  
 [!code-vb[VbVbalrPartialMeths#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrPartialMeths/VB/Class1.vb#6)]  
  
 此時應該會出現訊息方塊，顯示此訊息：  
  
 `Quantity was changed to 100`  
  
## <a name="see-also"></a>另請參閱

- [Sub 陳述式](../../../../visual-basic/language-reference/statements/sub-statement.md)
- [Sub 程序](./sub-procedures.md)
- [選擇性參數](./optional-parameters.md)
- [Partial](../../../../visual-basic/language-reference/modifiers/partial.md)
- [LINQ to SQL 中的程式碼產生](../../../../framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)
- [使用部分方法新增商務邏輯](../../../../framework/data/adonet/sql/linq/adding-business-logic-by-using-partial-methods.md)

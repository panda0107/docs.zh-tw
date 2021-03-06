---
title: 必須有陳述式結尾
ms.date: 07/20/2015
f1_keywords:
- bc30205
- vbc30205
helpviewer_keywords:
- BC30205
ms.assetid: 53c7f825-a737-4b76-a1fa-f67745b8bd40
ms.openlocfilehash: 1ce5c793a09df34ac17e70e3253e98108bf76fb8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "61803315"
---
# <a name="end-of-statement-expected"></a>必須有陳述式結尾
陳述式語法上完成，但其他程式設計項目會遵循完成陳述式的項目。 需要在每個陳述式結尾的行結束字元。
  
 行結束字元會分成幾行中的 Visual Basic 原始程式檔中的字元。 範例的行結束字元是 Unicode 歸位字元傳回字元 （HD），Unicode 換行字元 （& HA），和 Unicode 歸位字元後面接著 Unicode 換行字元。 如需行結束字元的詳細資訊，請參閱[Visual Basic 語言規格](~/_vblang/spec/lexical-grammar.md#line-terminators)。
  
 **錯誤 ID:** BC30205
  
## <a name="to-correct-this-error"></a>更正這個錯誤
  
1. 檢查看看是否兩個不同的陳述式不小心存放在同一行。
  
2. 完成陳述式的項目之後插入的行結束字元。
  
## <a name="see-also"></a>另請參閱

- [如何：在程式碼內中斷和合併陳述式](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
- [陳述式](../../../visual-basic/programming-guide/language-features/statements.md)

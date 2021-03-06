---
title: 公用
ms.date: 07/20/2015
f1_keywords:
- vb.Public
helpviewer_keywords:
- Public keyword [Visual Basic]
- Public keyword [Visual Basic], syntax
- Public access modifier
ms.assetid: 284c9e1b-ed23-499b-9bc9-ad87c11485a5
ms.openlocfilehash: 35bf1a65e0b8f24a1263adc480719c69b95dff9b
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351286"
---
# <a name="public-visual-basic"></a>Public (Visual Basic)
指定一個或多個宣告的程式設計項目沒有存取限制。  
  
## <a name="remarks"></a>備註  
 如果您要發佈元件或元件集（例如類別庫），您通常會想要讓程式設計項目可供與您的元件互通的任何程式碼存取。 若要對專案授與這類無限制存取，您可以使用 `Public`來宣告。  
  
 公用存取是程式設計項目的一般層級，當您不需要限制它的存取權時。 請注意，在介面、模組、類別或結構內宣告之元素的存取層級預設為 `Public` 如果您未將它宣告為。  
  
## <a name="rules"></a>規則  
  
- **宣告內容。** 您只能在模組、介面或命名空間層級使用 `Public`。 這表示 `Public` 元素的宣告內容必須是原始程式檔、命名空間、介面、模組、類別或結構，而且不能是程式。  
  
## <a name="behavior"></a>行為  
  
- **存取層級。** 所有可存取模組、類別或結構的程式碼都可以存取其 `Public` 元素。  
  
- **預設存取。** 程式內的區域變數預設為公用存取，而且您不能在這些變數上使用任何存取修飾詞。  
  
- **存取修飾詞。** 指定存取層級的關鍵字稱為*存取*修飾詞。 如需存取修飾詞的比較，請參閱[Visual Basic 中的存取層級](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
 `Public` 修飾詞可用於以下內容：  
  
 [Class 陳述式](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Const 陳述式](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Declare 陳述式](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Delegate 陳述式](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Dim 陳述式](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Enum 陳述式](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Event 陳述式](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function 陳述式](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface 陳述式](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Module 陳述式](../../../visual-basic/language-reference/statements/module-statement.md)  
  
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Property 陳述式](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Structure 陳述式](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub 陳述式](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>另請參閱

- [Protected](../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)
- [Private](../../../visual-basic/language-reference/modifiers/private.md)
- [Private Protected](private-protected.md)
- [Protected Friend](protected-friend.md)
- [Visual Basic 中的存取層級](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [程序](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [結構](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [物件和類別](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)

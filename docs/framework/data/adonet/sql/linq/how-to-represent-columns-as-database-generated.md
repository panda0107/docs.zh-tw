---
title: 作法：將資料行表示為資料庫產生的資料行
ms.date: 03/30/2017
ms.assetid: 6524b8a6-e5d2-4a3b-8e08-beafc4a84fd2
ms.openlocfilehash: bb9510986581ad6d3bcd0711aed681ef3a7c4e45
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781790"
---
# <a name="how-to-represent-columns-as-database-generated"></a>HOW TO：將資料行表示為資料庫產生的資料行
使用屬性[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] （ <xref:System.Data.Linq.Mapping.ColumnAttribute> attribute）上的<xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>屬性（property）來指定欄位或屬性（property），以表示資料庫產生的資料行。  
  
 如需程式碼範例，請參閱 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>。  
  
### <a name="to-designate-a-field-or-property-as-representing-a-database-generated-column"></a>若要指定欄位或屬性以表示資料庫產生的資料行  
  
1. 將 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> 屬性 (Property) 加入至 <xref:System.Data.Linq.Mapping.ColumnAttribute> 屬性 (Attribute)。  
  
2. 將屬性 (Property) 值設定為 `true`。  
  
## <a name="see-also"></a>另請參閱

- [LINQ to SQL 物件模型](the-linq-to-sql-object-model.md)
- [如何：使用程式碼編輯器自訂實體類別](how-to-customize-entity-classes-by-using-the-code-editor.md)

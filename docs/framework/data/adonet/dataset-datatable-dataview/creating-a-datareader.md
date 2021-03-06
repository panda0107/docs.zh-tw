---
title: 建立 DataReader
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49d4422a-7464-4ab8-8ec7-90185fde3ecf
ms.openlocfilehash: 696eb4dfc334390e1968dd317d441f3c987a1f77
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040115"
---
# <a name="creating-a-datareader"></a>建立 DataReader
<xref:System.Data.DataTable> 和 <xref:System.Data.DataSet> 類別 (Class) 具有 <xref:System.Data.DataTable.CreateDataReader%2A> 方法，可以用一或多個唯讀的順向結果集來傳回 <xref:System.Data.DataTable> 的內容或 <xref:System.Data.DataSet> 物件的 <xref:System.Data.DataSet.Tables%2A> 集合內容。  
  
## <a name="example"></a>範例  
 下列的主控台應用程式會建立 <xref:System.Data.DataTable> 執行個體 (Instance)。 然後，此範例會將填滿的 <xref:System.Data.DataTable> 傳遞至呼叫 <xref:System.Data.DataTable.CreateDataReader%2A> 方法的程式，而這個方法會逐一查看包含在 <xref:System.Data.DataTableReader>內的結果。  
  
 [!code-csharp[DataWorks DataTable.CreateDataReader#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTable.CreateDataReader/CS/source.cs#1)]
 [!code-vb[DataWorks DataTable.CreateDataReader#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTable.CreateDataReader/VB/source.vb#1)]  
  
 此範例會在主控台視窗中顯示以下輸出：  
  
```output  
1 Mary  
2 Andy  
3 Peter  
4 Russ  
```  
  
## <a name="see-also"></a>請參閱

- <xref:System.Data.DataTable.CreateDataReader%2A>
- <xref:System.Data.DataSet.CreateDataReader%2A>
- [DataTableReader](datatablereaders.md)
- [ADO.NET 概觀](../ado-net-overview.md)

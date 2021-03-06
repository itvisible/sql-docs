---
title: "SHAPE (DMX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2016"
ms.prod: analysis-services
ms.prod_service: "analysis-services"
ms.service: ""
ms.component: ""
ms.reviewer: ""
ms.suite: "pro-bi"
ms.technology: 
  
ms.component: data-mining
ms.tgt_pltfrm: ""
ms.topic: "language-reference"
f1_keywords: 
  - "SHAPE"
dev_langs: 
  - "DMX"
helpviewer_keywords: 
  - "SHAPE statement"
  - "multiple data sources"
ms.assetid: b9526ec2-40bc-4bf5-b4e5-774f71075065
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# &lt;source data query&gt; - SHAPE
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Combines queries from multiple data sources into a single hierarchical table (that is, a table with nested tables), which becomes the case table for the mining model.  
  
 The complete syntax of the **SHAPE** command is documented in the [!INCLUDE[msCoName](../includes/msconame-md.md)] Data Access Components (MDAC) Software Development Kit (SDK).  
  
## Syntax  
  
```  
  
SHAPE {<master query>}  
APPEND ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS < column table name>  
...  
]       
```  
  
## Arguments  
 *master query*  
 The query returning the parent table.  
  
 *child table query*  
 The query returning the nested table.  
  
 *master column*  
 The column in the parent table to identify child rows from the result of a child table query.  
  
 *child column*  
 The column in the child table to identify the parent row from the result of a master query.  
  
 *column table name*  
 The newly appended column name in the parent table for the nested table.  
  
## Remarks  
 You must order the queries by the column that relates the parent table and child table.  
  
## Examples  
 You can use the following example within an [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) statement to train a model containing a nested table. The two tables within the **SHAPE** statement are related through the **OrderNumber** column.  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## See Also  
 [&#60;source data query&#62;](../dmx/source-data-query.md)   
 [Data Mining Extensions &#40;DMX&#41; Data Definition Statements](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40;DMX&#41; Data Manipulation Statements](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40;DMX&#41; Statement Reference](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

---
title: 'Alternativas: Utilizar instrucciones SQL | Documentos de Microsoft'
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a8480e03fe09d640e02bb387e56e2c44556c6d4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="alternatives-using-sql-statements"></a>Alternativas: Utilizar instrucciones SQL
ADO también permite utilizar comandos como alternativa a sus propiedades y métodos integrados para modificar los datos. Dependiendo de su proveedor, todas las operaciones que se mencionan en esta sección también se podrían realizar pasando comandos a su origen de datos. Por ejemplo, se pueden utilizar instrucciones UPDATE de SQL para modificar datos sin usar la **valor** propiedad de un **campo**. Las instrucciones INSERT de SQL que pueden utilizarse para agregar nuevos registros a un origen de datos, en lugar de con el método ADO **AddNew**. Para obtener más información acerca de SQL o el lenguaje de manipulación de datos del proveedor, consulte la documentación del origen de datos.  
  
 Por ejemplo, puede pasar una cadena SQL que contiene una instrucción DELETE en una base de datos, como se muestra en el código siguiente:  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```

---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7b3d57b868d9602707889c0142d9f0ca7d730c7
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver137"></a>MSSQLSERVER_137
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|137|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P_SCALAR_VAR_NOTFOUND|  
|Texto del mensaje|Debe declarar la variable escalar "%.*ls".|  
  
## <a name="explanation"></a>Explicación  
Este error se produce cuando una variable se utiliza en un script SQL sin declararla primero. En el siguiente ejemplo, se devuelve el error 137 para las instrucciones SET y SELECT porque no se ha declarado **@mycol**.  
  
SET @mycol = 'ContactName'  
  
SELECT @mycol  
  
Una de las causas más complicadas de este error incluye el uso de una variable que se declara fuera de la instrucción EXECUTE. Por ejemplo, la variable **@mycol** especificada en la instrucción SELECT es local para la instrucción SELECT; por tanto, está fuera de la instrucción EXECUTE.  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20);  
  
SET @mycol = 'Name'  
  
EXECUTE ('SELECT @mycol FROM Production.Product;')  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe que cualquier variable que se use en un script SQL se declara antes de utilizarse en otra parte del script.  
  
Vuelva a escribir el script para que no haga referencia a las variables de la instrucción EXECUTE que se declaran fuera de ella. Por ejemplo:  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20)  
  
SET @mycol = 'Name'  
  
EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';)  
  
## <a name="see-also"></a>Ver también  
[EXECUTE &#40;Transact-SQL&#41;](~/t-sql/language-elements/execute-transact-sql.md)  
[Instrucciones SET &#40;Transact-SQL&#41;](~/t-sql/statements/set-statements-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](~/t-sql/language-elements/declare-local-variable-transact-sql.md)  
  

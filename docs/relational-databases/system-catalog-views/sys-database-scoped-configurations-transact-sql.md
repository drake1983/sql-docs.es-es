---
title: Sys.database_scoped_configurations (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
caps.latest.revision: 13
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 373d2933d362f565799518bfe1af516ad1943276
ms.sourcegitcommit: 0cc2cb281e467a13a76174e0d9afbdcf4ccddc29
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2018
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contiene una fila por cada configuración. 
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|Id. de la opción de configuración.|  
|**Nombre**|**nvarchar(60)**|El nombre de la opción de configuración. Para obtener información acerca de las configuraciones posibles, consulte [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|  
|**value**|**SQLVARIANT**|El valor establecido para esta opción de configuración para la réplica principal.|  
|**value_for_secondary**|**SQLVARIANT**|El valor establecido para esta opción de configuración para las réplicas secundarias.|  
|**elevate_online**|**nvarchar(60)** |Conjunto predeterminado de la opción en línea para las operaciones de índice de ámbito de la base de datos |
|**elevate_resumable**|nvarchar(60)|Conjunto predeterminado de la opción reanudable para operaciones de índice de ámbito de la base de datos| 
  
##  <a name="Permissions"></a> Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="remarks"></a>Comentarios  
 Cuando se devuelve NULL como el valor de **value_for_secondary**, esto significa que la base de datos secundaria está establecido en principal.  
 
 Las opciones de configuración con ámbito de base de datos se transfieren con la base de datos. Esto significa que cuando se restaura o adjunta una base de datos, se conservan las opciones de configuración existentes.
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  

---
title: Conjunto de filas DBSCHEMA_CATALOGS | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61e4de1591752919a5916d6044591bda49b14992
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="dbschemacatalogs-rowset"></a>Conjunto de filas DBSCHEMA_CATALOGS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica los atributos físicos asociados a los catálogos que son accesibles desde el sistema de administración de bases de datos (DBMS).  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DBSCHEMA_CATALOGS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|255|Nombre del catálogo. No puede ser null.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción legible de la tabla.|  
|**ROLES**|**DBTYPE_WSTR**||Una lista delimitada por comas de roles a los que pertenece el usuario actual.<br /><br /> Un asterisco (\*) se incluye como una función de si el usuario actual es un servidor o un administrador de base de datos.<br /><br /> **Username** se anexa a **ROLES** si uno de los roles utiliza la seguridad dinámica.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||Fecha de la última modificación del catálogo.|  
  
 El conjunto de filas se ordena en **CATALOG_NAME**.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DBSCHEMA_CATALOGS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema OLE DB](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  

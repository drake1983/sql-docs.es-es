---
title: Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd478b0185feffad77848f5c727c81931d57f9f5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingmodelcontentpmml-rowset"></a>Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Devuelve la estructura XML del modelo de minería de datos. El formato de las cadenas XML sigue el estándar PMML 2.1 (Lenguaje de marcado de modelos de predicción).  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DMSCHEMA_MINING_MODEL_CONTENT_PMML** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||Nombre del catálogo que se rellena con el nombre de la base de datos de la que el modelo es miembro.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||Nombre del esquema sin certificar. Esta columna no es compatible con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**MODEL_NAME**|**DBTYPE_WSTR**||Nombre del modelo. Esta columna no puede contener valores **NULL**.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**||Tipo del modelo. Es una cadena específica del proveedor. Puede ser **NULL**:|  
|**MODEL_GUID**|**DBTYPE_GUID**||GUID que identifica el modelo. Los proveedores que no utilizan GUID para identificar las tablas devuelven **NULL**.|  
|**MODEL_PMML**|**DBTYPE_WSTR**||Representación XML del contenido del modelo en formato PMML.|  
|**SIZE**|**DBTYPE_UI4**||Número de bytes de la secuencia de XML.|  
|**UBICACIÓN**|**DBTYPE_WSTR**||Ubicación del archivo XML. Es **NULL** si no hay ninguna ubicación disponible.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DMSCHEMA_MINING_MODEL_CONTENT_PMML** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

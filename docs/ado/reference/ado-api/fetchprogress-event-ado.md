---
title: Evento FetchProgress (ADO) | Documentos de Microsoft
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
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fea26975fc162f92527f63123eddb95fade8a8e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="fetchprogress-event-ado"></a>Evento FetchProgress (ADO)
El **FetchProgress**eventos se llama periódicamente durante una operación asincrónica prolongada para informar de cuántas filas se han recuperado actualmente en el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Progreso*  
 A **largo** valor que indica el número de registros que han sido recuperados actualmente por la operación de captura.  
  
 *MaxProgress*  
 A **largo** valor que indica el número máximo de registros que se espera recuperar.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado.  
  
 *pRecordset*  
 A **Recordset** objeto que es el objeto para el que se recuperan los registros.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se usa **FetchProgress** con un elemento secundario **Recordset**, tenga en cuenta que la *progreso* y *MaxProgress* se derivan los valores de parámetro desde subyacente [servicio Cursor](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) conjunto de filas. Los valores devueltos representan el número total de registros en el conjunto de filas subyacente, no solo el número de registros en el capítulo actual.  
  
> [!NOTE]
>  Usar **FetchProgress** con Microsoft Visual Basic, Visual Basic 6.0 o posterior es necesario.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)

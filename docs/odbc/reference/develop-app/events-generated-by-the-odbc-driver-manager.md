---
title: Eventos generados por el Administrador de controladores ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], events generated by
- Visual Studio Analyzer [ODBC], driver manager events
ms.assetid: 8c6efbbd-2c7d-4342-aa7b-201f94b3e3e3
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b101cbeaeea86741b92933a0367ff5e084c0a5fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="events-generated-by-the-odbc-driver-manager"></a>Eventos generados por el Administrador de controladores ODBC
> [!IMPORTANT]  
>  Se quitó la compatibilidad con Visual Studio Analyzer a partir de Windows 8 (Visual Studio Analyzer sólo se incluyó en versiones anteriores de Visual Studio.). Para una solución de problemas de mecanismo de forma alternativa, utilizar el seguimiento de BID.  
  
 Eventos generados por el Administrador de controladores ODBC se registran cuando se hace clic en el botón Iniciar Visual Studio Analyzer. La propia herramienta ofrece eventos definidos por el sistema y la capacidad de crear eventos personalizados. Para obtener más información acerca de los eventos, vea el *Guía de referencia de Visual Studio Analyzer* dentro del conjunto de documentación de Visual Studio.  
  
|Eventos de Visual Studio Analyzer|Description|  
|----------------------------------|-----------------|  
|**Llamar a**|Se genera en cada entrada de la API de ODBC.|  
|**ReturnException**|Generado en todos los valores devueltos API de ODBC si el código de retorno es SQL_ERROR.|  
|**ReturnNormal**|Generado en todos los valores devueltos API de ODBC si el código devuelto no es SQL_ERROR.|  
|**Inicio de conexión**|Indica que ha iniciado una conexión. se genera cuando el Administrador de controladores ODBC llama la API de conexión del controlador.|  
|**Conexión completa**|Indica que se ha completado una conexión; se genera cuando las API de conexión del controlador devuelven al administrador de controladores ODBC.|  
|**Inicio de la desconexión**|Se genera cuando el Administrador de controladores ODBC llama el controlador **SQLDisconnect** función.|  
|**Finalización de desconexión**|Cuando el controlador **SQLDisconnect** función devuelve al administrador de controladores ODBC.|  
|**QuerySend**|Se genera cuando el Administrador de controladores ODBC llama el controlador **SQLPrepare**, **SQLExecute**, **SQLExecDirect** funciones, así como funciones de catálogo como **SQLTables** y **SQLColumns**.|  
|**QueryResult**|Se genera cuando el controlador devuelve un conjunto para el Administrador de controladores ODBC para las funciones relacionadas con las consultas de resultados.|  
|**TransactionStart**|Generado cuando una aplicación establece el valor de SQL_ATTR_AUTOCOMMIT como SQL_AUTOCOMMIT_OFF o cuando una aplicación llama correctamente **SQLEndTran**.|  
|**TransactionCommit**|Se genera cuando una aplicación llama **SQLEndTran** para confirmar una transacción local.|  
|**TransactionRollback**|Se genera cuando una aplicación llama **SQLEndTran** para revertir una transacción local.|  
|**JoinDTC**|Se genera cuando el Coordinador de transacciones distribuidas (DTC) se une a una aplicación.|  
|**LeaveDTC**|Se genera cuando una aplicación sale del Coordinador de transacciones distribuidas (DTC).|

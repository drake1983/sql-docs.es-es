---
title: Clase de eventos Broker:Activation | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Broker:Activation event class
ms.assetid: 481d5b13-657e-4b51-8783-ccac3595bd45
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5f77ed8e31137963790eef7e295ab5c506dd00b0
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="brokeractivation-event-class"></a>Broker:Activation, clase de eventos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento **Broker:Activation** cuando un monitor de cola inicia un procedimiento almacenado de activación, envía una notificación QUEUE_ACTIVATION o cuando se cierra un procedimiento almacenado de activación iniciado por un monitor de cola.  
  
## <a name="brokeractivation-event-class-data-columns"></a>Columnas de datos de la clase de eventos Broker:Activation  
  
|Columna de datos|Tipo|Descripción|Número de columna|Filtrable|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ClientProcessID**|**int**|Id. que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|**DatabaseID**|**int**|Identificador de la base de datos especificada mediante la instrucción USE *database* o identificador de la base de datos predeterminada si no se ha emitido la instrucción USE *database*para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**EventClass**|**int**|Tipo de clase de eventos capturado. Es siempre **163** para **Broker:Activation**.|27|no|  
|**EventSequence**|**int**|Número de secuencia de este evento.|51|no|  
|**EventSubClass**|**nvarchar**|Acción específica de la que este evento informa. Los valores pueden ser los siguientes:<br /><br /> **iniciar**:   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha iniciado un procedimiento almacenado de activación.<br /><br /> **finalizado**: el procedimiento almacenado de activación ha terminado con normalidad.<br /><br /> **anulado**: el procedimiento almacenado de activación ha terminado con un error.|21|no|  
|**HostName**|**nvarchar**|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|**IntegerData**|**int**|Número de tareas activas en esta cola.|25|no|  
|**IsSystem**|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|no|  
|**LoginSid**|**imagen**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|**NTDomainName**|**nvarchar**|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|**NTUserName**|**nvarchar**|Nombre del usuario al que pertenece la conexión que generó este evento.|6|Sí|  
|**ObjectID**|**int**|Cola asociada a este evento.|22|no|  
|**ServerName**|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|no|  
|**SPID**|**int**|Identificador de proceso del servidor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna al proceso asociado al cliente.|12|Sí|  
|**StartTime**|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**TransactionID**|**bigint**|Identificador de la transacción asignado por el sistema.|4|no|  
  
  

---
title: sp_change_agent_parameter (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_change_agent_parameter_TSQL
- sp_change_agent_parameter
helpviewer_keywords:
- sp_change_agent_parameter
ms.assetid: f1fbecc7-e64f-405c-8067-6b38c1f3c0a0
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d01a06f119a0c1d7669f0c811e8bee03e5eeb912
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spchangeagentparameter-transact-sql"></a>sp_change_agent_parameter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia un parámetro de un perfil de agente de replicación almacenado en el [MSagent_parameters](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) tabla del sistema. Este procedimiento almacenado se ejecuta en el distribuidor en el que se está ejecutando el agente, en cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_change_agent_parameter [ @profile_id= ] profile_id, [ @parameter_name= ] 'parameter_name', [ @parameter_value= ] 'parameter_value'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_id=**] *profile_id*,  
 Es el identificador del perfil. *profile_id* es **int**, no tiene ningún valor predeterminado.  
  
 [  **@parameter_name=**] **'***parameter_name***'**  
 Es el nombre del parámetro. *parameter_name* es **sysname**, no tiene ningún valor predeterminado. Para los perfiles del sistema, los parámetros que se pueden cambiar dependen del tipo de agente. Para averiguar qué tipo de agente esto *profile_id* representa, busque el *profile_id* columna en el **Msagent_profiles** de tabla y tenga en cuenta el *agent_type*  valor.  
  
> [!NOTE]  
>  Si un parámetro es compatible con un determinado *agent_type*, pero no se ha definido en el perfil del agente, se devuelve un error. Para agregar un parámetro a un perfil de agente que se debe ejecutar [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md).  
  
 Para un agente de instantáneas (*agent_type*=**1**), si se define en el perfil, pueden cambiarse las siguientes propiedades:  
  
-   **70Subscribers**  
  
-   **BcpBatchSize**  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxNetworkOptimization**  
  
-   **Salida**  
  
-   **OutputVerboseLevel**  
  
-   **Tamaño del paquete**  
  
-   **queryTimeout**  
  
-   **StartQueueTimeout**  
  
-   **UsePerArticleContentsView**  
  
 Para un agente de lector del registro (*agent_type*=**2**), si se define en el perfil, pueden cambiarse las siguientes propiedades:  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MessageInterval**  
  
-   **Salida**  
  
-   **OutputVerboseLevel**  
  
-   **Tamaño del paquete**  
  
-   **PollingInterval**  
  
-   **queryTimeout**  
  
-   **ReadBatchSize**  
  
-   **ReadBatchThreshold**  
  
 Para un agente de distribución (*agent_type*=**3**), si se define en el perfil, pueden cambiarse las siguientes propiedades:  
  
-   **BcpBatchSize**  
  
-   **CommitBatchSize**  
  
-   **CommitBatchThreshold**  
  
-   **FileTransferType**  
  
-   **HistoryVerboseLevel**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDeliveredTransactions**  
  
-   **MessageInterval**  
  
-   **Salida**  
  
-   **OutputVerboseLevel**  
  
-   **Tamaño del paquete**  
  
-   **PollingInterval**  
  
-   **queryTimeout**  
  
-   **QuotedIdentifier**  
  
-   **SkipErrors**  
  
-   **TransactionsPerHistory**  
  
 Para un agente de mezcla (*agent_type*=**4**), si se define en el perfil, pueden cambiarse las siguientes propiedades:  
  
-   **AltSnapshotFolder**  
  
-   **BcpBatchSize**  
  
-   **ChangesPerHistory**  
  
-   **DestThreads**  
  
-   **DownloadGenerationsPerBatch**  
  
-   **DownloadReadChangesPerBatch**  
  
-   **DownloadWriteChangesPerBatch**  
  
-   **DynamicSnapshotLocation**  
  
-   **ExchangeType**  
  
-   **FastRowCount**  
  
-   **FileTransferType**  
  
-   **GenerationChangeThreshold**  
  
-   **HistoryVerboseLevel**  
  
-   **InputMessageFile**  
  
-   **InteractiveResolution**  
  
-   **InterruptOnMessagePattern**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDownloadChanges**  
  
-   **MaxUploadChanges**  
  
-   **MetadataRetentionCleanup**  
  
-   **NumDeadlockRetries**  
  
-   **Salida**  
  
-   **OutputMessageFile**  
  
-   **OutputVerboseLevel**  
  
-   **Tamaño del paquete**  
  
-   **ParallelUploadDownload**  
  
-   **PauseOnMessagePattern**  
  
-   **PauseTime**  
  
-   **PollingInterval**  
  
-   **ProcessMessagesAtPublisher**  
  
-   **ProcessMessagesAtSubscriber**  
  
-   **queryTimeout**  
  
-   **QueueSizeMultiplier**  
  
-   **SrcThreads**  
  
-   **StartQueueTimeout**  
  
-   **SyncToAlternate al**  
  
-   **UploadGenerationsPerBatch**  
  
-   **UploadReadChangesPerBatch**  
  
-   **UploadWriteChangesPerBatch**  
  
-   **UseInprocLoader**  
  
-   **Validar**  
  
-   **ValidateInterval**  
  
 Para un agente de lectura de cola (*agent_type*=**9**), si se define en el perfil, pueden cambiarse las siguientes propiedades:  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **Salida**  
  
-   **OutputVerboseLevel**  
  
-   **PollingInterval**  
  
-   **queryTimeout**  
  
-   **ResolverState**  
  
-   **SQLQueueMode**  
  
 Para ver los parámetros que se han definido para un perfil determinado, ejecute **sp_help_agent_profile** y tenga en cuenta el *profile_name* asociados con el *profile_id*. Con el adecuado *profile_id*, a continuación ejecute **sp_help_agent_parameters** con esa *profile_id* para ver los parámetros asociados con el perfil. Parámetros pueden agregarse a un perfil mediante la ejecución de [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md).  
  
 [  **@parameter_value=**] **'***parameter_value***'**  
 Es el nuevo valor del parámetro. *parameter_value* es **nvarchar (255)**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_change_agent_parameter** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_change_agent_parameter**.  
  
## <a name="see-also"></a>Vea también  
 [Perfiles del Agente de replicación](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente de registro del LOG de replicación](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de mezcla de replicación](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de lectura de cola de replicación](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [sp_add_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

---
title: Script de información del distribuidor y del publicador | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Publishers [SQL Server replication], information scripts
- Distributors [SQL Server replication], information scripts
ms.assetid: 8622db47-c223-48fa-87ff-0b4362cd069a
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb479944aed98701bd6ad0fec7cabf4fe1fb4959
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="distributor-and-publisher-information-script"></a>Script de información del distribuidor y del publicador
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este script utiliza tablas del sistema y procedimientos almacenados de replicación para responder a las preguntas más frecuentes sobre los objetos del distribuidor y del publicador. El script se puede utilizar "tal cual" y puede también proporcionar la base para crear scripts personalizados. Para poder ejecutar el script en el entorno, puede que sea necesario realizar las dos modificaciones siguientes:  
  
-   Cambie la línea `use AdventureWorks2012` para utilizar el nombre de la base de datos de publicaciones.  
  
-   Quite los comentarios (`--`) de la línea `exec sp_helparticle @publication='<PublicationName>'` y reemplace \<nombrePublicación> por el nombre de una publicación.  
  
```  
--********** Execute at the Distributor in the master database **********--  
  
USE master;  
go  
  
--Is the current server a Distributor?  
--Is the distribution database installed?  
--Are there other Publishers using this Distributor?  
EXEC sp_get_distributor  
  
--Is the current server a Distributor?  
SELECT is_distributor FROM sys.servers WHERE name='repl_distributor' AND data_source=@@servername;  
  
--Which databases on the Distributor are distribution databases?  
SELECT name FROM sys.databases WHERE is_distributor = 1  
  
--What are the Distributor and distribution database properties?  
EXEC sp_helpdistributor;  
EXEC sp_helpdistributiondb;  
EXEC sp_helpdistpublisher;  
  
--********** Execute at the Publisher in the master database **********--  
  
--Which databases are published for replication and what type of replication?  
EXEC sp_helpreplicationdboption;  
  
--Which databases are published using snapshot replication or transactional replication?  
SELECT name as tran_published_db FROM sys.databases WHERE is_published = 1;  
--Which databases are published using merge replication?  
SELECT name as merge_published_db FROM sys.databases WHERE is_merge_published = 1;  
  
--What are the properties for Subscribers that subscribe to publications at this Publisher?  
EXEC sp_helpsubscriberinfo;  
  
--********** Execute at the Publisher in the publication database **********--  
  
USE AdventureWorks2012;  
go  
  
--What are the snapshot and transactional publications in this database?   
EXEC sp_helppublication;  
--What are the articles in snapshot and transactional publications in this database?  
--REMOVE COMMENTS FROM NEXT LINE AND REPLACE <PublicationName> with the name of a publication  
--EXEC sp_helparticle @publication='<PublicationName>';  
  
--What are the merge publications in this database?   
EXEC sp_helpmergepublication;  
--What are the articles in merge publications in this database?  
EXEC sp_helpmergearticle; -- to return information on articles for a single publication, specify @publication='<PublicationName>'  
  
--Which objects in the database are published?  
SELECT name AS published_object, schema_id, is_published AS is_tran_published, is_merge_published, is_schema_published  
FROM sys.tables WHERE is_published = 1 or is_merge_published = 1 or is_schema_published = 1  
UNION  
SELECT name AS published_object, schema_id, 0, 0, is_schema_published  
FROM sys.procedures WHERE is_schema_published = 1  
UNION  
SELECT name AS published_object, schema_id, 0, 0, is_schema_published  
FROM sys.views WHERE is_schema_published = 1;  
  
--Which columns are published in snapshot or transactional publications in this database?  
SELECT object_name(object_id) AS tran_published_table, name AS published_column FROM sys.columns WHERE is_replicated = 1;  
  
--Which columns are published in merge publications in this database?  
SELECT object_name(object_id) AS merge_published_table, name AS published_column FROM sys.columns WHERE is_merge_published = 1;  
```  
  
## <a name="see-also"></a>Ver también  
 [Preguntas más frecuentes para administradores de replicación](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [sp_get_distributor &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-get-distributor-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_helpreplicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpreplicationdboption-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.procedures &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [sys.servers &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-servers-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  

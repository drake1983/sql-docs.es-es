---
title: sp_addsrvrolemember (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addsrvrolemember
- sp_addsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addsrvrolemember
ms.assetid: 777f0e09-8ee5-4cb2-a3ac-939d02c3cd22
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8d718d3cb44a4a1f148cd92df72dde7465b61762
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spaddsrvrolemember-transact-sql"></a>sp_addsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un inicio de sesión como miembro de un rol fijo de servidor.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @loginame **=** ] **'***inicio de sesión***'**  
 Es el nombre del inicio de sesión que se va a agregar al rol fijo de servidor. *inicio de sesión* es **sysname**, no tiene ningún valor predeterminado. *inicio de sesión* puede ser un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión o un inicio de sesión de Windows. Si el inicio de sesión de Windows no tiene acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todavía, se le concede el acceso automáticamente.  
  
 [ @rolename **=** ] **'***rol***'**  
 Es el nombre del rol fijo de servidor al que se va a agregar el inicio de sesión. *rol* es **sysname**, su valor predeterminado es null y debe ser uno de los siguientes valores:  
  
-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin  

## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Cuando se agrega un inicio de sesión a un rol fijo de servidor, el inicio de sesión obtiene los permisos asociados a dicho rol.  
  
 No se puede cambiar la pertenencia al rol de inicio de sesión sa y pública.  
  
 Utilice sp_addrolemember para agregar a un miembro a una base de datos fija o rol definido por el usuario.  
  
 sp_addsrvrolemember no puede ejecutarse en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol al que se agrega el nuevo miembro.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se agrega el inicio de sesión de Windows `Corporate\HelenS` a la `sysadmin` rol fijo de servidor.  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  

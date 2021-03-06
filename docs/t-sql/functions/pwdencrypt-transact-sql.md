---
title: PWDENCRYPT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PWDENCRYPT
- PWDENCRYPT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PWDENCRYPT function [Transact-SQL]
ms.assetid: 333e9a43-1099-4b9b-b941-4b0b016f47f3
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 974f09b3b98844b91a6ac339411d675c333b3fb6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="pwdencrypt-transact-sql"></a>PWDENCRYPT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor hash de la contraseña de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondiente al valor de entrada que usa la versión actual del algoritmo de hash de contraseñas.  
  
 PWDENCRYPT es una función antigua y puede que no se admita en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En cambio, puede usar [HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md). HASHBYTES proporciona más algoritmos de hash.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PWDENCRYPT ( 'password' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *password*  
 Es la contraseña que se va a cifrar. *password* es **sysname**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary(128)**  
  
## <a name="permissions"></a>Permisos  
 PWDENCRYPT está disponible al público.  
  
## <a name="see-also"></a>Ver también  
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [PWDCOMPARE &#40;Transact-SQL&#41;](../../t-sql/functions/pwdcompare-transact-sql.md)  
  
  

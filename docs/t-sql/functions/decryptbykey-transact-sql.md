---
title: DECRYPTBYKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DecryptByKey_TSQL
- DECRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], DecryptByKey function
- decryption [SQL Server], keys
- decryption [SQL Server], symmetric keys
- DECRYPTBYKEY function
ms.assetid: 6edf121f-ac62-4dae-90e6-6938f32603c9
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 57a2175b3c4096ab9af7203d7f7d3733947f8e78
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Descifra datos utilizando una clave simétrica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *ciphertext*  
 Son datos que se han cifrado con la clave. *ciphertext* es **varbinary**.  
  
 **@ciphertext**  
 Es una variable de tipo **varbinary** que contiene los datos que se han cifrado con la clave.  
  
 *add_authenticator*  
 Indica si se ha cifrado un autenticador junto con el texto simple. Debe ser el mismo valor pasado a EncryptByKey cuando se cifraron los datos. *add_authenticator* es **int**.  
  
 *authenticator*  
 Son los datos de los que se generará un autenticador. Debe coincidir con el valor que se proporcionó para EncryptByKey. *authenticator* es **sysname**.  
  
 **@authenticator**  
 Es una variable que contiene los datos a partir de los cuales se generará un autenticador. Debe coincidir con el valor que se proporcionó para EncryptByKey.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary** con un tamaño máximo de 8000 bytes.
 
Devuelve NULL si la clave simétrica usada para cifrar los datos no está abierta o si *ciphertext* es NULL.
  
## <a name="remarks"></a>Notas  
 DecryptByKey utiliza una clave simétrica. La clave simétrica ya debe estar abierta en la base de datos. Puede haber varias claves abiertas a la vez. No tiene que abrir la clave inmediatamente antes de descifrar el texto cifrado.  
  
 El cifrado y descifrado simétrico es relativamente rápido y se puede adaptar para trabajar con grandes cantidades de datos.  
  
## <a name="permissions"></a>Permisos  
 Requiere que se haya abierto la clave simétrica en la sesión actual. Para más información, vea [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>A. Descifrar utilizando una clave simétrica  
 En el siguiente ejemplo se descifra texto cifrado utilizando una clave simétrica.  
  
```  
-- First, open the symmetric key with which to decrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
GO  
  
-- Now list the original ID, the encrypted ID, and the   
-- decrypted ciphertext. If the decryption worked, the original  
-- and the decrypted ID will match.  
SELECT NationalIDNumber, EncryptedNationalID   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalID))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-decrypting-by-using-a-symmetric-key-and-an-authenticating-hash"></a>B. Descifrar utilizando una clave simétrica y un hash de autenticación  
 En el siguiente ejemplo se descifran datos que se cifraron mediante un autenticador.  
  
```  
-- First, open the symmetric key with which to decrypt the data  
OPEN SYMMETRIC KEY CreditCards_Key11  
   DECRYPTION BY CERTIFICATE Sales09;  
GO  
  
-- Now list the original card number, the encrypted card number,  
-- and the decrypted ciphertext. If the decryption worked,   
-- the original number will match the decrypted number.  
SELECT CardNumber, CardNumber_Encrypted   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByKey(CardNumber_Encrypted, 1 ,   
    HashBytes('SHA1', CONVERT(varbinary, CreditCardID))))   
    AS 'Decrypted card number' FROM Sales.CreditCard;  
GO  
  
```  
  
## <a name="see-also"></a>Ver también  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Elegir un algoritmo de cifrado](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  

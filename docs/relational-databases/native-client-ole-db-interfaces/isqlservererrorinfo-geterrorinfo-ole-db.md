---
title: 'ISQLServerErrorInfo:: GetErrorInfo (OLE DB) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
ms.assetid: 83265c9c-eaf9-41f0-9f73-b0ae0972f0d5
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 564ce1ad8361e2eddbc858ce78fc17e3cf3cac75
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Devuelve un puntero a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la estructura SSERRORINFO del proveedor OLE DB de Native Client la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detalles del error.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define la **ISQLServerErrorInfo** interfaz de errores. Esta interfaz devuelve los detalles de una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error, incluso la gravedad y estado.  

  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ppSSErrorInfo*[out]  
 Un puntero a una estructura SSERRORINFO. Si el método produce un error o no hay ningún [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información asociada con el error, el proveedor no asigna memoria y se asegura de que el *ppSSErrorInfo* argumento es un puntero nulo en la salida.  
  
 *ppErrorStrings*[out]  
 Un puntero a una cadena de caracteres Unicode. Si el método produce un error o no hay ningún [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información asociada con un error, el proveedor no asigna memoria y se asegura de que el *ppErrorStrings* argumento es un puntero nulo en la salida. Liberar la *ppErrorStrings* argumento con el **IMalloc:: Free** método libera los tres miembros individuales de una cadena de la estructura SSERRORINFO devuelta, tal y como se asigna la memoria en un bloque.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_INVALIDARG  
 Ya sea la *ppSSErrorInfo* o *ppErrorStrings* argumento era nulo.  
  
 E_OUTOFMEMORY  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB no pudo asignar memoria suficiente para completar la solicitud.  
  
## <a name="remarks"></a>Comentarios  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client asigna memoria para las cadenas SSERRORINFO y OLECHAR devueltas a través de los punteros pasados por el consumidor. El consumidor debe desasignar esta memoria utilizando la **IMalloc:: Free** método cuando ya no necesita acceso a los datos de error.  
  
 La estructura SSERRORINFO se define como sigue:  
  
```  
typedef struct tagSSErrorInfo  
   {  
   LPOLESTR pwszMessage;  
   LPOLESTR pwszServer;  
   LPOLESTR pwszProcedure;  
   LONG lNative;  
   BYTE bState;  
   BYTE bClass;  
   WORD wLineNumber;  
   }  
SSERRORINFO;  
```  
  
|Miembro|Description|  
|------------|-----------------|  
|*pwszMessage*|El mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El mensaje se devuelve a través de la **IErrorInfo:: GetDescription** método.|  
|*pwszServer*|El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que se ha producido el error.|  
|*pwszProcedure*|El nombre del procedimiento almacenado que genera el error si éste se produjo en un procedimiento almacenado; de lo contrario, una cadena vacía.|  
|*lNative*|El número de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El número de error es idéntico al devuelto en el *plNativeError* parámetro de la **ISQLErrorInfo:: GetSQLInfo** método.|  
|*bState*|El estado del error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|La gravedad del error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Cuando sea aplicable, la línea de un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que generó el mensaje de error. Si no hay implicado ningún procedimiento, se utiliza el valor predeterminado 1.|  
  
 Punteros en la estructura de hacer referencia a direcciones en la cadena devuelta en el *ppErrorStrings* argumento.  
  
## <a name="see-also"></a>Vea también  
 [ISQLServerErrorInfo & #40; OLE DB & #41;](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)   
 [RAISERROR & #40; Transact-SQL & #41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

---
title: 'PDO:: exec | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 359a87c6-c13a-4518-8f23-a922e7f3b171
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 205d07a7c64573bf970ebda1fc32950b7b362e37
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="pdoexec"></a>PDO::exec
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Prepara y ejecuta una instrucción SQL en una única llamada a una función, y devuelve el número de filas a las que afecta la instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int PDO::exec ($statement)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$statement*: una cadena que contiene la instrucción SQL que se ejecutará.  
  
## <a name="return-value"></a>Valor devuelto  
Un valor entero que notifica el número de filas afectadas.  
  
## <a name="remarks"></a>Comentarios  
Si *$statement* contiene varias instrucciones SQL, solo se notifica el recuento de filas afectadas de la última instrucción.  
  
PDO::exec no devuelve los resultados de una instrucción SELECT.  
  
Los siguientes atributos afectan al comportamiento de PDO::exec:  
  
-   PDO::ATTR_DEFAULT_FETCH_MODE  
  
-   PDO::SQLSRV_ATTR_ENCODING  
  
-   PDO::SQLSRV_ATTR_QUERY_TIMEOUT  
  
Para obtener más información, consulte [PDO::setAttribute](../../connect/php/pdo-setattribute.md). 
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo se eliminan las filas de Table1 que incluyen "xxxyy" en col1. En el ejemplo se informa de cuántas filas se han eliminado.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec("use Test");  
   $ret = $c->exec("delete from Table1 where col1 = 'xxxyy'");  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  

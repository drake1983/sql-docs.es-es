---
title: Método getPrimaryKeys (SQLServerDatabaseMetaData) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getPrimaryKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebfe236a-dc02-493e-a3ab-5353d3769e36
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15e8882067a67ec5d276e23c7cb3d2ea3684bf38
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getprimarykeys-method-sqlserverdatabasemetadata"></a>Método getPrimaryKeys (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de las columnas de clave principal de la tabla determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getPrimaryKeys(java.lang.String cat,  
                                         java.lang.String schema,  
                                         java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *CAT*  
  
 A **cadena** que contiene el nombre del catálogo.  
  
 *schema*  
  
 A **cadena** que contiene el nombre del esquema.  
  
 *table*  
  
 A **cadena** que contiene el nombre de tabla.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getPrimaryKeys especificado por el método getPrimaryKeys en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getPrimaryKeys contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|String|El nombre de la base de datos en el que reside la tabla especificada.|  
|TABLE_SCHEM|String|El esquema para la tabla.|  
|TABLE_NAME|String|Nombre de la tabla.|  
|COLUMN_NAME|String|Nombre de la columna.|  
|KEY_SEQ|short|Número de secuencia de la columna en una clave principal en varias columnas.|  
|PK_NAME|String|Nombre de la clave principal.|  
  
> [!NOTE]  
>  Para obtener más información acerca de los datos devueltos por el método getPrimaryKeys, vea "sp_pkeys (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getPrimaryKeys para devolver información sobre las claves principales de la tabla Person.Contact en la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo.  
  
```  
public static void executeGetPrimaryKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getPrimaryKeys("AdventureWorks", "Person", "Contact");  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

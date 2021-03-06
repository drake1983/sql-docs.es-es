---
title: Nuevas características de fecha y hora con versiones anteriores de servidor SQL (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5cb50889a9cb584e5f22d5f2e77960dba567fda1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>Nuevas características de fecha y hora con versiones anteriores de servidor SQL (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tema describe el comportamiento esperado cuando una aplicación cliente que utiliza características mejorada fecha y hora se comunica con una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]y cuando un cliente compilado con una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] envía comandos a un servidor que admite características mejoradas de fecha y hora.  
  
## <a name="down-level-client-behavior"></a>Comportamiento del cliente de nivel inferior  
 Aplicaciones cliente que utilizan una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ver los tipos de fecha y hora nueva como **nvarchar** columnas. El contenido de las columnas son representaciones de literales. Para obtener más información, vea la sección "Formatos de datos: cadenas y literales" de [compatibilidad de tipos de datos para mejoras de hora y fecha de OLE DB](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md). El tamaño de columna es la longitud máxima del literal para la precisión especificada para la columna.  
  
 Las API de catálogo devolverán metadatos coherentes con el código de tipo de datos de nivel inferior devuelve al cliente (por ejemplo, **nvarchar**) y la representación asociada de nivel inferior (por ejemplo, el formato literal adecuado). Sin embargo, el nombre del tipo de datos devuelto será el nombre del tipo real de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Cuando se ejecuta una aplicación de cliente de nivel inferior en un [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o posterior) en los cambios de esquema a la fecha y hora se realizaron los tipos de servidor, el comportamiento esperado es como sigue:  
  
|Tipo de cliente OLE DB|Tipo de SQL Server 2005|Tipo SQL Server 2008 (o posterior)|Conversión del resultado (servidor a cliente)|Conversión de parámetros (cliente a servidor)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|Fecha y hora|Date|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de hora se establecen en cero.|Si el campo de hora es distinto de cero, se producirá un error de IRowsetChange debido al truncamiento de cadenas.|  
|DBTYPE_DBTIME||Time(0)|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de fecha se establecen en la fecha actual.|Si las fracciones de segundo son distintos de cero, se producirá un error de IRowsetChange debido al truncamiento de cadenas.<br /><br /> Se omite la fecha.|  
|DBTYPE_DBTIME||Time(7)|Se produce un error: literal de hora no válido.|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Se produce un error: literal de hora no válido.|Aceptar|  
|DBTYPE_DBTIMESTAMP||Datetime2(3)|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP||Datetime2(7)|Aceptar|Aceptar|  
|DBTYPE_DBDATE|Smalldatetime|Date|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de hora se establecen en cero.|Si el campo de hora es distinto de cero, se producirá un error de IRowsetChange debido al truncamiento de cadenas.|  
|DBTYPE_DBTIME||Time(0)|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de fecha se establecen en la fecha actual.|Si las fracciones de segundo son distintos de cero, se producirá un error de IRowsetChange debido al truncamiento de cadenas.<br /><br /> Se omite la fecha.|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|Aceptar|Aceptar|  
  
 OK significa que si ha funcionado con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], también debería funcionar con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posterior.  
  
 Solo se han considerado los siguientes cambios de esquema:  
  
-   Usar un nuevo tipo donde de forma lógica una aplicación requiere un único valor de fecha u hora. Sin embargo, la aplicación se obligaba a usar **datetime** o **smalldatetime** porque no estaban disponibles diferente tipos de fecha y hora.  
  
-   Usar un nuevo tipo para obtener más precisión o exactitud en fracciones de segundo.  
  
-   Cambiar a **datetime2** porque éste es el tipo de datos preferido para la fecha y hora.  
  
 Se producirá un error de las aplicaciones que usan los metadatos del servidor obtenidos a través de conjuntos de filas de esquema o ICommandWithParameters:: GetParameterInfo para establecer la información de tipo de parámetro a través de ICommandWithParameters:: SetParameterInfo durante las conversiones de cliente donde la cadena representación de un tipo de origen es mayor que la representación de cadena del tipo de destino. Por ejemplo, si un enlace del cliente usa DBTYPE_DBTIMESTAMP y la columna del servidor es la fecha, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client convertirá el valor a "aaaa-mm-dd fff", pero los metadatos del servidor se devolverán como **nvarchar (10)**. El desbordamiento resultante produce DBSTATUS_E_CATCONVERTVALUE. Surgen problemas similares con las conversiones de datos por IRowsetChange, porque los metadatos de conjunto de filas se establecen en los metadatos del conjunto de resultados.  
  
### <a name="parameter-and-rowset-metadata"></a>Parámetros y metadatos de conjuntos de filas  
 Esta sección describen los metadatos de parámetros, las columnas de resultados y conjuntos de filas de esquema para los clientes que se compilan con una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 La estructura DBPARAMINFO devuelve la siguiente información a través de la *prgParamInfo* parámetro:  
  
|Tipo de parámetro|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 Observe que algunos de estos intervalos de valores no son continuos; por ejemplo, en el intervalo 8,10..16 falta el 9. Esto se debe a la adición de un separador decimal cuando la precisión fraccionaria es mayor que cero.  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 Se devuelven las siguientes columnas:  
  
|Tipo de columna|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|date|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 La estructura DBCOLUMNINFO devuelve la siguiente información:  
  
|Tipo de parámetro|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>Conjuntos de filas de esquema  
 En esta sección se describen los metadatos para los parámetros, columnas de resultados y conjuntos de filas de esquema de los nuevos tipos de datos. Esta información es útil es que tenga un proveedor de cliente desarrollado con herramientas anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
#### <a name="columns-rowset"></a>Conjunto de filas COLUMNS  
 Para los tipos de fecha y hora se devuelven los siguientes valores de columna:  
  
|Tipo de columna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|date|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedureparameters-rowset"></a>Conjunto de filas PROCEDURE_PARAMETERS  
 Para los tipos de fecha y hora se devuelven los siguientes valores de columna:  
  
|Tipo de columna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|date|DBTYPE_WSTR|10|20|date|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|datetime|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="providertypes-rowset"></a>Conjunto de filas PROVIDER_TYPES  
 Para los tipos de fecha y hora se devuelven las siguientes filas:  
  
|Tipo -><br /><br /> Columna|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>Comportamiento de un servidor de nivel inferior  
 Cuando se conecta a un servidor de una versión anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], cualquier intento de usar los nuevos nombres de tipo de servidor (por ejemplo, con ICommandWithParameters:: SetParameterInfo o ITableDefinition:: CreateTable) dará como resultado en lugar a DB_E_BADTYPENAME.  
  
 Si los nuevos tipos se enlazan en parámetros o resultados sin usar un nombre de tipo y el nuevo tipo se usa para especificar implícitamente el tipo de servidor, o no hay ninguna conversión válida del tipo de servidor al tipo de cliente, se devuelve DB_E_ERRORSOCCURRED, y DBBINDSTATUS_UNSUPPORTED_CONVERSION se establece como estado de enlace para el descriptor de acceso que se usó en Execute.  
  
 Si hay una conversión de cliente compatible del tipo de búfer al tipo de servidor para la versión del servidor en la conexión, pueden usarse todos los tipos de búfer del cliente. En este contexto, *tipo de servidor* significa que el tipo especificado por ICommandWithParameters:: SetParameterInfo o implícito en el tipo de búfer si no se ha llamado ICommandWithParameters:: SetParameterInfo. Esto significa que DBTYPE_DBTIME2 y DBTYPE_DBTIMESTAMPOFFSET pueden usarse con servidores de nivel inferior, o cuando DataTypeCompatibility=80, si la conversión del cliente a un tipo de servidor compatible se realiza correctamente. Es evidente que si el tipo de servidor es incorrecto, el servidor todavía podría notificar un error si no puede realizar una conversión implícita al tipo de servidor real.  
  
## <a name="sspropinitdatatypecompatibility-behavior"></a>Comportamiento de SSPROP_INIT_DATATYPECOMPATIBILITY  
 Cuando SSPROP_INIT_DATATYPECOMPATIBILITY se establece en SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000, los tipos nuevos de fecha y hora y los metadatos asociados aparecen en los clientes tal y como aparecen para los clientes de nivel inferior, como se describe en [cambios de copia masiva Tipos de fecha y hora ha mejorado &#40;de OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
## <a name="comparability-for-irowsetfind"></a>Comparaciones en IRowsetFind  
 Se permiten todos los operadores de comparación para los nuevos tipos de fecha y hora, debido a que aparecen como tipos de cadena en lugar de tipos de fecha y hora.  
  
## <a name="see-also"></a>Vea también  
 [Fecha y hora mejoras & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  

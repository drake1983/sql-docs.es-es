---
title: SQLGetDescField | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetDescField function
ms.assetid: 3e59a37a-28ee-4c91-8968-7fe3b966739d
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 33504794f4f79db4e5f59aea6746753351be3d60
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdescfield"></a>SQLGetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client expone campos descriptores específicos del controlador para la fila descriptor de implementación (IRD) únicamente. En IRD, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] campos de descriptor hace referencia a través de atributos de columna específicos del controlador. Para obtener información acerca de cómo obtener una lista completa de campos descriptores específicos del controlador disponibles, consulte [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md).  
  
 Los campos de descriptor que contienen cadenas de identificador de columna son a menudo cadenas de longitud cero. Todos los valores de campos de descriptor específicos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son de solo lectura.  
  
 Al igual que los atributos se recuperan con SQLColAttribute, campos de descriptor que se notifican los atributos de nivel de fila de informe (como SQL_CA_SS_COMPUTE_ID) para todas las columnas del conjunto de resultados.  
  
## <a name="sqlgetdescfield-and-table-valued-parameters"></a>SQLGetDescField y parámetros con valores de tabla  
 SQLGetDescField puede utilizarse para obtener valores de atributos extendidos de parámetros con valores de tabla y las columnas de parámetros con valores de tabla. Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgetdescfield-support-for-enhanced-date-and-time-features"></a>SQLGetDescField admite las características mejoradas de fecha y hora  
 Para obtener información acerca de los campos de descriptor disponibles con los tipos de fecha y hora nueva, vea [parámetros y metadatos de resultados](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obtener más información, consulte [fecha y hora mejoras & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
 A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede devolver SQLGetDescField **SQL_C_SS_TIME2** (para **tiempo** tipos) o **SQL_C_SS_TIMESTAMPOFFSET** (para  **DateTimeOffset**) en lugar de **SQL_C_BINARY**, si su aplicación utiliza ODBC 3.8.  
  
## <a name="sqlgetdescfield-support-for-large-clr-udts"></a>SQLGetDescField admite UDT CLR grandes  
 **SQLGetDescField** admite los tipos definidos por el usuario CLR grandes (UDT). Para obtener más información, consulte [Large CLR User-Defined tipos & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlgetdescfield-support-for-sparse-columns"></a>SQLGetDescField admite columnas dispersas  
 SQLGetDescField puede utilizarse para consultar el nuevo campo IRD sql_ca_ss_is_column_set y determinar si una columna es una **column_set** columna.  
  
 Para obtener más información, consulte [Sparse Columns Support &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="example"></a>Ejemplo  
  
```  
typedef struct tagCOMPUTEBYLIST  
    {  
    SQLSMALLINT nBys;  
    SQLSMALLINT aByList[1];  
    } COMPUTEBYLIST;  
typedef COMPUTEBYLIST* PCOMPUTEBYLIST;   
  
SQLHDESC    hIRD;   
SQLINTEGER  cbIRD;   
SQLINTEGER  nSet = 0;   
  
// . . .  
// Execute a statement that contains a COMPUTE clause,  
//  then get the descriptor handle of the IRD and  
//  get some IRD values.  
  
SQLGetStmtAttr(g_hStmt, SQL_ATTR_IMP_ROW_DESC,  
    (SQLPOINTER) &hIRD, sizeof(SQLHDESC), &cbIRD);  
  
// For statement-wide column attributes, any  
//  descriptor record will do. You know that 1 exists,  
//  so use it.  
SQLGetDescField(hIRD, 1, SQL_CA_SS_NUM_COMPUTES,  
    (SQLPOINTER) &nComputes, SQL_IS_INTEGER, &cbIRD);  
  
if (nSet == 0)  
    {  
    SQLINTEGER      nOrderID;  
  
    printf_s("Normal result set.\n");  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ORDER,  
            (SQLPOINTER) &nOrderID, SQL_IS_INTEGER,  
            &cbIRD);  
  
        if (nOrderID != 0)  
            {  
            printf_s("Col in ORDER BY, pos: %ld",  
                nOrderID);  
            }  
            printf_s("\n");  
        }  
  
    printf_s("\n");  
    }  
else  
    {  
    PCOMPUTEBYLIST  pByList;  
    SQLSMALLINT     nBy;  
    SQLINTEGER      nColID;  
  
    printf_s("Computed result set number: %lu\n",  
        nSet);  
  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_BYLIST,  
        (SQLPOINTER) &pByList, SQL_IS_INTEGER,  
        &cbIRD);  
  
    if (pByList != NULL)  
        {  
        printf_s("Clause ordered by columns: ");  
        for (nBy = 0; nBy < pByList->nBys; )  
            {  
            printf_s("%u", pByList->aByList[nBy]);  
            nBy++;  
  
            if (nBy == pByList->nBys)  
                {  
                printf_s("\n");  
                }  
            else  
                {  
                printf_s(", ");  
                }  
            }  
        }  
    else  
        {  
        printf_s("Compute clause set not ordered.\n");  
        }  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ID, (SQLPOINTER) &nColID,  
            SQL_IS_INTEGER, &cbIRD);  
        printf_s("ColumnID: %lu, nColID);  
        }  
    printf_s("\n");  
    }  
  
if (SQLMoreResults(g_hStmt) == SQL_SUCCESS)  
    {  
    // Determine the result set indicator.  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_ID,  
        (SQLPOINTER) &nSet, SQL_IS_INTEGER, &cbIRD);  
    }  
```  
  
## <a name="see-also"></a>Vea también  
 [Sqlgetdescfield, función](http://go.microsoft.com/fwlink/?LinkId=59351)   
 [Detalles de implementación de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  

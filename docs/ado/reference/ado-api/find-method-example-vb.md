---
title: Buscar el ejemplo del método (VB) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Find method [ADO], Visual Basic example
ms.assetid: bbf27dcc-9815-4e2f-8ea8-b8c9fe6dedd6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e909b0786e4d7f91ff20c77530c6c1d14fd421b8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="find-method-example-vb"></a>Ejemplo (VB) del método Find
Este ejemplo se utiliza la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) del objeto [buscar](../../../ado/reference/ado-api/find-method-ado.md) método para localizar y contar el número de títulos de empresa en el ***Pubs*** base de datos. En el ejemplo se da por supuesto que el proveedor subyacente no admite una funcionalidad similar.  
  
```  
'BeginFindVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection and recordset variables  
    Dim Cnxn As New ADODB.Connection  
    Dim rstTitles As New ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
     ' record variables  
    Dim mark As Variant  
    Dim count As Integer  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open recordset with default parameters which are  
    ' sufficient to search forward through a Recordset  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "SELECT title_id FROM titles"  
    rstTitles.Open strSQLTitles, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    count = 0  
    rstTitles.Find "title_id LIKE 'BU%'"  
  
    Do While Not rstTitles.EOF  
        'continue if last find succeeded  
        Debug.Print "Title ID: "; rstTitles!title_id  
        'count the last title found  
        count = count + 1  
        ' note current position  
        mark = rstTitles.Bookmark  
        rstTitles.Find "title_id LIKE 'BU%'", 1, adSearchForward, mark  
        ' above code skips current record to avoid finding the same row repeatedly;  
        ' last arg (bookmark) is redundant because Find searches from current position  
    Loop  
  
    Debug.Print "The number of business titles is " & count  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndFindVB  
```  
  
## <a name="see-also"></a>Vea también  
 [Find (método) (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

---
title: Generación de informes (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Generating reports
ms.assetid: 1c0202e8-546d-4cb3-a37f-1d2e35d53839
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: aaa0b1d90463f1e6b85a3423c13e4f785621c817
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="generating-reports-mysqltosql"></a>Generación de informes (MySQLToSQL)
Se generan los informes de ciertas actividades que se realizan mediante comandos en la consola SSMA al nivel de árbol de objetos.  
  
Utilice el procedimiento siguiente para generar informes:  
  
1.  Especifique el **escritura-resumen-informe de** parámetro. El informe al respecto se almacena como el nombre de archivo (si se especifica) o en la carpeta especifique. El nombre de archivo es definido por el sistema como se mencionó en la tabla siguiente where, **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
    Los comandos de à respecto de los informes son:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Command**|**Título del informe**|  
    |1|informe de evaluación generar|AssessmentReport&lt;n&gt;. XML|  
    |2|convertir esquema|SchemaConversionReport&lt;n&gt;. XML|  
    |3|migrar datos|DataMigrationReport&lt;n&gt;. XML|  
    |4|instrucción de sql Convert|ConvertSQLReport&lt;n&gt;. XML|  
    |5|destino sincronizar|TargetSynchronizationReport&lt;n&gt;. XML|  
    |6|actualización de base de datos|SourceDBRefreshReport&lt;n&gt;. XML|  
  
    > [!IMPORTANT]  
    > Un informe de salida es distinto de los informes de evaluación. El primero es un informe sobre el rendimiento de un comando ejecutado al, el segundo es un informe XML para su uso mediante programación.  
  
    Para las opciones de comando para los informes de salida (de Sl. No. 2 a 4 anteriores), consulte el [ejecutando la consola SSMA &#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) sección.  
  
2.  Indica el grado de detalle que desee en el informe de salida con la configuración de nivel de detalle del informe:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Parámetros y comandos**|**Descripción de salida**|  
    |1|detallado = "false"|Genera un informe resumido de la actividad.|  
    |2|detallado = "true"|Genera un informe de estado resumida y detallada para cada actividad.|  
  
    > [!NOTE]  
    > La configuración de nivel de detalle del informe especificada anteriormente son aplicable para informe de evaluación generar, convert-schema, migrar datos, comandos de la instrucción de sql de convert.  
  
3.  Indica el grado de detalle que desee en los informes de errores mediante la configuración de informe de errores:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Parámetros y comandos**|**Descripción de salida**|  
    |1|informe de errores = "false"|No hay detalles de error / advertencia / mensajes de información.|  
    |2|informe de errores = "true"|Error detallado / advertencia / mensajes de información.|  
  
    > [!NOTE]  
    > La configuración de informe de errores especificados anteriormente son aplicable para informe de evaluación generar, convert-schema, migrar datos, comandos de la instrucción de sql de convert.  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"  
  
/>  
```  
  
### <a name="synchronize-target"></a>destino sincronizar:  
El comando **destino sincronizar** tiene **informe de errores a** parámetro, que especifica la ubicación del informe de error para la operación de sincronización. A continuación, un archivo con nombre **TargetSynchronizationReport&lt;n&gt;. XML** se crea en la ubicación especificada, donde **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
**Nota:** si se proporciona la ruta de acceso de carpeta, el parámetro 'informe-errores-to' se convierte en un atributo opcional para el comando 'sincronizar el destino'.  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**nombre de objeto:** especifica los objetos que se consideran para la sincronización (también puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
**error:** especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles en el error:  
  
-   total de informes como advertencia  
  
-   informes-each-como-advertencia  
  
-   Error-script  
  
### <a name="refresh-from-database"></a>actualización-de-base de datos:  
El comando **actualización de base de datos** tiene **informe de errores a** parámetro, que especifica la ubicación del informe de error para la operación de actualización. A continuación, un archivo con nombre **SourceDBRefreshReport&lt;n&gt;. XML** se crea en la ubicación especificada, donde **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
**Nota:** si se proporciona la ruta de acceso de carpeta, el parámetro 'informe-errores-to' se convierte en un atributo opcional para el comando 'sincronizar el destino'.  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**nombre de objeto:** especifica los objetos que se consideran para la actualización (también puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
**error:** especifica si se debe especificar la actualización de errores como advertencias o errores. Opciones disponibles en el error:  
  
-   total de informes como advertencia  
  
-   informes-each-como-advertencia  
  
-   Error-script  
  
## <a name="see-also"></a>Vea también  
[Ejecutar la consola SSMA (MySQL)](http://msdn.microsoft.com/en-us/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  

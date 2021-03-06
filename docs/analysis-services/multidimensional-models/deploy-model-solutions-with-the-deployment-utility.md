---
title: Implementar soluciones de modelos con la utilidad de implementación | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 76d1a3e3cfff777f610bb00f52644af3903ac615
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="deploy-model-solutions-with-the-deployment-utility"></a>Implementar soluciones de modelos con la utilidad de implementación
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  La utilidad **Microsoft.AnalysisServices.Deployment** permite iniciar el motor de implementación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] desde el símbolo del sistema. Como archivo de entrada, la utilidad utiliza archivos de salida XML creados al construir un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Los archivos de entrada se pueden modificar fácilmente para personalizar la implementación de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El script de implementación generado puede ejecutarse inmediatamente o guardarse para su implementación posterior.  
  
> [!NOTE]
> El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente/utilidad de implementación se instala con [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS). Asegúrese de que está utilizando la versión más reciente. De forma predeterminada, la versión más reciente del Asistente para la implementación se instala en C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio. 

## <a name="syntax"></a>Sintaxis  
  
```  
  
Microsoft.AnalysisServices.Deployment [ASdatabasefile]   
    {[/s[:logfile]] | [/a] | [[/o[:output_script_file]] [/d]]}  
```  
  
##  <a name="Arguments"></a> Argumentos  
 *ASdatabasefile*  
 Ruta de acceso completa de la carpeta en la que se encuentra el archivo de script de implementación (.asdatabase) de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Este archivo se genera al implementar un proyecto en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Se encuentra en la carpeta bin del proyecto. El archivo .asdatabase contiene la ubicación de las definiciones de objetos que se implementarán. Si no se especifica, se usa la carpeta actual.  
  
 **/s**  
 Ejecuta la utilidad en modo silencioso y no muestra cuadros de diálogo. Para obtener más información sobre los modos, vea la sección [Modos](#Modes), más adelante en este tema.  
  
 *archivoDeRegistro*  
 Ruta completa y nombre del archivo de registro. Los eventos de seguimiento se registrarán en el archivo de registro especificado. Si el archivo de registro ya existe, se reemplazará el contenido del archivo.  
  
 **/a**  
 Ejecuta la utilidad en modo de respuesta. Todas las respuestas realizadas durante la parte del asistente de la utilidad deben volver a escribirse en los archivos de entrada, pero en realidad no se realizará ningún cambio en los destinos de la implementación.  
  
 **/o**  
 Ejecuta la utilidad en modo de salida. No se producirá la implementación, pero el script XML for Analysis (XMLA) que normalmente se enviaría a los destinos de implementación se guarda en el archivo de script de salida especificado. Si no se especifica *output_script_file* , la utilidad intenta usar el archivo de script de salida especificado en el archivo de entrada de opciones de implementación (.deploymentoptions). Si no se especifica un archivo de script de salida en el archivo de entrada de opciones de implementación, se produce un error.  
  
 Para obtener más información sobre los modos, vea la sección [Modos](#Modes), más adelante en este tema.  
  
 *output_script_file*  
 Ruta de acceso completa y nombre del archivo de script de salida.  
  
 **/d**  
 Si se usa el argumento **/o** , especifica que la utilidad no debe conectarse con la instancia de destino. Como no se realiza ninguna conexión con los destinos de implementación, el script de salida se genera basándose solamente en la información recuperada de los archivos de entrada.  
  
> [!NOTE]  
>  El argumento **/d** se usa solamente en modo de salida. Este argumento se omite si se especifica en modo silencioso o de respuesta. Para obtener más información sobre los modos, vea la sección [Modos](#Modes), más adelante en este tema.  
  
## <a name="remarks"></a>Comentarios  
 La utilidad **Microsoft.AnalysisServices.Deployment** toma un conjunto de archivos que proporcionan definiciones de objetos, destinos de implementación y parámetros de configuración, e intenta implementar las definiciones de objetos en los destinos de implementación especificados mediante les opciones de implementación y los parámetros de configuración que se han indicado. Esta utilidad puede proporcionar una interfaz de usuario cuando se invoca en el modo de salida o en el archivo de salida. Para obtener más información sobre cómo usar la interfaz de usuario proporcionada por esta utilidad para crear archivos de respuesta, vea [Implementar soluciones de modelos con la utilidad de implementación](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md).  
  
 La utilidad se encuentra en la carpeta de \Microsoft SQL Server\140\Binn\ManagementStudio de archivos (x86) \Program.  
  
##  <a name="Modes"></a> Modos  
 La utilidad se puede ejecutar en los modos que se enumeran en la siguiente tabla.  
  
|Modo|Description|  
|----------|-----------------|  
|Modo silencioso|No se muestra ninguna interfaz de usuario y toda la información necesaria para la implementación la proporcionan los archivos de entrada. La utilidad no muestra el progreso en el modo silencioso. En su lugar, se puede usar un archivo de registro opcional para capturar el progreso y la información de errores para su posterior revisión.|  
|Modo de respuesta|Se muestra la interfaz de usuario del Asistente para la implementación y las respuestas del usuario se guardan en los archivos de entrada especificados para la posterior implementación. La implementación no se produce en el modo de respuesta. El único propósito del modo de respuesta es capturar las respuestas del usuario|  
|Modo de salida|No se muestra ninguna interfaz de usuario y toda la información necesaria para la implementación la proporcionan los archivos de entrada.<br /><br /> Sin embargo, a diferencia del modo silencioso, la salida de la utilidad se escribe en un archivo de script de salida, no se envía a los destinos de implementación indicados en los archivos de entrada. A menos que especifique el argumento **/d** , la utilidad conecta con cada destino de implementación para comparar los metadatos mientras genera el archivo de script de salida.|  
  
 [Volver a Argumentos](#Arguments)  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra cómo implementar un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo silencioso y registrar los mensajes de progreso y de error para una posterior revisión:  
  
 `Microsoft.AnalysisServices.Deployment.exe`  
  
 `<drive>:\My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin`  
  
 `/s: C:\ My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin\deployment.log`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la utilidad del símbolo del sistema &#40;motor de base de datos&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  

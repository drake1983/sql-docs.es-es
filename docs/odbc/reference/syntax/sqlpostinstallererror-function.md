---
title: Función SQLPostInstallerError | Documentos de Microsoft
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
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b34cef9e116bd75b5394cfe86e5f8784f0ff152
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0  
  
 **Resumen**  
 **SQLPostInstallerError** proporciona un mecanismo para una biblioteca del programa de instalación de controlador o traductor para informar de errores para el **ConfigDriver**, **ConfigDSN**, y **ConfigTranslator**  funciones a la cola de error del instalador. Las aplicaciones no usan esta API; usan **SQLInstallerError** para recuperar el error.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>Argumentos  
 *fErrorCode*  
 [Entrada] Código de error del instalador.  
  
 *szErrorMsg*  
 [Entrada] Texto del mensaje de error.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLPostInstallerError** no publica valores de error para sí mismo. Si el error se ha registrado correctamente a la cola de errores de instalador (usando recuperables **SQLInstallerError**), se devuelve SQL_SUCCESS. Se devolverá SQL_ERROR si el valor de la *dwErrorCode* argumento no es uno de los códigos de error del instalador especificado.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|Agregar, modificar o quitar orígenes de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Establecer una opción de traducción|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|

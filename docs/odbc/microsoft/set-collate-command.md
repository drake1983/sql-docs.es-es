---
title: Comando COLLATE | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1ce3b75134da55286f40dc77cf6f6ba7de7e5b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="set-collate-command"></a>Comando COLLATE Set.
Especifica una secuencia de intercalación para los campos de carácter en posteriores indización y operaciones de ordenación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>Argumentos  
 *cSequenceName*  
 Especifica una secuencia de intercalación. Las opciones de secuencia de intercalación disponibles se describen en la tabla siguiente.  
  
|Opciones|Lenguaje|  
|-------------|--------------|  
|HOLANDÉS|Neerlandés|  
|GENERAL|Inglés, francés, alemán, español moderno, portugués y otros idiomas de Europa occidental|  
|ALEMÁN|Orden de alemán libreta de teléfonos (DIN)|  
|ISLANDIA|Islandés|  
|MÁQUINA|Máquina (la secuencia de intercalación predeterminada para las versiones anteriores de FoxPro)|  
|NORDAN|Noruego, danés|  
|ESPAÑOL|Español tradicional|  
|SWEFIN|Sueco, finlandés|  
|UNIQWT|Peso único|  
  
> [!NOTE]  
>  Cuando se especifica la opción español, *ch* es una letra única que ordena entre *c* y *d.*, y *ll* ordena entre  *l* y *m*.  
  
 Si especifica una opción de secuencia de intercalación como una cadena de caracteres literales, asegúrese de incluir la opción entre comillas:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MÁQUINA es la opción de secuencia de intercalación predeterminada y es que están familiarizados con los usuarios de Xbase de secuencia. Caracteres se ordenan como aparecen en la página de códigos actual.  
  
 GENERAL puede ser preferible para los usuarios de Estados Unidos y Europa occidental. Caracteres se ordenan como aparecen en la página de códigos actual. En versiones de FoxPro anteriores a la 2.5, índices podrían haberse creados mediante el **superior**() o **inferior**funciones () para convertir campos de caracteres en un caso coherente. En versiones de FoxPro posteriores a la 2.5, en su lugar, puede especificar la opción de secuencia de intercalación GENERAL y omitir el **superior**conversión ().  
  
 Si especifica una opción de secuencia de intercalación distinta de la máquina y si se crea un archivo .idx, siempre se crea un .idx compact.  
  
 Utilice SET("COLLATE") para devolver la secuencia de intercalación actual.  
  
 Puede especificar una secuencia de intercalación para un origen de datos mediante la [cuadro de diálogo de configuración de Visual FoxPro de ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) o mediante la palabra clave Collate en la cadena de conexión con [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md). Esto es idéntico al emitir el comando siguiente:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Comentarios  
 ESTABLECER COLLATE permite a las tablas de orden que contiene los caracteres acentuados de cualquiera de los idiomas admitidos. Cambiar la configuración de establecer COLLATE no afecta a la secuencia de intercalación de índices abiertos anteriormente. Visual FoxPro mantiene automáticamente los índices existentes, lo que ofrece la flexibilidad para crear muchos tipos diferentes de índices, incluso para el mismo campo.  
  
 Por ejemplo, si se crea un índice con establecer COLLATE establecido en GENERAL y posteriormente se cambia la configuración de establecer COLLATE en español, el índice conserva la secuencia de intercalación GENERAL.  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo de configuración de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)

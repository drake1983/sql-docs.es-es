---
title: CustomData (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5161bb180b6acdf8f6ab6d16d6d0f15bd8f40a39
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577817"
---
# <a name="customdata-mdx"></a>CustomData (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el valor de la **CustomData** propiedad de cadena de conexión si está definida; en caso contrario, **null**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 El **CustomData** función puede recuperar la **CustomData** propiedad de cadena de conexión y pasar de una configuración que va a usar funciones de expresiones multidimensionales (MDX) e instrucciones, como [UserName (MDX)](../mdx/username-mdx.md) y [llamar (instrucción, MDX)](../mdx/mdx-data-manipulation-call.md). Por ejemplo, esta función puede utilizarse en una expresión de la seguridad dinámica para seleccionar los miembros del conjunto permitidos o denegados para el valor de cadena en el **CustomData** propiedad cadena de conexión.  
  
## <a name="example"></a>Ejemplo  
 La consulta siguiente muestra el valor devuelto por la **CustomData** función en una medida calculada:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

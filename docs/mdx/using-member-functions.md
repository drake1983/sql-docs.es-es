---
title: Mediante las funciones miembro | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 59be2bef7e2a3fb57b720672c3c89d0500feef8b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581557"
---
# <a name="using-member-functions"></a>Usar funciones de miembro
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Una función miembro es una función MDX (Expresiones multidimensionales) que devuelve un miembro. Las funciones de  miembro, al igual que las funciones de tupla y de conjunto, son esenciales para negociar las estructuras multidimensionales de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 De las muchas funciones de miembro en MDX, el más importante es la **CurrentMember** función, que se usa para determinar el miembro actual en una jerarquía. La consulta siguiente muestra cómo se usa, junto con el **primario**, **antecesor**, y **Prevmember** funciones:  
  
 `WITH`  
  
 `//Returns the name of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[CurrentMemberDemo] AS [Date].[Calendar].CurrentMember.Name`  
  
 `//Returns the name of the parent of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[ParentDemo] AS [Date].[Calendar].CurrentMember.Parent.Name`  
  
 `//Returns the name of the ancestor of the currentmember on the Calendar hierarchy at the Year level`  
  
 `MEMBER MEASURES.[AncestorDemo] AS ANCESTOR([Date].[Calendar].CurrentMember, [Date].[Calendar].[Calendar Year]).Name`  
  
 `//Returns the name of the member before the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[PrevMemberDemo] AS [Date].[Calendar].CurrentMember.Prevmember.Name`  
  
 `SELECT{MEASURES.[CurrentMemberDemo],MEASURES.[ParentDemo],MEASURES.[AncestorDemo],MEASURES.[PrevMemberDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;sintaxis MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Usar funciones de tupla](../mdx/using-tuple-functions.md)   
 [Uso de funciones de conjuntos](../mdx/using-set-functions.md)  
  
  

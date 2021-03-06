---
title: Elemento return (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e8746fb9f8b397ef50b1a5c66a2132e5f0cf5c87
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576197"
---
# <a name="return-element-xmla"></a>Elemento return (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene la información devuelta por un [DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md) elemento en respuesta a un [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) llamada al método o una [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md) elemento en respuesta a una [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DiscoverResponse> <!-- or ExecuteResponse -->  
   <return>  
      <root>...</root>  
      <!-- or -->  
      <results>...</results> <!-- ExecuteResponse only -->  
   </return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md), [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|  
|Elementos secundarios|Vea la tabla siguiente.|  
  
|Ancestor|Elementos secundarios|  
|--------------|--------------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[Raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) o [resultados](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El **devolver** elemento contiene los datos devueltos por la **Discover** y **Execute** métodos. Normalmente, el **devolver** elemento contiene un único **raíz** elemento que contiene los datos devueltos por una correcta **Discover** o **Execute** llamada al método o un XML de excepción de Analysis (XMLA) devuelta por una llamada de método incorrecto. Si el **Execute** método contiene un **lote** comando que realiza varias operaciones, el **devolver** elemento contiene un **resultados** elemento que, a su vez, contiene un **raíz** elemento para cada comando ejecutado correcta o incorrectamente por el **lote** comando.  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

---
title: DateCreated (propiedad, ADOX) | Documentos de Microsoft
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
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2b1848170421fec72fd6b0e502c015fa5be48f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="datecreated-property-adox"></a>DateCreated (propiedad, ADOX)
Indica la fecha en que se creó el objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **Variant** valor que especifica la fecha de creación. El valor es null si **DateCreated** no es compatible con el proveedor.  
  
## <a name="remarks"></a>Comentarios  
 El **DateCreated** propiedad es null para objetos recién anexados. Después de anexar una nueva [vista](../../../ado/reference/adox-api/view-object-adox.md) o [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md), debe llamar a la [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método de la [vistas](../../../ado/reference/adox-api/views-collection-adox.md) o [procedimientos ](../../../ado/reference/adox-api/procedures-collection-adox.md) colección para obtener los valores de la **DateCreated** propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo DateCreated y DateModified propiedades (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified (propiedad, ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)

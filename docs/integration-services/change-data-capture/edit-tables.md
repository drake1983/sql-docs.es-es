---
title: Editar tablas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 190858cabf05b04f58e73c3d7b7260a2669b897b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="edit-tables"></a>Editar tablas
  Use la pestaña **Tablas** para realizar cambios en las tablas y columnas que seleccionó en la base de datos de origen de Oracle. Esta pestaña contiene los elementos siguientes:  
  
 **Lista de la tabla**  
 La lista de tablas tiene tres columnas:  
  
-   **Nombre de tabla de Oracle**: nombre de la tabla, incluido el esquema de tabla.  
  
-   **Instancia de captura**: nombre de la instancia de captura que se usa para denominar los objetos de captura de datos modificados específicos de una instancia. La instancia de captura no puede ser NULL. Si no se especifica, el nombre deriva del nombre del esquema de origen más el nombre de la tabla de origen, con el formato `<schema-name>_<table-name>.` . El nombre de la instancia de captura no puede tener más de 100 caracteres y debe ser único dentro de la base de datos. Puede hacer clic en cualquier celda de esta columna para editar manualmente **capture_instance**.  
  
-   **Rol de seguridad**: nombre del rol de base de datos usado para obtener acceso a los datos de cambios. Puede hacer clic en cualquier celda de esta columna para editar manualmente **security_role**.  
  
 **Agregar tablas**  
 Haga clic en **Agregar tablas** para abrir el cuadro de diálogo Selección de tabla, donde puede [Agregar tablas a una instancia CDC](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md). La primera vez que tenga acceso a la base de datos de Oracle en esta sesión, debe [Connect to Oracle](../../integration-services/change-data-capture/connect-to-oracle.md).  
  
 **Editar**  
 Seleccione una tabla de la lista y haga clic en **Editar** para abrir el cuadro de diálogo **Propiedades** de la tabla, donde puede [Editar las propiedades de tabla](../../integration-services/change-data-capture/edit-the-table-properties.md).  
  
> [!NOTE]  
>  No puede editar la asignación de tipos para las tablas que ya tienen tablas reflejadas. Solo puede hacerlo para las tablas nuevas.  
  
 **Quitar**  
 Seleccione una tabla de la lista y haga clic en **Quitar** para quitar la tabla de la instancia CDC.  
  
## <a name="see-also"></a>Ver también  
 [Cómo editar las propiedades de la instancia CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Seleccione las columnas y tablas de Oracle ](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  

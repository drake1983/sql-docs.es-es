---
title: Elementos de informe personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: custom-report-items
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- extending Reporting Services
- Reporting Services, extending
- custom report items
ms.assetid: 64dcaf2c-1af5-4937-8ff7-98f1ec3b367e
caps.latest.revision: 22
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 618e0d126a1bfe86679eecc180d764f614b035c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="custom-report-items"></a>Elementos de informe personalizados
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona un abundante conjunto de herramientas para crear y publicar informes de empresa, administrar la seguridad y las suscripciones, y extender la funcionalidad de informes a través de una completa API. Los informes se definen utilizando un lenguaje basado en XML denominado lenguaje RDL (Report Definition Language). RDL proporciona un conjunto de instrucciones que describen el diseño, la información de las consultas y los tipos de elementos de un informe. Se puede extender RDL escribiendo un elemento de informe personalizado. El elemento de informe personalizado consta de un componente de tiempo de ejecución, que se denomina procesador de informes en tiempo de ejecución, y un componente de tiempo de diseño, que permite al elemento de informe personalizado estar disponible en el Diseñador de informes.  
  
 Para obtener un ejemplo de un elemento de informe personalizado totalmente implementado, vea [Ejemplos del producto SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="custom-report-item-scenarios"></a>Escenarios de elementos de informe personalizado  
 Los desarrolladores de software que necesitan integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en sus aplicaciones pueden requerir alguna funcionalidad que no se admita de forma nativa en RDL. Esto puede incluir elementos como controles de mapas, listas horizontales, listas de columnas y matrices dinámicas. Un componente de elemento de informe personalizado de tiempo de ejecución se puede desarrollar y distribuir con una aplicación para cubrir esta necesidad.  
  
 Además de proporcionar una funcionalidad que no se admita de forma nativa, algunos programadores pueden desear extender la funcionalidad existente con versiones alternativas de controles que ya están incluidos con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. En este escenario, un programador podría proporcionar tres componentes: un componente de tiempo de ejecución, un componente de tiempo de diseño y un componente de conversión de elementos de informe de tiempo de diseño que convierte un elemento de informe existente en un elemento de informe personalizado a petición.  
  
## <a name="in-this-section"></a>En esta sección  
 [Arquitectura de elementos de informe personalizados](../../reporting-services/custom-report-items/custom-report-item-architecture.md)  
 Describe los componentes que constituyen un elemento de informe personalizado.  
  
 [Requisitos de implementación de elementos de informe personalizados](../../reporting-services/custom-report-items/custom-report-item-implementation-requirements.md)  
 Describe los requisitos previos para crear un elemento de informe personalizado.  
  
 [Creación de un componente de tiempo de ejecución de elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)  
 Describe cómo crear un componente de tiempo de ejecución de elementos de informe personalizado.  
  
 [Creación de un componente de tiempo de diseño de elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
 Describe cómo crear un componente de tiempo de diseño de elementos de informe personalizado.  
  
 [Implementación de un elemento de informe personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
 Describe cómo implementar un elemento de informe personalizado.  
  
 [Bibliotecas de clases de elemento de informe personalizado](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
 Describe las clases de infraestructuras de los elementos de informe personalizados y las clases contenedoras administradas en el espacio de nombres **Microsoft.ReportDesigner**.  
  
## <a name="see-also"></a>Ver también  
 [Referencia técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  

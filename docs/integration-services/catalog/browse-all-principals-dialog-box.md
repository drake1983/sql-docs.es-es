---
title: Cuadro de diálogo Examinar todas las entidades de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: service
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 830bdc3728c23a420867ed5f5e53fcc4b69809f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="browse-all-principals-dialog-box"></a>Examinar todas las entidades (cuadro de diálogo)
  Use el cuadro de diálogo **Examinar todas las entidades** para seleccionar la entidad de seguridad de base de datos a la que desea cambiar los permisos en el proyecto seleccionado o en todos los proyectos incluidos en una carpeta seleccionada.  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el cuadro de diálogo Examinar todas las entidades](#open_dialog)  
  
-   [Configurar las opciones](#options)  
  
##  <a name="open_dialog"></a> Abrir el cuadro de diálogo Examinar todas las entidades  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese al servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Se conectará a la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda el catálogo SSISDB.  
  
2.  En el Explorador de objetos, expanda el árbol para que se muestre el nodo **Catálogos de Integration Services** .  
  
3.  Expanda el nodo **SSISDB** .  
  
4.  Para cambiar los permisos de la entidad de seguridad en todos los proyectos incluidos en una carpeta seleccionada, haga clic con el botón derecho en la carpeta y después haga clic en **Propiedades**.  
  
     Para cambiar los permisos de la entidad de seguridad en un proyecto seleccionado, expanda la carpeta que contiene el proyecto, haga clic con el botón derecho en él y después haga clic en **Propiedades**.  
  
5.  Seleccione la página **Permisos** y haga clic en **Examinar**.  
  
##  <a name="options"></a> Configurar las opciones  
 En esta página se muestran las entidades de seguridad de la vista de catálogo, sys.database_principals, de la base de datos de SSISDB.  
  
 Si selecciona las entidades de seguridad, se agregarán a la lista **Inicios de sesión o roles** de la página **Permisos** del cuadro de diálogo principal cuando haga clic en **Aceptar** y cierre el cuadro de diálogo **Examinar todas las entidades** . Después de agregar entidades de seguridad a la lista de **Inicios de sesión o roles** , puede cambiar sus permisos en el proyecto seleccionado.  
  
 **Columna de selección**  
 Seleccione esta opción para agregar la entidad de seguridad a la lista **Inicios de sesión o roles** de la página **Permisos** del cuadro de diálogo principal.  
  
 **Columna de icono**  
 Icono que corresponde al **Tipo** de la entidad de seguridad.  
  
 **Nombre**  
 Nombre de la entidad de seguridad.  
  
 **Tipo**  
 Tipo de la entidad de seguridad. Los tipos comunes son:  
  
-   Usuario de SQL  
  
-   Usuario de Windows  
  
-   Rol de base de datos  
  
  

---
title: 'Paso 3: Prueba de concepto que se conecta a SQL con Ruby | Documentos de Microsoft'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: ruby
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5bf98585281b4b84869c385c848d9add459d57b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>Paso 3: Prueba de concepto que se conecta a SQL con Ruby

En este ejemplo debe considerarse una prueba de concepto solo.  El código de ejemplo se ha simplificado para mayor claridad y no representa necesariamente mejores prácticas recomendadas por Microsoft.  
  
## <a name="step-1--connect"></a>Paso 1: conectar  
  
El [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) función se utiliza para conectarse a la base de datos SQL.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>Paso 2: Ejecutar una consulta  
  
Copie y pegue el siguiente código en un archivo vacío. Llámelo test.rb. A continuación, ejecutar, escriba el comando siguiente desde el símbolo del sistema:  
  
    ruby test.rb  
  
En el ejemplo de código, el [TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds) función se utiliza para recuperar un conjunto de resultados de una consulta en base de datos de SQL. Esta función acepta una consulta y devuelve un conjunto de resultados. Se recorre en iteración el conjunto de resultados con la tecla [result.each hacer | fila |](https://github.com/rails-sqlserver/tiny_tds).  
  
``` ruby 
    require 'tiny_tds'    
    print 'test'       
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC")  
    results.each do |row|  
    puts row  
    end  
```  
  
## <a name="step-3--insert-a-row"></a>Paso 3: Insertar una fila  
  
En este ejemplo se muestra cómo ejecutar un [insertar](../../t-sql/statements/insert-transact-sql.md) instrucción de forma segura, pasar parámetros que protección la aplicación de [inyección de código SQL](../../relational-databases/tables/primary-and-foreign-key-constraints.md) valor.    
  
Para usar TinyTDS con Azure, se recomienda ejecutar varias `SET` instrucciones para cambiar la forma en que la sesión actual controla información específica. Se recomienda `SET` se proporcionan las instrucciones en el ejemplo de código. Por ejemplo, `SET ANSI_NULL_DFLT_ON` permitirá las nuevas columnas creadas para permitir valores null, incluso si no se indica explícitamente el estado de nulabilidad de la columna.  
  
Para alinear con Microsoft SQL Server [datetime](http://msdn.microsoft.com/library/ms187819.aspx) formato, utilice la [strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) función para convertir al formato de fecha y hora correspondiente.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SET ANSI_NULLS ON")  
    results = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")  
    results = client.execute("SET ANSI_NULL_DFLT_ON ON")  
    results = client.execute("SET IMPLICIT_TRANSACTIONS OFF")  
    results = client.execute("SET ANSI_PADDING ON")  
    results = client.execute("SET QUOTED_IDENTIFIER ON")  
    results = client.execute("SET ANSI_WARNINGS ON")  
    results = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")  
    require 'date'  
    t = Time.now  
    curr_date = t.strftime("%Y-%m-%d %H:%M:%S.%L")  
    results = client.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate)  
    OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, '#{curr_date}' )")  
    results.each do |row|  
    puts row  
    end  
```

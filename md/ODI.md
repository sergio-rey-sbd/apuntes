---
title: Apache NiFi
description: Apache NiFi
permalink: /nifi/
---

<h1>Apache Nifi</h1>

<div align="center">
    <img src="../img/LogoNiFi.jpeg" alt="Logo Apache NiFi" width="15%" />
</div>

<h3>Tabla de contenidos</h3>

# Introducción a `Oracle Data Integrator`. `ODI`

La base es que todo lo guarda en repositorios.


# Demo de uso con `ODI`

Los puntos 2 y 3 hacen una introducción de lo que se va a hacer.

El punto 4 y 5 ya tienen cómo se implementa un ETL en ODI.

## Maquina virtual

Hay un fichero que indica donde esta todo: `Information about this machine`. Aquí tenemos todo lo que esta instalado así como usuarios y contraseñas de cada unos de los elementos que hay en el sistema.

- `ODI 12c Getting Started Guide.pdf`, fichero donde esta la demo que nos explica paso a paso un ejemplo de utilización de ODI.
- `SQL Developer`, el IDE de acceso a la base de datos
  - Se debe probar. Al abrir el IDE, veremos que muestra todas las bases de datos
  - Le damos a crear nuevo conexión, utilizando la plantilla existente y le metemos como nombre y usuario: `ODI_DEMO`, así tenemos una conexión a la base de datos que solo tiene permisos sobre las tablas que a nosotros nos interesan.
  - Ahora tenemos una interfaz sobre la que vamos a trabajar

El propio ODI tiene por ejemplo un registro de errores que se guardar en la propia base de datos, por lo que es interesante poder visualizar y manipular los datos 
- `ODI studio`: Se entra con la password `welcome1`


# ODI Studio

Cuando le damos a entrar, tenemos el listado en el desplegable de las diferentes demos.

Si le damos al lápiz, podemos editar y podemos ver unos cuantos datos como por ejemplo que el usuario de la base de datos es `prod.odi_repo` y otros datos como . El usuario y el password de la conexión también se ve en el primer grupo de datos.

Cuando abrimos ODI, vemos una parte del entorno, en Window podemos ver el resto de ventanas ocultas, como por ejemplo en `security`, podemos también acceder a el `log`

- `Topología`: se divide en tres partes
  - Parte física, donde se definen todas las conexiones, por ejemplo en technologies->files, estan las ficheros de dónde estan las cosas
  - Parte lógica que corresponde con la física
  - Context: es el que relaciona la parte física con la lógica

En la parte superior de la ventana de Topología hay un botón con icono de fábrica donde podemos ver por ejemplo todas las tecnologías (de conexión a diferentes sistemas de datos) 


En la parte de `Projects` tenemos 
- Paquetes
- Mappings: tienen 


# Ejercicio de demo de `ODI 12c Getting Started Guide.pdf`

Aqui tenemos una demo guiada que nos explica cómo hacer un par de mappings y ponerlos en macha, en concreto los puntos a realizar en clase son los siguientes

## Ejercicio 4.1 

En la parte física. del elemento final le pone un `TRUCATE` a `true`, que al parecer lo que hace es que cada vez que vamos a ejecutar elimina todo lo que hay en el destino para rehacerlo de nuevo.
También el `FLOW_CONTROL` a `false`. Esto lo que hace es verificar las claves primarias y si esta a true, fallará.

Tal y como esta hecho en clase, no llegamos a crear el paquete, (LOAD_SALES_ADMINISTRATION), por lo que al ejecutar puede fallar, Así porque antes de ejecutar el TRG_CUSTOMER se tiene que ejecutar los TRG_COUNTRY, REGION y CITY, por eso en clase pasamos directamente al 6.2 para hacer un paquete añadiendo los mapping hasta TRG_CUSTOMER. Bueno en clase hace el CITY, COUNTRY y ya el CUSTOMER.

Una vez hecho esto, seleccionamos el paquete y le damos al *play* para ejecutar.

## Ejercicio 4.2

Aquí se hace el mapping TRG_SALES

## Ejercicio 6.2.2

Aquí se hace el package que ejecuta todo el ETL completo


## Entregable 1 

Es la continuación del supuesto para generar un mapping “AGR_VENTAS_PRODUCTOS” 

Lo único reseñable esta en el punto *2. Importar la nova taula al model de dades de ODI, a la carpeta “Sales Administration”.*

Sobre modelos -> Sales Administration, click con botón derecho y hacemos click en ***Reverse Engineer***. Aparece una nueva pestaña y en la parte superior izquierda le damos el botón de ***Revese-Engeneer*** y busca tablas nuevas en el esquema de oracle y con esto lo tenemos.

El resto ya es lo mismo de siempre.... 

En el punto 9 tenemos las modificaciones de la parte física del mapping:ç
- IKM : IKM Control Append (POST FLOW = False, TRUNCATE = TRUE). Esto es `FLOW CONTROL` y `TRUNCATE`



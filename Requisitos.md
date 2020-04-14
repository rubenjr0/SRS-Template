# Especificación de requisitos 
## Del proyecto Clean Up

Versión 0.1  
Generada por Rubén Jiménez
Clean Up  
13/04/2020

Índice
=================
* [Versiones](#versiones)
* 1 [Introducción](#1-introducción)
  * 1.1 [Objetivo del documento](#11-objetivo-del-documento)
  * 1.2 [Ámbito del proyecto](#12-ámbito-del-proyecto)
  * 1.3 [Definiciones, acrónimos y abreviaturas](#13-definiciones-acrónimos-y-abreviaturas)
  * 1.4 [Referencias](#14-referencias)
  * 1.5 [Resumen del documento](#15-resumen-del-documento)
* 2 [Vista general del producto](#2-vista-general-del-producto)
  * 2.1 [Perspectiva del producto](#21-perspectiva-del-producto)
  * 2.2 [Funciones del producto](#22-funciones-del-producto)
  * 2.3 [Restricciones del producto](#23-restricciones-del-producto)
  * 2.4 [Perfiles de usuario](#24-perfiles-de-usuario)
  * 2.5 [Suposiciones y dependencias](#25-suposiciones-y-dependencias)
* 3 [Interfaces externas](#3-interfaces-externas)
    * 3.1 [Interfaces con el Usuario](#31-interfaces-con-el-usuario)
    * 3.2 [Interfaces con el Hardware](#32-interfaces-con-el-hardware)
    * 3.3 [Interfaces con el Software](#33-interfaces-con-el-software)
* 4 [Requisitos](#4-requisitos)
  * 4.1 [Precedencia y prioridad](#41-precedencia-y-prioridad) 
  * 4.2 [Funcionales](#42-funcionales)
  * 4.3 [Calidad de Servicio](#43-calidad-de-servicio)
    * 4.3.1 [Rendimiento](#431-rendimiento)
    * 4.3.2 [Seguridad](#432-seguridad)
    * 4.3.3 [Fiabilidad](#433-fiabilidad)
    * 4.3.4 [Disponibilidad](#434-disponibilidad)
  * 4.4 [Normativas aplicables](#44-normativas-aplicables)
  * 4.5 [Diseño e implementación](#45-diseño-e-implementación)
    * 4.5.1 [Instalación](#451-instalación)
    * 4.5.2 [Distribución](#452-distribución)
    * 4.5.3 [Mantenimiento](#453-mantenimiento)
    * 4.5.4 [Reusabilidad](#454-reusabilidad)
    * 4.5.5 [Portabilidad](#455-portabilidad)
    * 4.5.6 [Coste](#456-coste)
    * 4.5.7 [Fecha de Entrega](#457-fecha-de-entrega)
* 5 [Verificación](#5-verificación)
* 6 [Apendices](#6-apendices) 
  
## Versiones
| Name | Date    | Reason For Changes  | Version   |
| ---- | ------- | ------------------- | --------- |
| Inicial | 13/04/2020 | Creación del documento | 0.1 |
|      |         |                     |           |
|      |         |                     |           |

## 1. Introducción
En este documento se discutiran los requisitos de la plataforma de Clean Up.

### 1.1 Objetivo del documento
El objetivo de este documento es que los requisitos y funcionalidad objetivo de la plataforma queden bien especificados.
El público objetivo de este documento es el cliente y los desarrolladores.

### 1.2 Ámbito del proyecto
El producto discutido en este documento es la plataforma Clean Up, version 0.1.
La plataforma permite a los usuarios crear tickets de incidencias en la via pública, para que posteriormente un agente revise dichos tickets y los cierre cuando la incidencia sea solucionada.
Esta plataforma ayuda a que que los ciudadanos colaboren en mantener el buen estado de la vía pública.
El software puede ser comercializado con un modelo de suscripción para las instituciones que lo implementen, mientras que los usuarios no deberan pagar por usar la plataforma.

### 1.3 Definiciones, acrónimos y abreviaturas
- Usuario: Ciudadano que usa la plataforma.
- Agente: Entidad que revisa, notifica al organo competente y cierra las incidencias.
- Clientes: Terminales que usan los usuarios y agentes para interactuar con el sistema.
- Plataforma: El sistema comprendido por servidor, base de datos y clientes.
- LOPD: Ley Orgánica de Protección de Datos.
- GDPR: General Data Protection Regulation.

### 1.5 Resumen del documento
Describa lo que contiene el resto del documento y cómo está organizado. Dependiendo del proyecto, algunas subsecciones de las secciones 2 y 3 serán eliminadas.

## 2. Vista general del producto

### 2.1 Perspectiva del producto
Se trata de una plataforma web nueva compuesta por un servidor que atenderá las peticiones de los usuarios y los agentes, una base de datos que almacenará toda la información necesaria para permitir el correcto funcionamiento de la plataforma, y los clientes que permitiran interactuar y recibir información del servidor.

### 2.2 Funciones del producto
Los usuarios crearan tickets de incidencias en la via pública. El usuario proporcionara detalles como imagenes que podra tomar con sus dispositivo móvile o subir desde el almacenamiento del dispositivo que este usando, además de una breve descripción de la incidencia y la ubicación de la misma.
Las incidencias también tendran un ID propio, además de registraran el ID del usuario que la creo, asi como la fecha y hora en la que se creo.
En caso de que el sistema detecte un posible duplicado por cercania geográfica avisara al usuario. Si el usuario confirma que la incidencia ha sido reportada con anterioridad, su ticket se anexara al principal como subticket.
Un usuario podra consultar en todo momento el estado de los tickets que ha creado.

Los agentes podrán revisar tickets creados por los usuarios y cerrarlos una vez la incidencia haya sido solucionada.
Los agentes dispondrán de un mapa donde podrán ver las incidencias reportadas según su ubicación.
Tras haberse solucionado la incidencia reportada, los agentes pueden cerrarla, y en caso de tener subtickets, estos se cerraran tambien.

### 2.3 Restricciones del producto
La plataforma solo funcionará con conexión a internet, aunque los agentes contaran con un cache para ver tickets offline.
Los tickets contaran con una descripción con un número fijo de caracteres y 3 imagenes.
La plataforma respetará tanto la LOPD como la GDPR, y por extensión la Cookie Law. Debido a esto, se informará al usuario que al usar la plataforma, está de acuerdo con el uso de cookies en su navegador y con que nuestro servicio almacene sus datos. Además, los usuarios menores de 14 años no podrán utilizar la plataforma.

### 2.4 Perfiles de usuario
Los usuarios serán ciudadanos interesados en el buen estado de la infraestructura pública de donde vivan.
Nuestros usuarios objetivo son especialmente jovenes (con una edad igual o superior a 14 años) y adultos, ya que tienen una mayor fácilidad para aprender a manejar nuevas herramientas tecnológicas.

### 2.5 Suposiciones y dependencias
El sistema dependerá de otros sistemas y librerias externos:
- [Firebase de Google](https://firebase.google.com/): Base de datos nosql, sistema de gestión de usuarios que por correo y/o cuenta de Google, almacenamiento de archivos.
- [Bulma](https://bulma.io/): Framework de CSS.
- [VueJS]()
- Servicio de geolocalizacion con una api de geolocalización (propia del navegador o externa).
- Servicio de mapas, bien OpenStreetMap o Google Maps.

### 3 Interfaces externas

#### 3.1 Interfaces con el usuario 
La página principal tanto para usuarios como para agentes solicitara la creación de una cuenta o el inicio de sesión.
Después, dependiendo del tipo de usuario (usuario o agente), se mostraran interfaces distintas.

La interfaz para los usuarios permitirá ver los tickets creados en el pasado por el usuario en cuestión o crear un ticket nuevo.
Al pulsar el botón de crear ticket se mostrará una página con el formulario con los campos necesarios para crear un ticket. Una vez creado el ticket se volverá a la lista de tickets.

La interfaz para los agentes mostrará un mapa con incidencias, así como estadísticas (número de tickets abiertos).
El agente podrá abrir un ticket de interes para inspeccionarlo, pudiendo ver las imagenes, descripción y subtickets del mismo, además de poder cerrarlo pulsando un botón.

Una característica importante es que el diseño estará optimizado para ser usado tanto en moviles como en ordenadores. Esto será gracias a un enfoque [Responsive Web Design](https://www.w3schools.com/html/html_responsive.asp) y [Mobile-First Design](https://www.initcoms.com/que-es-mobile-first-posicionamiento/).

#### 3.2 Interfaces con el Hardware
El sistema necesitará un servidor en el que ejecutar el backend, y los dispositivos de los usuarios y agentes (ordenadores o móviles).
En el caso de los dispositivos móviles, necesitarán disponer de GPS activo

#### 3.3 Interfaces con el Software
Describa las conexiones entre este producto y otros componentes de software específicos (nombre y versión), incluidas bases de datos, sistemas operativos, herramientas, bibliotecas y componentes comerciales integrados. Identifique los elementos de datos o mensajes que entran y salen del sistema y describa el propósito de cada uno. Describa los servicios necesarios y la naturaleza de las comunicaciones. Consulte los documentos que describen los protocolos detallados de la interfaz de programación de aplicaciones. Identifique los datos que se compartirán entre los componentes de software. Si el mecanismo de intercambio de datos debe implementarse de una manera específica (por ejemplo, memoria compartida, ficheros, en la nube, etc), especifique esto como una restricción de implementación.


## 4. Requisitos
Esta sección especifica los requisitos del producto a nivel de sistema y desglosa estos en diferentes categorías. El conjunto de requisitos se debe validar y estos deben ser:
* Vigentes: Los requisitos reflejan las necesidades actuales de los usuarios del sistema, estos han podido cambiar con el tiempo, por tanto se debe revisar que sigen estando vigentes.
* Consistentes: Los requisitos no deben tener conflicto entre ellos. De tenerlo se puede establecer prioridades (obligatorio, deseable o opcional sería una opción).
* Completos: El conjunto de los requisitos define todas las funciones y restricciones deseadas por los stakeholders.
* Viables: Los requisitos pueden ser implementados dentro del presupuesto y tiempo planeado.
* Verificables: Los requisitos pueden ser comprobables (verificables) mediante tests.

Para cada requisito se debería especificar, su ID, nombre del requisito, descripción del requisito, dependencias, prioridad y justificación de su espeficación (stakeholder, derivado de un caso de uso, una interfaz necesaria, etc). Un estilo formateado facilitará la lectura. Podéis usar el siguiente formato(dependiendo de la sección se añadiran más o menos almohadillas para ponerlo en su subsección correspondiente):

### ID - Nombre del requisito
Descripción
#### Dependencias 
#### Priodidad
#### Justificación

### 4.1 Precedencia y prioridad
Esta sección está compuesta por una tabla que resumirá todos los requisitos especificados en las secciones siguientes. Se debe detallar un ID único, un nombre de requisito, su descripción, la prioridad de ese requisitos (es algo **Fundamental** a desarrollar; es **Deseable** tenerlo para que el cliente esté satisfecho; o es algo **Opcional** que estaría bien desarrollar si el tiempo lo permite), su precedencia (requisitos que deberán ser implementados antes) y el tipo (funcional o no funcional).

Esta tabla se generará en paralelo a las secciones correspondientes, y se completará cuando todas las secciones estén terminadas. Os recomiendo hacerla en excel e importarla en https://www.tablesgenerator.com/markdown_tables para generar la tabla en formato Markdown. Meter retornos de carro para que no se alarge mucho la tabla y usad la opción *_line break as <br>_* para que esos retornos de carro sean efectivos al copiarlos.


| Id 	| Nombre 	| Descripción 	| Priodidad 	| Precedencia 	| Tipo 	|
|:--:	|:----------------------------:	|:----------------------------------------------------------------------------------------------------------------------------------------------------------------:	|:-------------------:	|:-----------:	|-----------	|
| R3 	| Datos de clientes 	| El sistema deberá registar los datos de los clientes<br>para su posterior tratamiento. Estos incluirán su <br>nombre, DNI, fecha de nacimiento, género y e-mail. 	| <br>Fundamental<br> 	|  	| Funcional 	|
| R4 	| Modificar datos <br>clientes 	| El sistema permitirá modificar el e-mail del cliente. 	| Fundamental 	| R3 	| Funcional 	|
|  	|  	|  	|  	|  	|  	|
	


### 4.2 Funcionales
Esta sección especifica los requisitos funcionales de sistema que el futuro software debe tener en su entorno. Se aconseja poner un enlace al documento de casos de uso generado por magic draw para que el lector tenga una vista general de las funcionalidades del producto a generar.



### 4.3 Calidad de Servicio
Esta sección establece requisitos no funcionales relacionados con la calidad que deben presentar las funcionales del software.
 
#### 4.3.1 Rendimiento
Si existen requisitos no funcionales de rendimiento para el producto en varias circunstancias, indíquelos aquí y explique sus razones, para ayudar a los desarrolladores a comprender la intención y tomar las decisiones de diseño adecuadas. Especifique las restricciones de tiempo. Haga tales requisitos tan específicos como sea posible. Es posible que deba indicar los requisitos de rendimiento para requisitos funcionales o características individuales.

#### 4.3.2 Seguridad
Especifique los requisitos no funcionales relacionados con los problemas de seguridad o privacidad relacionados con el uso del producto. 
* Protección de los datos utilizados o creados por el producto.
* Requisitos de autenticación de identidad de usuario. 
* Políticas o regulaciones externas que contengan problemas de seguridad que afecten al producto. 
* Certificaciones de seguridad o privacidad que deben cumplirse.

#### 4.3.3 Fiabilidad
Especifique los requisitos no funcionales necesarios para establecer la fiabilidad requerida del sistema de software al momento de la entrega.

#### 4.3.4 Disponibilidad
Especifique los requisitos no funcionales necesarios para garantizar un nivel de disponibilidad definido para todo el sistema, tiempo mínimo disponible por día, máximos de reinicios permitidos por tiempo, etc.

### 4.4 Normativas aplicables
Especifique los requisitos no funcionales derivados de las normas o regulaciones existentes, que incluyen:
* Formato de informe
* Nombre de datos
* Procedimientos contables
* Seguimiento de auditoría

### 4.5 Diseño e implementación

#### 4.5.1 Instalación
Restricciones para garantizar que el futuro software se ejecutará sin problemas en la plataforma de implementación de destino.

#### 4.5.2 Distribución
Restricciones en los componentes de software para adaptarse a la estructura distribuida geográficamente de la organización en la que se va a instalar el software, la distribución de datos a procesar o la distribución de dispositivos a controlar.

#### 4.5.3 Mantenimiento
Especifique los atributos del software que se relacionan con la facilidad de mantenimiento del software en sí. Estos pueden incluir requisitos para cierta modularidad, interfaces o limitación de complejidad. Los requisitos no se deben colocar aquí solo porque son buenas prácticas de diseño.

#### 4.5.4 Reusabilidad
Software externo que deberá usarse.

#### 4.5.5 Portabilidad
Especifique los atributos del software que se relacionan con la facilidad de portar el software a otras máquinas host y / o sistemas operativos.

#### 4.5.6 Coste
Especifique las limitaciones en el costo del producto de software.

#### 4.5.7 Fecha de entrega
Especifique, si tiene, fecha de entrega del producto.

## 5. Verificación
Esta sección proporciona los enfoques y métodos de verificación planeados para calificar el software. Se recomienda que los elementos de información para verificación se proporcionen de manera paralela con los elementos de requisitos en la Sección 4. El propósito del proceso de verificación es proporcionar evidencia objetiva de que un sistema o elemento del sistema cumple con los requisitos y características especificados.


## 6. Apendices
### Apéndice A: Ejemplos de este documento relleno
Incluir y referenciar en el documento tantos apéndices como sea necesario. Los siguientes, son ejemplo de este documento (con algunas modificaciones), relleno:

[Ejemplo relleno en inglés 1](https://arxiv.org/pdf/1005.0330.pdf)
[Ejemplo relleno en inglés 2](http://www.cse.chalmers.se/~feldt/courses/reqeng/examples/srs_example_2010_group2.pdf)

### Apéndice B: Generar PDF usando un fichero MD
Hay multitud de herramientas online y offline, por ejemplo: https://www.markdowntopdf.com/

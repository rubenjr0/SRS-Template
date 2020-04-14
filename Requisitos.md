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
    * 4.3.1 [Seguridad](#431-seguridad)
    * 4.3.2 [Fiabilidad](#433-fiabilidad)
  * 4.4 [Diseño e implementación](#44-diseño-e-implementación)
    * 4.4.1 [Reusabilidad](#441-reusabilidad)
    * 4.4.2 [Portabilidad](#442-portabilidad)
    * 4.4.3 [Fecha de Entrega](#443-fecha-de-entrega)
* 5 [Verificación](#5-verificación)
* 6 [Apendices](#6-apendices) 
  
## Versiones
| Name | Date    | Reason For Changes  | Version   |
| ---- | ------- | ------------------- | --------- |
| Inicial | 13/04/2020 | Creación del documento | 0.1 |
|      |         |                     |           |
|      |         |                     |           |

## 1. Introducción
En este documento se discutirán los requisitos de la plataforma de Clean Up.

### 1.1 Objetivo del documento
El objetivo de este documento es que los requisitos y funcionalidad objetivo de la plataforma queden bien especificados.
El público objetivo de este documento es el cliente y los desarrolladores.

### 1.2 Ámbito del proyecto
El producto discutido en este documento es la plataforma Clean Up, version 0.1.
La plataforma permite a los usuarios crear tickets de incidencias en la vía pública, para que posteriormente un agente revise dichos tickets y los cierre cuando la incidencia sea solucionada.
Esta plataforma ayuda a que que los ciudadanos colaboren en mantener el buen estado de la vía pública.
El software puede ser comercializado con un modelo de suscripción para las instituciones que lo implementen, mientras que los usuarios no deberán pagar por usar la plataforma.

### 1.3 Definiciones, acrónimos y abreviaturas
- Usuario: Ciudadano que usa la plataforma.
- Agente: Entidad que revisa, notifica al órgano competente y cierra las incidencias.
- Clientes: Terminales que usan los usuarios y agentes para interactuar con el sistema.
- Plataforma: El sistema comprendido por servidor, base de datos y clientes.
- LOPD: Ley Orgánica de Protección de Datos.
- GDPR: General Data Protection Regulation.

### 1.5 Resumen del documento
Describa lo que contiene el resto del documento y cómo está organizado. Dependiendo del proyecto, algunas subsecciones de las secciones 2 y 3 serán eliminadas.

## 2. Vista general del producto

### 2.1 Perspectiva del producto
Se trata de una plataforma web nueva compuesta por un servidor que atenderá las peticiones de los usuarios y los agentes, una base de datos que almacenará toda la información necesaria para permitir el correcto funcionamiento de la plataforma, y los clientes que permitirán interactuar y recibir información del servidor.

### 2.2 Funciones del producto
Los usuarios crearan tickets de incidencias en la via pública. El usuario proporcionara detalles como imágenes que podra tomar con sus dispositivos móviles o subir desde el almacenamiento del dispositivo que este usando, además de una breve descripción de la incidencia y la ubicación de la misma.
Las incidencias también tendrán un ID propio, además de registrarán el ID del usuario que la creo, así como la fecha y hora en la que se creó.
En caso de que el sistema detecte un posible duplicado por cercanía geográfica avisara al usuario. Si el usuario confirma que la incidencia ha sido reportada con anterioridad, su ticket se anexara al principal como subticket.
Un usuario podra consultar en todo momento el estado de los tickets que ha creado.

Los agentes podrán revisar tickets creados por los usuarios y cerrarlos una vez la incidencia haya sido solucionada.
Los agentes dispondrán de un mapa donde podrán ver las incidencias reportadas según su ubicación.
Tras haberse solucionado la incidencia reportada, los agentes pueden cerrarla, y en caso de tener subtickets, estos se cerraran tambien.

### 2.3 Restricciones del producto
La plataforma solo funcionará con conexión a internet, aunque los agentes contaran con un cache para ver tickets offline.
Los tickets contaran con una descripción con un número fijo de caracteres y 3 imágenes.
La plataforma respetará tanto la LOPD como la GDPR, y por extensión la Cookie Law. Debido a esto, se informará al usuario que al usar la plataforma, está de acuerdo con el uso de cookies en su navegador y con que nuestro servicio almacene sus datos. Además, los usuarios menores de 14 años no podrán utilizar la plataforma.

### 2.4 Perfiles de usuario
Los usuarios serán ciudadanos interesados en el buen estado de la infraestructura pública de donde vivan.
Nuestros usuarios objetivos son especialmente jóvenes (con una edad igual o superior a 14 años) y adultos, ya que tienen una mayor fácilidad para aprender a manejar nuevas herramientas tecnológicas.

### 2.5 Suposiciones y dependencias
El sistema dependerá de otros sistemas y librerías externos:
- [NodeJS](https://nodejs.org/es/): Backend hecho en javascript.
- [NPM](https://www.npmjs.com/): Gestor de paquetes de NodeJS.
- [Firebase de Google](https://firebase.google.com/): Base de datos nosql, sistema de gestión de usuarios que por correo y/o cuenta de Google, almacenamiento de archivos.
- [Bulma](https://bulma.io/): Framework de CSS.

Además, la plataforma empleará un servicio de geolocalizacion con una api de geolocalización (propia del navegador o externa) y un servicio de mapas, o bien OpenStreetMap o Google Maps.

### 3 Interfaces externas

#### 3.1 Interfaces con el usuario 
La página principal tanto para usuarios como para agentes solicitara el inicio de sesión. También habrá una opción de crear una cuenta de tipo usuario.
Después, dependiendo del tipo de usuario (usuario o agente), se mostraran interfaces distintas.

La interfaz para los usuarios permitirá ver los tickets creados en el pasado por el usuario en cuestión o crear un ticket nuevo.
Al pulsar el botón de crear ticket se mostrará una página con el formulario con los campos necesarios para crear un ticket. Una vez creado el ticket se volverá a la lista de tickets.
Los usuarios también dispondran de una pagina con los detalles de su cuenta donde podran hacer cambios o darse de baja en la plataforma.

La interfaz para los agentes mostrará un mapa con incidencias, así como estadísticas (número de tickets abiertos).
El agente podrá abrir un ticket de interes para inspeccionarlo, pudiendo ver las imágenes, descripción y subtickets del mismo, además de poder cerrarlo pulsando un botón.

Una característica importante es que el diseño estará optimizado para ser usado tanto en moviles como en ordenadores. Esto será gracias a un enfoque [Responsive Web Design](https://www.w3schools.com/html/html_responsive.asp) y [Mobile-First Design](https://www.initcoms.com/que-es-mobile-first-posicionamiento/).

#### 3.2 Interfaces con el Hardware
El sistema necesitará un servidor en el que ejecutar el backend, y los dispositivos de los usuarios y agentes (ordenadores o móviles).
En el caso de los dispositivos móviles, necesitarán disponer de GPS.
El servicio utilizará el protocolo HTTPS.

#### 3.3 Interfaces con el Software
La plataforma empleará Firebase de Google como base de datos ([Cloud Firestore](https://firebase.google.com/docs/firestore?hl=es-419)), sistema de almacenamiento ([Cloud Storage](https://firebase.google.com/docs/storage?hl=es-419)) y [autentificación](https://firebase.google.com/docs/auth?hl=es-419).

El sistema operativo del servidor será Linux ya que es más barato que Windows Server, aunque el sistema también podrá correr en un servidor Windows. En cualquier caso, debe tener instalados node y npm, además de disponer de puertos abiertos.
El sistema operativo de los clientes puede ser tanto Windows, Linux, MacOS, Android o iOS, siempre que disponga de un navegador web actualizado (2016 o más recientes).

## 4. Requisitos

### R1 - Conexión a internet
Los usuarios y agentes necesitan una conexión a internet activa.
#### Priodidad: Fundamental
#### Justificación
Para poder enviar, recibir y visualizar datos de la plataforma es necesario tener una conexión a internet activa.

### R1.1 - Navegador web moderno
Navegador con soporte HTML5, CSS, JavaScript, subida de archvios y preferiblemente geolocalización.
#### Prioridad: Fundamental
#### Justificación
Es necesario un navegador que cargue correctamente la página y que permita subir imágenes para poder utilizar la plataforma.

### R2 - Crear una cuenta de usuario
Los usuarios podrán crear una cuenta ingresando nombre, email y contraseña. Alternativamente podrán hacerlo con su cuenta de Google.
#### Prioridad: Fundamental
#### Dependencias: R1
#### Justificación
Los usuarios necesitaran una cuenta para poder crear y ver sus tickets.

### R3 - Crear una cuenta de agente
La creación de la cuenta de un agente depende del acuerdo con una entidad (por ejemplo el Ayuntamiento), por lo que su creación debe ser llevada acabo por los administradores de la plataforma.
#### Prioridad: Fundamental
#### Dependencias: R1
#### Justificación
Los agentes necesitan tener una cuenta para poder ver y cerrar tickets.

### R4 - Inicio de sesión
#### Prioridad: Fundamental
#### Dependencias: R1, R2, R3
#### Justificación
Tanto los usuarios como los agentes deben iniciar sesión para utilizar la plataforma.

### R5 - Crear ticket
Los usuarios podrán crear tickets de incidencias. El usuario proporcionara una descripción, imagenes y ubicacion de la incidencia.
#### Prioridad: Fundamental
#### Dependencias: R1, R4
#### Justificación
El objetivo de la plataforma es que los usuarios creen tickets para reportar incidencias, por lo que debe haber un mecanismo que habilite la creacion de tickets.

### R5.1 - Crear subticket
En caso de que exista un ticket similar previamente reportado (por proximidad geográfica), se pedira al usuario que confirme si efectivamente la incidencia ha sido reportada previamente. En caso afirmativo, el ticket se adjuntará como subticket al ticket principal.
#### Prioridad: Fundamental
#### Dependencias: R1, R4, R5
#### Justificación
Evitar que haya duplicados en el sistema para facilitar a los agentes la labor de revisar y cerrar tickets.

### R5.2 - Descripción de un ticket
La descripción tendrá un tamaño máximo de 240 caracteres.
#### Prioridad: Fundamental
#### Dependencias: R1, R4, R5
#### Justificación
Reducir el tamaño máximo que puede tener un ticket.

### R5.3 - Imagenes de un ticket
Un ticket contará con entre 1 y 3 imagenes, en formato png o jpg y de no mas de 15mb
#### Prioridad: Fundamental
#### Dependencias: R1, R4, R5
#### Justificación
Reducir el tamaño máximo que puede tener un ticket.

### R5.4 - Ubicación de un ticket
La ubicación de un ticket vendrá dada por el GPS del dispositivo en caso de estar usando un móvil, o de una API de terceros en caso contrario o si el GPS no esta disponible.
#### Prioridad: Deseable
#### Dependencias: R1, R4, R5
#### Justificación
Indicar a los agentes donde esta la incidencia a solucionar.

### R6 - Cerrar ticket
Un agente puede cerrar un ticket una vez solucionada una incidencia. Si el ticket tenia subtickets estos también se cerraran.
#### Prioridad: Fundamental
#### Dependencias: R1, R4
#### Justificación
Permite tanto a los usuarios como a los agentes que incidencias han sido resueltas. 

### R7 - Consultar tickets propios
Un usuario podrá ver todos los tickets que ha creado.
#### Prioridad: Fundamental
#### Dependencias: R1, R4, R5

### R8 - Mapa de tickets
Un agente podrá ver las incidencias en un mapa segun la ubicación de esta.
#### Prioridad: Opcional
#### Dependencias: R1, R4
#### Justificación
Permite ver a los agentes donde hay mayor número de incidencias.

### R9 - Consultar ticket
Un agente podrá ver los detalles de un ticket.
#### Prioridad: Fundamental
#### Dependencias: R1, R4
#### Justificación
Permite al agente ver toda la información necesaria de una incidencia para poder reportarla y solucionarla.

### R10 - Detalles de la cuenta
Un usuario podrá consultar y modificar los detalles de su cuenta.
#### Prioridad: Deseable
#### Dependencias: R1, R4
#### Justificación
Permitir a un usuario modificar detalles como su dirección de correo y nombre de usuario.

### R11 - Cerrar cuenta
Un usuario podrá cerrar su cuenta. Los tickets creados por este usuario permanecerán en el sistema.
#### Prioridad: Deseable
#### Dependencias: R1, R4, R7

### R12 - Protocolo del servidor
La web será servida mediante HTTPS.
#### Prioridad: Deseable
#### Justificación
El HTTPS garantiza la encriptacion de los datos y permite usar herramientas como la geolocalización en el navegador.

### R13 - LOPD y GDPR
La información de los usuarios estará custodiada de acuerdo a la LOPD y GDPR. Los menores de 14 años no podrán usar la plataforma.
#### Prioridad: Fundamental

### 4.1 Precedencia y prioridad

| Id   | Nombre                      | Descripción                                                                                                                                                                                                                                                                              | Prioridad   | Precedencia    | Tipo         |
|------|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|----------------|--------------|
| R1   | Conexión a internet         | Los usuarios y agentes necesitan una conexión a internet<br>  activa.                                                                                                                                                                                                                    | Fundamental |                | No funcional |
| R1.1 | Navegador web moderno       | Navegador con soporte HTML5, CSS, JavaScript, subida de<br>  archivos y preferiblemente geolocalización.                                                                                                                                                                                 | Fundamental |                | No funcional |
| R2   | Crear una cuenta de usuario | Los usuarios podrán crear una cuenta ingresando nombre, email<br>  y contraseña. Alternativamente podrán hacerlo con su cuenta de Google.                                                                                                                                                | Fundamental | R1             | Funcional    |
| R3   | Crear una cuenta de agente  | La creación de la cuenta de un agente depende del acuerdo con<br>  una entidad (por ejemplo el Ayuntamiento), por lo que su creación debe ser<br>  llevada acabo por los administradores de la plataforma.                                                                               | Fundamental | R1             | Funcional    |
| R4   | Inicio de sesión            | Tanto los usuarios como los agentes deben iniciar sesión para<br>  utilizar la plataforma.                                                                                                                                                                                               | Fundamental | R1, R2, R3     | Funcional    |
| R5   | Crear Ticket                | Los usuarios podrán crear tickets de incidencias. El usuario<br>  proporcionara una descripción, imágenes y ubicación de la incidencia.                                                                                                                                                  | Fundamental | R1, R2, R4     | Funcional    |
| R5.1 | Crear subticket             | En caso de que exista un ticket similar previamente reportado<br>  (por proximidad geográfica), se pedira al usuario que confirme si<br>  efectivamente la incidencia ha sido reportada previamente. En caso<br>  afirmativo, el ticket se adjuntará como subticket al ticket principal. | Fundamental | R1, R2, R4, R5 | Funcional    |
| R5.2 | Descripción de un ticket    | La descripción tendrá un tamaño máximo de 240 caracteres.                                                                                                                                                                                                                                | Fundamental | R1, R2, R4, R5 | No funcional |
| R5.3 | Imagenes de un ticket       | Un ticket contará con entre 1 y 3 imagenes, en formato png o<br>  jpg y de no mas de 15mb.                                                                                                                                                                                               | Fundamental | R1, R2, R4, R5 | No funcional |
| R5.4 | Ubicación de un ticket      | La ubicación de un ticket vendrá dada por el GPS del<br>  dispositivo en caso de estar usando un móvil, o de una API de terceros en<br>  caso contrario o si el GPS no esta disponible.                                                                                                  | Deseable    | R1, R2, R4, R5 | No funcional |
| R6   | Cerrar ticket               | Un agente puede cerrar un ticket una vez solucionada una<br>  incidencia. Si el ticket tenia subtickets estos también se cerraran.                                                                                                                                                       | Fundamental | R1, R2, R4     | Funcional    |
| R7   | Consultar tickets propios   | Un usuario podrá ver todos los tickets que ha creado.                                                                                                                                                                                                                                    | Fundamental | R1, R2, R4, R5 | Funcional    |
| R8   | Mapa de tickets             | Un agente podrá ver las incidencias en un mapa segun la<br>  ubicación de esta.                                                                                                                                                                                                          | Opcional    | R1, R3, R4     | Funcional    |
| R9   | Consultar ticket            | Un agente podrá ver los detalles de un ticket.                                                                                                                                                                                                                                           | Fundamental | R1, R3, R4     | Funcional    |
| R10  | Detalles de la cuenta       | Un usuario podrá consultar y modificar los detalles de su<br>  cuenta.                                                                                                                                                                                                                   | Deseable    | R1, R2, R4     | Funcional    |
| R11  | Cerrar cuenta               | Un usuario podrá cerrar su cuenta. Los tickets creados por<br>  este usuario permanecerán en el sistema.                                                                                                                                                                                 | Deseable    | R1, R2, R4, R7 | Funcional    |
| R12  | Protocolo del servidor      | La web será servida mediante HTTPS.                                                                                                                                                                                                                                                      | Deseable    |                | No funcional |
| R13  | LOPD y GDPR                 | La información de los usuarios estará custodiada de acuerdo a<br>  la LOPD y GDPR. Los menores de 14 años no podrán usar la plataforma.                                                                                                                                                  | Fundamental |                | No funcional |


### 4.2 Funcionales
[Casos de uso](https://github.com/rubenjr0/SRS-Template/blob/master/CasosDeUso.pdf).

### 4.3 Calidad de Servicio
#### R1: Es necesaria una conexión a internet para usar la plataforma.
#### R2: Es necesario un navegador con las funciones especificadas para utilizar la plataforma.
#### R5.1, R5.2, R5.3: Con estas especificaciones se busca reducir el tamaño de los tickets para poder almacenar más.
#### R5.4: La ubicación del ticket permite localizar las incidencias.

#### 4.3.1 Seguridad
#### R12: El HTTPS es más seguro que el HTTP y permite usar geolocalización en el navegador.
#### R13: El cumplimiento de estas normas es necesario para que la plataforma sea usable.

#### 4.3.2 Fiabilidad
#### R13: El cumplimiento de estas normas es necesario para que la plataforma sea usable.

### 4.4 Diseño e implementación

#### 4.4.1 Reusabilidad
Firebase de Google para la base de datos, almacenamiento y gestión de cuentas.

#### 4.4.2 Portabilidad
NodeJS corre tanto en sistemas de tipo UNIX (Linux y MacOS) como en Windows, por lo que el backend funcionará en cualquier equipo con estos sistemas operativos siempre que tenga NodeJS y NPM instalado.

Los usuarios y agentes podrán acceder a la plataforma desde sus dispositivos móviles y ordenadores.

#### 4.4.3 Fecha de entrega
5 de Junio de 2020

## 5. Verificación
Se utilizarán librerias de testing para javascript para verificar el backend, además de herramientas como Postman e Insomnia para comprobar que los datos servidos por el servidor son correctos.

### Apéndice B: Generar PDF usando un fichero MD
Hay multitud de herramientas online y offline, por ejemplo: https://www.markdowntopdf.com/

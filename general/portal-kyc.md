---
description: Consolidado de consultas realizadas por la empresa
cover: ../.gitbook/assets/login-bg.487dd9af.jpg
coverY: 0
---

# 〽️ Portal KYC

{% hint style="info" %}
**GBC tip:** Este producto puede ser utilizado para el control de peticiones o para el uso de los componentes propiamente. No requiere configuración adicional.
{% endhint %}

## Vista general

Video demostrativo con algunas reseñas de su utilidad:

* Control de usuarios&#x20;
* Control de peticiones
* Asignación de permisos a los usuarios por servicios
* Uso de los componentes como  servicios (Lista de sanciones, LivenessCheck y Lectura de documento de identidad)
* Personalización del servicio Secure Link (Solo aplica para Administradores Clientes)

<figure><img src="../.gitbook/assets/1215.gif" alt=""><figcaption></figcaption></figure>



## Blacklist Masivo

Con éste servicio le será posible realizar consultas a Listas de Sanciones y/o PEP's de manera masiva, se realizaría a través de un archivo CSV en donde enlistará a todas las personas y/o compañías que quisieras analizar.

Los Headers del CSV se compone de la siguiente manera:

<table><thead><tr><th width="192">Key</th><th width="102">Tipo</th><th>Descripción</th></tr></thead><tbody><tr><td>First Name</td><td>string</td><td>Nombre de la persona a analizar. También pude ir varios nombres ej.: "Horacio Manuel"</td></tr><tr><td>Last Name</td><td>string</td><td>Apellido de la persona a analizar. También pude ir varios apellidos ej.: "Cartes Jara"</td></tr><tr><td>Street</td><td>string</td><td>Calle de la búsqueda</td></tr><tr><td>City</td><td>string</td><td>Ciudad de la búsqueda</td></tr><tr><td>State</td><td>string</td><td>Estado de la búsqueda</td></tr><tr><td>Country</td><td>string</td><td>País de nacimiento de la búsqueda</td></tr><tr><td>Zip</td><td>string</td><td>Código Postal de la búsqueda</td></tr><tr><td>Company</td><td>string</td><td>Nombre de la compañía</td></tr><tr><td>Date of Birth</td><td>string</td><td>Fecha Nacimiento de la Persona. Formato iso 8601(yyyy-dd-mm) o Unix Timestamp</td></tr><tr><td>Man</td><td>N/A</td><td>N/A</td></tr><tr><td>Merchant txn Id</td><td>N/A</td><td>N/A</td></tr></tbody></table>

Puedes obtener un ejemplo del archivo CSV al darle clic [aquí.](https://drive.google.com/file/d/1lJZBDYSYs-yBAyV4gi0w0ruiCCa\_TJtz/view?usp=drive\_link)

A continuación se mostrará un video ilustrativo de como utilizar el servicio de Blacklist Masivo

<figure><img src="../.gitbook/assets/BlacklistBatch (1).gif" alt=""><figcaption></figcaption></figure>

Como resultado del proceso se obtendrá un resumen de personas y las listas en las que se encontraron coincidencias, también se dispone de la opción de descargar un archivo CSV con dicha información.

El archivo CSV de respuesta consta de los siguientes headers

<table><thead><tr><th width="192">Key</th><th width="102">Tipo</th><th>Descripción</th></tr></thead><tbody><tr><td>batchId</td><td>string</td><td>id de lote</td></tr><tr><td>firstName</td><td>string</td><td>Nombres utilizados como filtro</td></tr><tr><td>lastName</td><td>string</td><td>Apellidos utilizados como filtro</td></tr><tr><td>country</td><td>string</td><td>País utilizado como filtro</td></tr><tr><td>birthDate</td><td>string</td><td>Fecha Nacimiento utilizado como filtro</td></tr><tr><td>matchesListId</td><td>string</td><td>Id's de las listas en las que se encontraron coincidencias</td></tr><tr><td>matchesListCategory</td><td>string</td><td>Categorías de las listas en las que se encontraron coincidencias</td></tr><tr><td>matchesListDescription</td><td>string</td><td>Descripciones de las listas en las que se encontraron coincidencias</td></tr><tr><td>matchesLastUpdate</td><td>string</td><td>Fechas de las ultimas actualizaciones de las listasen las que se encontraron coincidencias</td></tr><tr><td>matchesNames</td><td>string</td><td>Nombres en las listas con la hubieron coincidencias</td></tr></tbody></table>

# ℹ️ ¿Cómo reducir el tamaño del Payload Final?

### inicio

La función de reducir el Payload Final consiste en reemplazar las imágenes en Base64 de la estructura final por códigos identificadores de dichas imágenes a fin de reducir considerablemente el tamaño de lo que se retorna.

### ¿Cómo activar la función?

La función se habilita encendiendo el switch de ducha función través del Portal KYC -> Mi Perfil.

<figure><img src="../.gitbook/assets/Reducir payload.png" alt=""><figcaption></figcaption></figure>

### ¿Cómo obtener las imágenes?

Para obtener las imágenes en base64 se precisa de un JWT generado con las credenciales del cliente como en el [paso 1 ](../implementacion/secure-link-implementacion.md)de la generación del link seguro y ya con ésta se tienen dos opciones.

#### Opción 1

La primera opción consiste en recuperar todas las imágenes recabas durante un link seguro a través de un endpoint habilitado que tiene como parámetro el tracking\_id obtenida en el Payload Final.

<mark style="color:blue;">`GET`</mark> `{host_api}api-hub/v1/images?tracking_id={tracking_id}`

#### Query Parameters

| Name                                           | Type   | Description                               |
| ---------------------------------------------- | ------ | ----------------------------------------- |
| tracking\_id<mark style="color:red;">\*</mark> | String | tracking\_id obtenido en el payload final |

#### Headers

| Name                                            | Type | Description                                   |
| ----------------------------------------------- | ---- | --------------------------------------------- |
| Authorization<mark style="color:red;">\*</mark> | JWT  | JWT generado con las credenciales del cliente |

#### Opción 2

La segunda opción consiste en recuperar una sola imagen a través de un endpoint habilitado que tiene como parámetro mediante el código identificador del base64 retornada en el Payload Final.

<mark style="color:blue;">`GET`</mark> `{host_api}api-hub/v1/image?image_id={image_id}`

#### Query Parameters

| Name                                        | Type   | Description                    |
| ------------------------------------------- | ------ | ------------------------------ |
| image\_id<mark style="color:red;">\*</mark> | String | Codigo identificador de Imagen |

#### Headers

| Name                                            | Type | Description                                   |
| ----------------------------------------------- | ---- | --------------------------------------------- |
| Authorization<mark style="color:red;">\*</mark> | JWT  | JWT generado con las credenciales del cliente |

### ¿Cuánto tiempo tengo para descargar las imágenes?

Actualmente el cliente tiene un tiempo limite de 5 días desde la creación del link seguro para obtener sus imágenes, luego de dicho plazo las imágenes serán borradas del entorno de almacenamiento temporal.

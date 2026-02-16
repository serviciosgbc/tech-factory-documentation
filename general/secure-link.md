---
description: >-
  Es una herramienta que tiene como objetivo facilitar el onboarding de usuarios
  de una forma rápida y segura. Compatible para desarrollos web y mobile
  (webview)
---

# 🔐 Secure Link

<figure><img src="../.gitbook/assets/Captura de pantalla 2023-05-30 a la(s) 13.50.03.png" alt=""><figcaption></figcaption></figure>

Consiste en generar una intención de onboarding con el llamado a nuestra API, retornamos un link con el que inicia el proceso de carga de documento (OCR), posteriormente pasa al Liveness Check y finalmente se ejecuta el FaceMatch, en el caso de completar el flujo se enviarán los datos recaudados a un callback previamente definido en el llamado de la intención. En caso de que no se complete el flujo pero el token siga vigente podrá retomar el proceso en el paso por completar.

Podrá configurar y personalizar los estilos de los componentes a través del Portal KYC. También podrá ajustar la vigencia del Token.

<figure><img src="../.gitbook/assets/Captura de pantalla 2023-05-30 a la(s) 11.54.10 (1).png" alt=""><figcaption></figcaption></figure>

## Estructura de datos que retorna el Secure Link

Tras completar el proceso se enviará un JSON con toda la data recaudada usando el callback definido al inicio de la petición (Intención de Onboarding). La estructura del JSON está definida en [este apartado](https://global-bridge-connections-paragu.gitbook.io/dashboard-kyc/base-de-conocimientos/que-datos-retorna-el-servicio-de-secure-link).



## 1 - Lectura de documento de identidad (OCR)

Vista donde se carga un documento de identidad, reconoce la información y extrae para ser retornada en formato JSON, con esto permite automatizar la captura de datos y reduce el margen de error en una transcripción. Los datos que retorna el componente son todos los capturados del documento. (Varían de acuerdo al país y tipo de documento). Se puede optar por solicitar uno o ambos lados del documento según la necesidad.

<figure><img src="../.gitbook/assets/Captura de pantalla 2023-05-30 a la(s) 11.44.02.png" alt=""><figcaption></figcaption></figure>

## 2 - LivenessCheck

Vista en la que se da fe de vida de la persona frente a la cámara, entre los datos que retorna este componente se encuentra la foto de la persona la cual fue validada, esta foto podrá ser comparada contra un documento de identidad o una base de datos para asegurar que sea la misma persona. Otras funciones que puede encontrar:

* Valida si realmente es un adulto
* Si usa mascarilla medica, lentes, sombrero

<figure><img src="../.gitbook/assets/Captura de pantalla 2023-05-30 a la(s) 11.46.31.png" alt=""><figcaption></figcaption></figure>

## 3 - FaceMatch

Proceso que se ejecuta de fondo cuando el Liveness Check finaliza. Compara la imagen del documento de identidad versus la selfie que captura en el momento. El dato que retorna es el porcentaje de similitud entre ambos rostros.


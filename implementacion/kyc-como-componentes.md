---
description: Librería desarrollada en React JS + Node Js
---

# 🖥️ KYC como componentes

## Instalación de la librería

Con NPM:

```
$ npm i gbc-kyc-kit
```

Con Yarn:

```
$ yarn add gbc-kyc-kit
```

## Importar los estilos

Importar los css de la librería:

```
import '../node_modules/gbc-kyc-kit/dist/style.css'
```

## Personalizar los estilos

Podrás adaptar los componentes con el estilo de tu aplicación, solo debes usar el custom css de la siguiente manera:

{% hint style="warning" %}
Recuerda que tienes el prop mode que puede variar entre dark o light sin necesidad de alterar los estilos del componente.
{% endhint %}

{% tabs %}
{% tab title="CSS/SASS/SCSS" %}
```css
:root {
  --primary: #1976d2;
  --primary-hov: #2689ed;
  --secondary: #e8edff;
  --button-color: #1976d2;
  --text-button-color: #fff;
  --secondary: #e8edff;
  --warning: #f8bb86;
  --success: #4caf50;
  --error: #ff1199;
  --text-color: #8c8c8c;
  --title-color: #262626;
  --font-family: "Noto Sans", sans-serif;
}
```
{% endtab %}
{% endtabs %}

## Importar los componentes

```
import { BlackList, LivenessCheck, DocumentReader, FaceMatch } from 'gbc-kyc-kit'
```

Ejemplos:

{% hint style="warning" %}
Para todos los componentes se debe enviar un token que tiene como expiración 1 hora y eso es lo que retorna el método getAccessToken, Aquí un ejemplo👇
{% endhint %}

```
import axios from "axios";

const TOKEN    = "**************" //Bearer Token entregado por Global Bridge Connections
const clientId = "**************" //Client ID entregado por Global Bridge Connections
const host_api = "https://gbc-py-core-master-api-products-rtm3lv2joa-uc.a.run.app/"
/* Se recomienda administrar estos valores como variables de entorno */

async function getAccessToken(){
    const customHeaders = {
      "Content-Type": "application/json", 
      "Authorization": TOKEN
    }
    
    const parseReq = {
      method: "POST",
      url: `${host_api}api-hub/oauth2/v1/generate_access_token`,
      headers: customHeaders,
      data: {
          "grant_type":"client_credentials",
      }
    }

    try{
      const res = await axios(parseReq);
      const { access_token } = res.data;
      return access_token;
    } catch (error){
      throw new error('Error al obtener el Token')
    }
  }
```

{% hint style="warning" %}
Para el uso con TS es important crear un archivo customType.d.ts dentro de la carpeta src que contenga: **declare module 'gbc-kyc-kit'**
{% endhint %}



<table><thead><tr><th width="166">Props</th><th width="100">Type</th><th width="202">Values</th><th>Description</th></tr></thead><tbody><tr><td>inProduction</td><td>string</td><td>prd | stg | dev</td><td>Este atributo no es requerido, el defaultValue es "prd". Toda prueba de integración y reconocimiento debe ser realizada con "dev", la data que retorna es dummy, posteriormente puede pasar a "stg" para recibir datos reales y por último, pasarían a "prd" donde se hace validación de host e IP.</td></tr><tr><td>mode</td><td>string</td><td>dark | light</td><td>Este atributo no es requerido, el defaultValue es "light".</td></tr><tr><td>clientId</td><td>string</td><td>Entregado por Global Bridge Connections</td><td>Este valor es único por cada cliente y será entregado previo acuerdo comercial.</td></tr><tr><td>authorize</td><td>promise</td><td>() => Promise()</td><td>Función que valida clientId vs TOKEN y retorna un accessToken habilitado por una hora para ejecutar el resto de las peticiones.</td></tr><tr><td>picBase64</td><td>string</td><td></td><td>Este atributo es requerido. Es utilizado para comparar dos rostros (Un rostro lo da el cliente en base64 y el otro sería el selfie capturado mediante la webcam)</td></tr><tr><td>countryCodeAllowed</td><td>array</td><td>["PY", "PE", ...]</td><td>Atributo no requerido, en el caso de pasar un arreglo con los códigos de países permitidos se hará una validación de la IP del usuario para permitir o no el uso del componente. El código de país debe ser en formato ISO Alpha-2 code</td></tr><tr><td>validateVpn</td><td>boolean</td><td></td><td>Atributo no requerido, por defecto es false, si viene en true se validará que el usuario no esté usando VPN o Proxy</td></tr><tr><td>dualModeRequired</td><td>boolean</td><td></td><td>Atributo no requerido, por defecto es false, en el caso que sea true se obligará al usuario cargar ambos lados del documento. Solo aplica para OCR Component</td></tr><tr><td>successMessage</td><td>string</td><td></td><td>Atributo utilizado para customizar el mensaje exitoso en cada componente</td></tr><tr><td>alertMessage</td><td>string</td><td></td><td>Atributo utilizado para customizar el mensaje de alerta si existe coincidencias con listas de saniones. Solo aplica para Blacklist Component</td></tr><tr><td>faceMatch</td><td>string</td><td></td><td>Atributo para pasar una imagen en base64 o url. En el caso que sea distinto de null se procesará una comparación de rostro entre el liveness y la foto enviada. Solo aplica para LivenessCheck Component.</td></tr><tr><td>showFilterByButton</td><td>boolean</td><td></td><td>Atributo no requerido. Si este atributo se pasa como false el componente oculta el botón 'Filtrar por' luego de realizar una búsqueda. El valor predeterminado es verdadero.</td></tr></tbody></table>



{% tabs %}
{% tab title="BlackList" %}
<pre><code><strong>&#x3C;BlackList
</strong>    clientId={clientId}
    authorize={getAccessToken}
    dataBlackList={getDataBlackList}
    inProduction= "prd" // Default value is prd, not is required
    mode= 'dark' // Default value is light, not is required
    countryCodeAllowed={["PY","PE"]} // En este caso solo se estarían permitiendo usuarios conectados desde Paraguay o Perú
/>
</code></pre>
{% endtab %}

{% tab title="DocumentReader" %}
<pre><code>const getDataDocument = async (info) => {
    if (info) {
      console.log(info.data)
    }
}
//getDataDocument es la función con la que podrá capturar los datos que retorna el componente
<strong>
</strong><strong>&#x3C;DocumentReader
</strong>    dataDocument={getDataDocument}
    clientId={clientId}
    authorize={getAccessToken}
    inProduction="prd"
/>
</code></pre>
{% endtab %}

{% tab title="LivenesCheck" %}
<pre><code>const listener = (event) => {
    console.log(event)
    if (event.detail) {
      if (event.detail.action === 'PROCESS_FINISHED') {
        const { response } = event.detail.data
        console.log(response)
      }
    }
  }

useEffect(() => {
    const component = document.getElementsByTagName('face-liveness')[0]
    if (component) {
      component.addEventListener('face-liveness', listener)
    }
  }, [listener])
 
<strong>&#x3C;LivenessCheck
</strong>    clientId={clientId}
    authorize={getAccessToken}
    inProduction="prd"
/>
</code></pre>
{% endtab %}

{% tab title="FaceMatch" %}
<pre><code>const getDataFaceMatch = async (info) => {
    if (info) {
      console.log(info.data)
    }
}
//getDataFaceMatch es la función con la que podrá capturar los datos que retorna el componente
<strong>
</strong>const picbase64 = " ...Este es el base64 de la imagen a ser comparada con el selfie. Puede ser el rostro que sale en documento de identidad u otra imagen como la de un onboarding por ejemplo"
<strong>
</strong><strong>&#x3C;FaceMatch
</strong>    dataFaceMatch={getDataFaceMatch}
    clientId={clientId}
    authorize={getAccessToken}
    inProduction="prd"
    picBase64={picbase64}
/>
</code></pre>
{% endtab %}
{% endtabs %}


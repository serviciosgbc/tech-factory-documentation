# ℹ️ ¿Qué datos retorna el servicio de Secure Link?

## Estructura de datos del Payload Final

Una vez finalizado el proceso de onboarding, el servicio de Secure Link proporcionará un JSON que contendrá todos los datos recopilados durante dicho proceso. Este JSON será enviado al callback que el cliente haya definido al generar el link seguro.&#x20;

#### Está compuesto por:

* **external\_id:**&#x20;
  * Identificador único que envía el cliente al inicio del proceso para el control de peticiones.
* **tracking\_id:**&#x20;
  * Identificador único que hace referencia al evento por el lado de IDG.
* **liveness:**&#x20;
  * Objeto que contiene una foto en formato base64 o MD5, representa la selfie del proceso de Livenes Check. También contiene el porcentaje de coincidencia entre la foto del documento de identidad y la selfie.
* **blacklist:**&#x20;
  * Aparecerán tantos arreglos como coincidencias existan con ese criterio de búsqueda (Nombres y apellidos).
  * En el caso que no se detecte coincidencia quedaría el arreglo vacío.
  * Cada arreglo interno representa una lista de sanción en el que el primer valor de ese arreglo será el nombre de la lista y el resto de los valores son complementarios. (Varía de acuerdo a la lista, persona y país).
* **document\_data:**
  * Retorna un objeto con todos los datos extraídos del documento de identidad (ambos lados).

La estructura del JSON resultante es la siguiente:



{% hint style="info" %}
El campo _**reference**_ siempre retornará el número del documento escaneado mientras que _**documentNumber**_ retornará el número de cédula de la persona.\
\
Si el documento escaneado es una cédula entonces tanto reference como documentNumber tendrán el mismo dato.
{% endhint %}

{% hint style="warning" %}
Dentro de **document\_data** hay 4 campos booleanos que permitirán alertar cuando un documento fue capturado de forma errada. Tener en cuenta las [recomendaciones](https://global-bridge-connections-paragu.gitbook.io/dashboard-kyc/base-de-conocimientos/calidad-de-imagen-requerido) para la captura correcta de un documento.

**qa\_doc\_out\_focus** = El documento está desenfocado

**qa\_moire\_present** = Se detectó un patrón de muaré

**qa\_doc\_incomplete =** El documento no figura completamente en la foto

**qa\_doc\_out\_perspective** = El documento está fuera de perspectiva (Ángulo incorrecto)
{% endhint %}

{% code lineNumbers="true" fullWidth="false" %}
```json
{
    "external_id": string | null,
    "tracking_id": string,
    "liveness": {
        "selfie": string | null,
        "similarity": number | null
    },
    "blacklist": string[][],
    "document_data": {
        "mrz": string | null,
        "sex": string | null,
        "status": string | null,
        "address": string | null,
        "last_name": string,
        "reference": string | null, // Número del documento escaneado
        "first_name": string,
        "date_expiry": string | null, // Formato estándar aaaa-mm-dd
        "fathers_name": string | null,
        "mothers_name": string | null,
        "date_of_birth": string | null,
        "date_of_birth_std": string | null, // Formato estándar aaaa-mm-dd
        "document_category": string | null,
        "document_type": string | null,
        "marital_status": string | null,
        "document_number": string | null, //Número de cédula de identidad
        "documents_image": {
            "first_image": string | null,
            "second_image": string | null,
        },
        "first_last_name": string | null,
        "reference_image": string | null,
        "document_country": string | null,
        "nationality_code": string | null,
        "qa_doc_out_focus": boolean,
        "qa_moire_present": boolean,
        "second_last_name": string | null,
        "qa_doc_incomplete": boolean,
        "qa_doc_out_perspective": boolean,
        "count_side_doc_analized": number,
        "donor": string | null,
        "height": string | null,
        "blood_group": string | null
    }
}
```
{% endcode %}



{% hint style="warning" %}
Ejemplo de payload retornado al final del proceso de onboarding (Estos datos son netamente utilizados para ejemplificar un caso de uso. No son datos reales).
{% endhint %}

<pre class="language-json" data-line-numbers><code class="lang-json">```json
{
<strong>    "liveness": {
</strong><strong>        "selfie": "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAYEBQYFBAYGBQYHBwYIChAKCgkJChQODwwQFxQYGBcUFhYaHSUfGhsjHBYWICwgIyYnKSopGR8tMC0...",
</strong>        "similarity": 0.030609101057052612
    },
<strong>    "blacklist": [
</strong><strong>        [
</strong>            "PEP_BRA",
            " Names: [Leonardo De Farias Duarte]",
            " Address:[Country:PE]",
            " Function: National Council of Public Prosecutions",
            " Ex Adviser",
            " NOT IN CHARGE SINCE: 27.08.2015",
            " CATEGORY: Ex PEPs",
            " State Executive Functions",
            " Government",
            " Ministries",
            " Match score of 100"
        ],
        [
            "PEP_BRA",
            " Names: [Leonardo Duarte Pascoal",
            " Pascoal",
            " Leonardo]",
            " Date of Birth:[1990-09-01]",
            " Address:[Country:PE]",
            " Function: Municipality of Esteio",
            " Mayor",
            " CATEGORY: Regional and Local Functions",
            " Match score of 100"
        ],
        [
            "OFAC_SDN",
            " Names: [Franklyn Leonardo Duarte]",
            " Date of Birth:[1977-05-15]",
            " Address:[stateOfProvince:Tachira;Country:PE]"
        ]
    ],
    "external_id": "a2545ht6-v154c-4487-s666eew4789",
    "tracking_id": "c842cd13-b2dd-42da-93b0-d223c00ac09c",
    "document_data": {
        "mrz": "CEESP879451&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;^8610278M2509149ESP&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;6^DUARTE&#x3C;&#x3C;LEONARDO&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;&#x3C;",
        "sex": "M",
        "status": "ACTIVE",
        "address": "CALLE 123 MIRAFLORES",
        "last_name": "DUARTE ESPINOSA",
        "reference": "879451",
        "first_name": "LEONARDO",
        "date_expiry": "2025-09-14",
        "fathers_name": null,
        "mothers_name": null,
        "date_of_birth": "760927",
        "document_type": "Peru - Residence Permit #4 Side B",
        "marital_status": "S",
        "document_number": "879451",
        "documents_image": {
            "first_image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArYAAAPoCAYAAAAr8L3fAAAAAXNSR0IArs4c6QAAIABJREFUeF50vdd3nVeS5RnXAx...",
            "second_image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAoUAAAPoCAYAAACoNITkAAAAAXNSR0IArs4c6QAAIABJREFUeF50vWezHFmSLOapSlddraAa..."
        },
        "first_last_name": "DUARTE ESPINOSA",
        "reference_image": "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEBFQEVAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcK...",
        "document_country": "PER",
        "nationality_code": "ESP",
        "qa_doc_out_focus": false,
        "qa_moire_present": false,
        "second_last_name": null,
        "date_of_birth_std": "1976-09-27",
        "document_category": "Residence Permit",
        "qa_doc_incomplete": true,
        "qa_doc_out_perspective": false,
        "count_side_doc_analized": 2,
        "donor": null,
        "height": null,
        "blood_group": null
    }
}
```
</code></pre>


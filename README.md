# ChatLink API

ChatLink le permite integrar la recepción y envío de mensajes de WhatsApp en cualquiera de sus sistemas.
- La API utiliza el formato JSON https://www.json.org .
- Un Webhook es un sistema de comunicación automático que funciona a través de solicitudes del protocolo HTTP y que permite el intercambio de datos entre aplicaciones web en tiempo real.
- El Webhook recibirá los datos en formato JSON mediante el método POST del protocolo HTTP.
- Cuando la respuesta de la API contenga esl código de estado **4xx** o **5xx** se responderá con un JSON con el mensaje de error correspondiente.
- Query String o "Cadena de consulta" son parámetros que se añaden en la URL paara indicar datos.

## Endpoints Abiertos

Endpoints abiertos que no requieren autenticación.

------------------------------------------------------------------------------------------

#### Login

<details>
 <summary><code>POST</code> <code><b>/api/Login</b></code> <code>Emite un token que dura 2 días</code></summary>

##### Parámetros

> | Parámetro              |  Requerido?     | Tipo de Dato      | Descripción                         |
> |-------------------|-----------|----------------|-------------------------------------|
> | `Email` |  Sí | string   | Email del Usuario        |
> | `Password` |  Sí | string   | Password del Usuario        |



##### Respuesta JSON

> | Propiedad  | Descripción  |
> |----------|----------|
> | token    | Token de autorización que se utilizara en cada solicitud HTTP que requiera autenticación    |


</details>

------------------------------------------------------------------------------------------


## Endpoints que requieren Authenticación

Los Endpoints cerrados requieren que se incluya un **TOKEN** válido en el encabezado la solicitud HTTP mediante el header `Authorization: Bearer TOKEN` o mediante el *Query String* `?token=TOKEN `. Se puede adquirir un **TOKEN** desde el Endpoint anterior.


------------------------------------------------------------------------------------------


<details>
 <summary><code>GET</code> <code><b>/api/NewSession</b></code> <code>Crear una nueva sesión de WhatsApp</code></summary>


##### Respuesta JSON
> | Propiedad  | Descripción  | Tipo de Dato  |
> |----------|----------|----------|
> | `idSession`    | Identificador único para cada sesión de WhatsApp    | string    |




</details>



<details>
 <summary><code>GET</code> <code><b>/api/MySessions</b></code> <code>Listar las sesiones</code></summary>


##### Respuesta JSON (Array)

> | Propiedad  | Descripción  | Tipo de Dato  |
> |----------|----------|----------|
> | `idSession`    | Identificador único para cada sesión de WhatsApp    | string    |
> | `hasCredentials`    | Indica si la sesión tiene vinculado un dispositivo    | boolean/null    |
> | `Webhook`    | Webhook configurado para la sesión    | string/null    |
> | `DownloadMedia`    | Indica si la sesión descargará el contenido multimedia enviado (audio, fotos, video, stickers)    | boolean    |
> | `isRunning`    | Indica si la sesión se encuentra corriendo   | boolean    |
> | `qr`    | Valor del QR a escanear con la aplicación de WhatsAPp para autenticar la sesión   | string    |
> | `isConnected`    | Identifica si la sesión se encuentra conectada y autenticada    | boolean    |


</details>

<details>
 <summary><code>GET</code> <code><b>/api/Session/{idSession}</b></code> <code>Obtener la información relativa a una sesión</code></summary>


##### Respuesta JSON

> | Propiedad  | Descripción  | Tipo de Dato  |
> |----------|----------|----------|
> | `idSession`    | Identificador único para cada sesión de WhatsApp    | string    |
> | `hasCredentials`    | Indica si la sesión tiene vinculado un dispositivo    | boolean/null    |
> | `Webhook`    | Webhook configurado para la sesión    | string/null    |
> | `DownloadMedia`    | Indica si la sesión descargará el contenido multimedia enviado (audio, fotos, video, stickers)    | boolean    |
> | `isRunning`    | Indica si la sesión se encuentra corriendo   | boolean    |
> | `qr`    | Valor del QR a escanear con la aplicación de WhatsAPp para autenticar la sesión   | string    |
> | `isConnected`    | Identifica si la sesión se encuentra conectada y autenticada    | boolean    |

</details>

<details>
 <summary><code>DELETE</code> <code><b>/api/Session/{idSession}</b></code> <code>Eliminar una sesión</code></summary>


##### Respuesta JSON
> | Propiedad  | Descripción  | Tipo de Dato  |
> |----------|----------|----------|
> | `status`    | Estado de la eliminación   | string    |




</details>

<details>
 <summary><code>GET</code> <code><b>/api/Session/{idSession}/Start</b></code> <code>Iniciar una sesión</code></summary>


##### Respuesta JSON
> | Propiedad  | Descripción  | Tipo de Dato  |
> |----------|----------|----------|
> | `status`    | Estado de la inicialización   | string    |




</details>

<details>
 <summary><code>GET</code> <code><b>/api/Session/{idSession}/Stop</b></code> <code>Parar una sesión</code></summary>


##### Respuesta JSON
> | Propiedad  | Descripción  | Tipo de Dato  |
> |----------|----------|----------|
> | `status`    | Estado de éxito   | string    |




</details>

<details>
 <summary><code>POST</code> <code><b>/api/Session/{idSession}/SendMessage</b></code> <code>Envíar un Mensaje</code></summary>

##### Parámetros

> | Parámetro              |  Requerido?     | Tipo de Dato      | Descripción                         |
> |-------------------|-----------|----------------|-------------------------------------|
> | `To` |  Sí | string   | ID del grupo/usuario de WhatsApp, también puede ser el número de teléfono con el prefijo correspondiente al país        |
> | `text` |  Sí | string   | Mensaje que se enviará        |



##### Respuesta JSON

> | Propiedad  | Descripción  | Tipo de Dato  |
> |----------|----------|----------|
> | `status`    | Estado de éxito   | string    |


</details>

<details>
 <summary><code>POST</code> <code><b>/api/Session/{idSession}/SetWebhook</b></code> <code>Configurar el Webhook para una sesión</code></summary>

##### Parámetros

> | Parámetro              |  Requerido?     | Tipo de Dato      | Descripción                         |
> |-------------------|-----------|----------------|-------------------------------------|
> | `Webhook` |  Sí | string   | Webhook donde se haran las peteiciones POST con los mensaje enstrantes de la sesión        |



##### Respuesta JSON

> | Propiedad  | Descripción  | Tipo de Dato  |
> |----------|----------|----------|
> | `status`    | Estado de éxito   | string    |


</details>

------------------------------------------------------------------------------------------
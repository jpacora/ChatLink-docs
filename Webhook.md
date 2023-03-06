# ChatLink - Webhook

ChatLink le permite integrar la recepción y envío de mensajes de WhatsApp en cualquiera de sus sistemas.
- Se enviarán los datos al Webhook mediante una solicitud del tipo `POST` utilizando el formato JSON https://www.json.org .

## Mensajes

Cada solicitud hacia tu Webhook contendrá como minímo los siguientes parámetros:

| Parámetro  | Descripción  |
|----------|----------|
| idSession    | Identificador único para cada sesión de WhatsApp    |
| messageType    | Tipo de mensaje    |

Adicionalemnte, si el mensaje entrante a la sesión de WhatsApp contiene contenido multimedia (imageMessage, audioMessage, etc) se adicionará los siguientes campos:

| Parámetro  | Descripción  |
|----------|----------|
| idFile    | Identificador único para cada archivo multimedia    |
| mimetype    | Tipo del archivo    |
| caption    | Leyenda del archivo    |

## Tipos de Mensajes

<details>
	<summary>
		<code><b>sessionUpdate</b></code> <code>Información relevante a la sesión de Whatsapp</code>
	</summary>

> Este tipo de mensaje se emite cuanto sucede un evento relativo a la sesión y va acompañado del parametro `action` el cual puede contener los siguientes valores:

> | Acción  | Descripción  |
> |----------|----------|
> | connected    | Sesión conectada satisfactoriamente a los servidores de WhatsApp   |
> | loggedOut    | Sesión terminada    |
> | newQR    | Nuevo QR para la sesión    |
> | started    | Sesión iniciada    |
> | stopped    | Sesión parada    |
> | destroyed    | Sesión destruída/eliminada    |



</details>

- conversation
- imageMessage
- audioMessage
- stickerMessage
- documentMessage
- videoMessage
- contactMessage
> Estos tipos de mensajes son los entrantes para la sesión de WhatsApp los cuales tendrán los siguientes parámetros:

> | Parámetro  | Descripción  |
> |----------|----------|
> | senderNumber    | JID de la cuenta que envió el mensaje (`@s.whatsapp.net` para cuentas regulares y `@g.us` para grupos)    |
> | senderName    | Nombre de la persona que envía el mensaje    |
> | messageTimestamp    | Marca de tiempo del mensaje   |
> | isMessageFromGroup    | Indica si el mensaje proviene de un grupo    |
> | value    | Mensaje recibido (sólo en si el mensaje es del tipo `conversation`)    |


------------------------------------------------------------------------------------------


## Copyright

Copyright (c) 2023 ChatLink
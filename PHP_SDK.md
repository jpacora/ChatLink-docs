# ChatLink - SDK for PHP

## Requisitos

- PHP 5.6 o superior
- Extensiones de PHP: cURL, JSON y OpenSSL


## Configuración del Cliente

`ChatLink()` recibe en el constructor el hostname de su nodo asignado, si no se asigna ninguno la dirección del servidor por defecto será `santiago1.chatlink.redsec.network`.

```php
$client = new ChatLink();
```

Las credenciales del cliente deben configurarse antes de intentar solicitudes de API, esto se puede hacer utilizando su usuario y Password con el que se autentica en el panel de control o en su defecto utilizar un token generado desde el panel de control.

```php
// Utilizando Usuario y Password
$client->login($user, $password); // la sesión dura 2 días
// Utilizando un token
$client->setToken($token); // la sesión durará lo que se haya especificado al momento de su creación
```
## Ciclo de vida de la sesión de WhatsApp

```php
// Creamos una nueva sesión de WhatsApp
$idSession = $client->newSession();
// (OPCIONAL) Configuramos una URL donde se nos enviarán los mensajes entrantes
$client->setWebhook($idSession, $urlWebhook)
// Obtenemos los datos de la sesión para verificar el cambio de configuración
$info = $client->sessionInfo($idSession);
// Iniciamos la sesión de WhatsApp
$client->startSession($idSession);
// Obtenemos el QR en SVG para escanearlo con la apliación de WhatsApp
$client->sessionQR($idSession);
// Una vez escaneado el QR podemos enviar un mensaje
$client->sendMessage($idSession, $To, $text);
// Paramos al sesión de WhatsApp para dejar de recibir mensajes
$client->stopSession($idSession);

```

## Leer los datos enviados al Webhook

ChatLink envia información en formato JSON hacia su Webhok mediande el método POST del protocolo HTTP, para que PHP pueda pueda interpretar los datos en PHP se debe hacer lo siguiente:

```php
$json = file_get_contents('php://input');
$data = json_decode($json);
```

------------------------------------------------------------------------------------------


## Copyright

Copyright (c) 2023 ChatLink
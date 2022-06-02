# JWT: "Un token para tu seguridad"

![descarga](https://user-images.githubusercontent.com/87484792/171658838-eb16b3fb-ceaf-4897-aa57-d1351fa0a941.png)
## 

Buenas lectores! </br> Hoy vengo a hablar de *JWT* (Json Web Token), un tocken que nos ayudará a verificar la vericidad de una entidad. </br>
Como definición, podriamos decir que es un token de acceso (*estandarizado en el RFC 7519*) que permite el intercambio seguro de datos entre dos partes.
Contiene toda la información importante sobre una entidad, lo que implica que no hace falta consultar una base de datos ni que la sesión tenga que guardarse en el servidor (sesión sin estado).

Este token contiene información corta y precisa sobre el remitente, dando así información sobre sus capacidades y permisos. 
Para hacernos una idea aproximada, podriamos verlo como una cadena codificada. En él, se almacena información del usuario al que se le ha asignado esa cadena.

¡Pondré ejemplos más adelante cuando tengamos todos los datos explicados!

#
## Construcción de un JWT

Para formar un JWT necesitamos de los siguientes puntos:

`HEADER.PAYLOAD.SIGNATURE`

<h2> Header </h2>
El header consta generalmente de dos valores y proporciona información importante sobre el token. Contiene el tipo de token y el algoritmo de la firma y/o cifrado utilizados. Este podría ser un ejemplo de header de un JWT:


`{ "alg": "HS256", "typ": "JWT" }`

<h2> Payload </h2>
El campo payload de JSON Web Token contiene la información real que se transmitirá a la aplicación. Aquí se definen algunos estándares que determinan qué datos se transmiten y cómo. 
La información se proporciona como pares key/value (clave-valor); las claves se denominan "claims".

**Claims registrados:** Son Claims estandars, vienen ya configurados y dan valores como son, el emisor del token (iss, de issuer), el dominio de destino (aud, de audience) y el tiempo de vencimiento (exp, de expiration time).
</br> 

**Claims publicos:** Pueden definirse a voluntad, ya que no están sujetos a restricciones.
</br>

**Claims Privados:** Están destinados a los datos que intercambiamos especialmente con nuestras propias aplicaciones, sin claims más concretos. Por ejemplo, suelen incluir datos como identificación de usuario o nombre de departamento.

</br>

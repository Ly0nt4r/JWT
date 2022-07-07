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
Ejemplo de como se podría ver:
</br>

`{ "sub": "1", "name": "John", "exp": 50 }`

<h2> Firma </h2>

La firma de un JSON Web Token se crea utilizando la codificación Base64 del header y del payload, así como el método de firma o cifrado especificado. Para que la firma sea eficaz, es necesario utilizar unaclave secreta que solo conozca la aplicación original. Por un lado, la firma verifica que el mensaje no se ha modificado por el camino. Por otro, si el token está firmado con una clave privada, también garantiza que el remitente del JWT sea el correcto.

Existen diferentes métodos de firma, dependiendo del nivel de confidencialidad de los datos:

**Sin protección**: como hemos mencionado, si los datos no requieren un nivel de protección alto, puede especificarse el valor none en el header. En este caso, no se genera ninguna firma y el JWT solo constará de header y payload. Sin esta medida de protección, el payload puede leerse como texto en claro una vez descifrado el código Base64 y no se comprueba si el mensaje procede del remitente correcto o si fue modificado al transferirse.

**Firma (JWS)**: por lo general, basta con comprobar si los datos provienen del remitente correcto y si han sido modificados. Para ello, se utiliza el esquema JSON Web Signature (JWS), que garantiza que el mensaje no se haya cambiado por el camino y proceda del remitente correcto. Con este procedimiento, el payload también puede leerse como texto en claro tras el descifrado de Base64.

**Firma (JWS) y cifrado (JWE)**: además de JWS, es posible emplear JSON Web Encryption (JWE). JWE cifra el contenido del payload, que luego se firma con JWS. Para descifrar el contenido, se indica una contraseña común o una clave privada. De este modo, el remitente se verifica, el mensaje es confidencial y se autentifica, y el payload no puede leerse como texto en claro tras el descifrado de Base64.
El cifrado crea una secuencia de caracteres aparentemente aleatoria:

`{ 7WK5T79u5mIzjIXXi2oI9Fglmgivv7RAJ7izyj9tUyQ }`
##
<h2> ¿Cómo funciona un JSON Web Token?</h2>
El inicio de sesión de usuario ejemplifica bien la función del JSON Web Token. Antes de utilizar el JWT, hay que establecer una clave secreta. Una vez que el usuario ha introducido correctamente sus credenciales, el JWT se devuelve con la clave y se guarda localmente.

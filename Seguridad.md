# Estandares de Seguridad
Seguridad de la información es la preservación de la confidencialidad, integridad y disponibilidad de la información; también pueden estar involucradas otras propiedades como la autenticidad, responsabilidad, no repudio y confiabilidad.

## Índice
* [Seguridad en la Capa de Transporte](#seguridad-en-la-capa-de-transporte)
    * [TLS (Transport Layer Security o Seguridad de la Capa de Transporte)](#tls-transport-layer-security-o-seguridad-de-la-capa-de-transporte)
    * [VPN (Virtual Private Network o Red Privada Virtual)](#vpn-virtual-private-network-o-red-privada-virtual)
    * [Recomendaciones Generales](#recomendaciones-generales)
* [Seguridad de los Datos](#seguridad-de-los-datos)
    * [Autenticación y Autorización](#autenticación-y-autorización)
        * [Autenticación Básica (Basic auth)](#autenticación-básica-basic-auth)
        * [Autenticación con Certificados Electrónicos](#autenticación-con-certificados-electrónicos)
        * [Autenticación con JWT (JSON Web Tokens)](#autenticación-con-jwt-json-web-tokens)
        * [Autenticación y Autorización con OAuth (OAuth 1.0a y OAuth2)](#autenticación-y-autorización-con-oauth-oauth-10a-y-oauth2)
        * [Autenticación y Autorización con OpenID Connect](#autenticación-y-autorización-con-openid-connect)
        * [Recomendaciones Generales](#recomendaciones-generales-1)
    * [Integridad](#integridad)
        * [Registro Centralizado de Hashes](#registro-centralizado-de-hashes)
        * [Firma Electrónica](#firma-electrónica)
        * [Sellado de Tiempo](#sellado-de-tiempo)
        * [Cadena de Bloques (Blockchain)](#cadena-de-bloques-blockchain)
        * [Recomendaciones Generales](#recomendaciones-generales-2)
    * [Confidencialidad](#confidencialidad)
        * [Cifrado Simétrico](#cifrado-simétrico)
        * [Cifrado Asimétrico](#cifrado-asimétrico)
        * [Recomendaciones Generales](#recomendaciones-generales-3)
    * [Auditoría](#auditoría)


## Seguridad en la Capa de Transporte.

Es necesario contar con protocolos de seguridad en el canal o medio por el cual se transmitirá la información, esto para evitar que ajenos puedan verla o modificarla. Existen diversas tecnologías para este fin, como ser:
 
### TLS (Transport Layer Security o Seguridad de la Capa de Transporte).

El protocolo TLS permite la identificación y autenticación de las instituciones a nivel del protocolo de transporte, consiguiendo que la comunicación sea confidencial y que la información enviada y/o recibida esté íntegra.

Este protocolo provee un medio seguro para comunicarse, siendo su principal propósito la confidencialidad de la información transferida. La integridad de la información intercambiada se logra autenticando los mensajes en cada transmisión.

Es recomendable siempre utilizar TLS en procesos de interoperabilidad que requieren algún tipo de autenticación y/o confidencialidad, ya sea con claves obtenidas de una institución certificadora o con claves autogeneradas, dado que su implementación en general es sencilla de realizar, comparada con otras tecnologías.
 
### VPN (Virtual Private Network o Red Privada Virtual).
 
Una VPN es un canal privado cifrado de comunicación. Se trata de un ambiente de comunicaciones donde el ingreso es restringido y habilitado solo para las partes que quieren comunicarse; es decir, que el canal no puede ser visto ni entendido por ajenos.
 
Una VPN ofrece un canal seguro de transmisión sobre una red no segura, con las siguientes propiedades: confidencialidad, integridad y autenticación. Todas estas propiedades son añadidas a la seguridad propia del servicio web (el servicio web podría tener autenticación y autorización).

Esta tecnología se utiliza cuando se requiere transmitir información sensible, dado que al existir diversas tecnologías para la implementación de VPNs, la conexión entre productos de distintos proveedores suele ser compleja. 

Es posible crear una VPN usando mecanismos que operan en las primeras capasa del modelo OSI tales como IPSEC. Estos túneles permiten encapsular y conectar de dos redes físicamente separadas.  
A veces resulta innecesario o impráctico conectar dos redes, especialmente si solo necesitamos compartir un servicio web entre instituciones. En el caso más común un servicio web puede ser protegido y encapsulado usando identificación mutua TLS. 

Por último, MPLS es una tecnología de etiquetado de tráfico que permite crear canales privados en una red pública sin cifrar los datos, por lo que es indispensable utilizar TLS.
 
### Recomendaciones Generales.
Se recomienda siempre usar TLS para proteger y compartir servicios Web. Sin embargo si los datos necesitan un mayor grado de seguridad en el transporte, y es deseable tener dos redes conectadas entre instituciones, se puede utilizar una VPN (IPSec).
 
Es importante tomar en cuenta que el uso de estas tecnologías no es exclusivo, es decir que se puede utilizar una túnel TLS dentro de un canal VPN/IPSEC.

 
## Seguridad de los Datos.
 
### Autenticación y Autorización.

Al publicar datos a través de un servicio web es necesario identificar quién puede acceder al servicio, salvo en los servicios web que son de acceso público. La autenticación es la verificación de la institución de la institución consumidora, mientras que la autorización es la verificación de los permisos que tiene dicha institución sobre un recurso específico.

Siempre se debe realizar primero la autenticación y luego la autorización. Esto debe verificarse en cada petición de la institución consumidora hacia el servicio.
 
La autenticación y autorización pueden efectuarse de diversas maneras, a continuación se detallan las principales:
 
#### Autenticación Básica (Basic auth).

La autenticación básica es el método más simple y utiliza un usuario y contraseña para identificar a la institución consumidora.

Se recomienda usar este tipo de autenticación en los servicios web cuando los datos que se quiere intercambiar no tengan muchas restricciones de uso. Además, este tipo de autenticación permitirá identificar mínimamente el usuario de la institución consumidora. Cabe destacar que este tipo de autenticación puede ser utilizado tanto con un tipo de servicio web REST como SOAP.
 
Es recomendable implementar procedimientos de uso y ciclo de vida de las contraseñas.
 
#### Autenticación con Certificados Electrónicos.

La autenticación por medio de certificados se realiza solicitando el certificado digital del consumidor del servicio web (cliente) y verificando cada mensaje enviado contra dicho certificado, lo que garantiza que el consumidor del servicio es quien dice ser.

Si bien es posible realizar la autenticación por este medio, la administración de certificados para un servicio web con una gran cantidad de clientes es compleja, por lo que no se recomienda su uso existiendo otros medios de autenticación más sencillos e igualmente seguros.

Si se va a implementar la autenticación con certificados digitales, es necesario comprobar que el certificado haya sido entregado por una Autoridad Certificadora, que no haya expirado y no haya sido revocado.
 
#### Autenticación con JWT (JSON Web Tokens).
 
JWT es el medio principal de autenticación en servicios de tipo REST, es un medio compacto y autocontenido para enviar datos de manera segura entre las partes en formato JSON.

Un JWT puede ser firmado tanto con un algoritmo simétrico como uno asimétrico.

Los JWT consisten de tres partes separadas por puntos (.), las cuales son: cabecera (header), cuerpo (payload) y la firma (signature).
 
Se debe considerar el cifrado de los datos del cuerpo si estos se consideran sensibles, véase el punto (Confidencialidad).

Por su facilidad de implementación al trabajar con un servicio REST, se recomienda siempre utilizar JWT, sin olvidar que muchas veces es necesario revocar un token, por lo cual se sugiere que como mínimo esta implementación soporte la revocación además del tiempo de expiración del JWT.
 
#### Autenticación y Autorización con OAuth (OAuth 1.0a y OAuth2).

Existen dos versiones: OAuth 1.0a y OAuth2, siendo esta última la más utilizada.

OAuth2 es un protocolo de autorización y la manera de realizar la autenticación va más allá del alcance de la especificación, por lo que se puede implementar el proceso de autenticación que se desee. Una gran mayoría de las implementaciones del estándar ya ofrecen mecanismos de autenticación.

En OAuth2 existen varios roles: el cliente (o la aplicación que intenta tener acceso a la información del usuario), el servidor de recursos, el servidor de autorización (es el que pregunta al usuario si realmente quiere dar los permisos al cliente) y el usuario. Existen, además varios flujos o maneras para obtener un token, las principales son:
 
Otorgamiento de credenciales de cliente (Client Credentials Grant): Este método se utiliza comúnmente para comunicaciones de servidor a servidor, el cliente envía sus credenciales al servidor de autorización y este retorna un token firmado (el cliente y el usuario son los mismos).
Otorgamiento de código de autorización (Authorization Code Grant): Usado comúnmente en aplicaciones web cuando el cliente quiere acceder a recursos protegidos en favor del usuario. 

El flujo es el siguiente: el cliente redirecciona al usuario al servidor de autorización; entonces se solicita al usuario ingresar sus credenciales en el servidor de autorización y aprobar la solicitud del cliente; luego el cliente —con el permiso que ya dio el usuario—, negocia un token de acceso con el servidor de autorización (es una llamada en favor de un usuario, el usuario y el cliente son distintos).

OAuth resulta complejo en su implementación; sin embargo, destaca cuando se espera contar con una gran cantidad de servicios web, ya que al tratarse de un servicio centralizado, su administración resulta más sencilla de aplicar transversalmente.
Qué flujo de autorización se debe usar: 
![alt text](https://alexbilbie.com/images/oauth-grants.svg "Selección de flujo de Autorización")

*Fuente: alexbilbie.com *

#### Autenticación y Autorización con OpenID Connect

OpenID Connect (OIDC) es un protocolo que aumenta al protocolo OAuth2 agrgando datos de identidad del usuario a través de tokens firmados JWT; esto le permite ofrecer tanto autenticación como autorización, por lo que se considera más completo.

OpenID Connect se basa en el concepto de institución, que se define como un conjunto de atributos que identifican a los usuarios de forma exclusiva y que permite a las aplicaciones cliente confiar en la autenticación realizada por un proveedor de OpenID Connect para verificar la institución de un usuario.

OpenID Connect utiliza mensajes JSON sobre HTTPS y se recomienda su uso sobre versiones anteriores de OpenID que se marcaron como obsoletas. Más detalles sobre el estándard estan [disponibles en este enlace](http://openid.net/connect/faq/)
 
#### Recomendaciones Generales.

Si la institución carece de un mecanismo de autenticación y autorización ya definido, se recomienda utilizar JWT para servicios REST y BASIC para SOAP.
 
Si la institución ya cuenta con un mecanismo de autenticación y autorización, se recomienda mantener este mecanismo y solo realizar acciones de documentación y respaldo de su funcionamiento. 

Se recomienda la implementación de OAuth2 u OpenID Connect a mediano o largo plazo. 

Se sugiere utilizar un solo mecanismo de autenticación y autorización, esto para evitar complejidad administrativa en el largo plazo.

Es necesario asegurarse que a las funciones administrativas de autenticación y autorización del servicio web solamente puedan acceder administradores del servicio y no así consumidores.
 
Para REST se sugiere implementar un Administrador de APIs (Api Gateway). Esto posibilita aplicarlo transversalmente a todos los servicios web (tanto la autenticación como la autorización), además de que provee otros mecanismos de control como listas de acceso, logs, límite de solicitudes, etc. Dependiendo de la herramienta que se utilice, las características pueden variar, sin embargo se sugiere el uso de Kong por ser una herramienta completa.

Si la naturaleza del servicio es transaccional, se recomienda necesariamente aplicar un mecanismo de autorización.

Se recomienda realizar un inventario de vulnerabilidades técnicas respecto a la implementación del tipo de autenticación y autorización adoptada previo al despliegue en producción. Estas vulnerabilidades pueden corresponder al tipo de cifrado que se utilice, manejo de contraseñas entre otras.

### Integridad.

Usualmente los mismos protocolos de transmisión de datos otorgan integridad pero sólo en el nivel de transporte, esto no siempre es suficiente al implementar un servicio web, ya que sólo se garantiza que la información no haya sido alterada en el canal, aunque luego puede haber sido alterada por otros procesos.
 
Los servicios web deben garantizar la “exactitud” y “completitud” de los datos utilizando mecanismos como la Firma Electrónica, que evitan la alteración de los datos tanto en el canal como en el lugar donde se procesarán o almacenarán.

A continuación se detallan los mecanismos que nos garantizan la integridad de los datos: 

#### Registro Centralizado de Hashes.
 
Se puede utilizar una base de datos centralizada para garantizar la integridad de los mensajes. Esto se realiza distribuyendo un resumen (hash) de los datos intercambiados a una base de datos de confianza donde se almacenan. Junto con estos resúmenes se almacena el tiempo (timestamp) a fin de verificar el momento en que se haya efectuado una solicitud.

Es necesario que esta base de datos sea accesible para las instituciones participantes, de tal forma que cada una pueda obtener un respaldo de la misma, si así lo deseara.
 
Este medio de verificación de la integridad se utilizará solamente si las instituciones que requieren intercambiar datos establecen un acuerdo entre ellas, donde aceptan la validez de dicho registro.
 
#### Firma Electrónica.
 
La Firma Electrónica asocia al firmante con un documento (un mensaje en interoperabilidad) brindando autenticidad, integridad y no repudio.
 
La Firma Electrónica es parte de una infraestructura denominada PKI que permite identificar un certificado digital con la institución de una persona o institución. Con este mecanismo es posible verificar si la información ha sido modificada, incluso si solamente se hubiera cambiado un carácter.
 
Es posible incluso tener una infraestructura PKI propia, si todas las instituciones que intervienen aceptan su validez.
 
Para realizar la interoperabilidad entre las partes es necesario que estas intercambien las claves públicas, manteniendo las claves privadas en lugar seguro (esto solo si son certificados autofirmados, ya que si los certificados son generados por una institución Certificadora Pública, esta se encarga de verificar las claves).
 
Los certificados para realizar la Firma Electrónica entre servidores se pueden obtener de varias maneras. A continuación detallamos las más utilizadas:
 
Con una institución Certificadora Pública (CA o Certificate Authority): institución a la cual se acude para obtener certificados digitales para utilizarlos en el intercambio de datos.
Con Certificados Autofirmados: en este caso, los certificados son generados por las instituciones que desean intercambiar datos. El intercambio de las claves públicas puede efectuarse por cualquier método entre las partes; sin embargo, para darle un carácter legal, el intercambio de claves puede realizarse ante un notario de fe pública.

#### Sellado de Tiempo.

El sellado de tiempo se utiliza para especificar el momento en el cual se ha aplicado la Firma Electrónica. Usualmente el sellado de tiempo es parte de la infraestructura PKI y a la autoridad de sellado de tiempo se le denomina TSA (Time Stamping Authority).

El sellado de tiempo indica que los contenidos firmados digitalmente existieron en un momento dado y que no han cambiado desde ese instante. Sin la existencia de sellado de tiempo, no es posible saber cuándo se ha utilizado la Firma Electrónica o si ésta ha sido aplicada con un certificado válido en el momento del firmado.
 
Se sugiere usar el sellado de tiempo en conjunto con la Firma Electrónica, ya que permite saber cuándo se ha efectuado la firma de los datos, si se ha realizado con una clave válida o si la información es reciente.

#### Cadena de Bloques (Blockchain).

La cadena de bloques es un registro público en orden cronológico de las transacciones que se realizan. Esta cadena se comparte entre los usuarios, lo que permite verificar que un evento ha ocurrido, garantizando la integridad. En otras palabras, es un registro de transacciones descentralizado y distribuido, donde cada cliente puede tener su propia copia, lo cual evita modificaciones por parte de terceros.
 
En interoperabilidad se podría utilizar generando un resumen (hash) del mensaje que contenga los datos a intercambiar e insertando este resumen en la cadena de bloques, que al ser distribuida es muy difícil de alterar.
 
#### Recomendaciones Generales.

Se recomienda el uso de la Firma Electrónica en todos los servicios web que intercambien datos sensibles, tomando en cuenta la complejidad que esto implica.
 
Si se va a utilizar la Firma Electrónica es conveniente establecer mecanismos seguros para el intercambio de las claves públicas entre las instituciones (si fuera necesario) y el almacenamiento de las claves privadas en lugar seguro, garantizando así la integridad de los datos y evitando que estas claves se pierdan en caso de alguna eventualidad. Además es necesario verificar que los certificados no hayan expirado y que no hayan sido revocados.
 
En SOAP se sugiere utilizar un XML Signature de acuerdo a la W3C o WS-Security; en REST, el RFC 7515 de JWS (JSON Web Signature) para la firma de JSON.
 
### Confidencialidad.
 
Cuando los datos fluyen de un lado a otro, muchas veces a través de varios intermediarios, se debe evitar que sean entendidos por terceros; más aún, es necesario que dichos datos no sean entendibles por administradores de la infraestructura y otros con acceso al mismo servicio web. El método más común para mantener la confidencialidad de los datos es el cifrado.

El cifrado es el proceso de convertir los datos a un formato no legible por ajenos no autorizados (terceros que observen el canal de transmisión, administradores del servicio web u otros). Los datos solamente puede ser entendidos por aquellos que posean la clave para descifrarlos.
 
Los métodos utilizados para el cifrado son el simétrico y el asimétrico, que detallamos a continuación:
 
#### Cifrado Simétrico.
 
El cifrado simétrico se realiza con una clave secreta y es seguro siempre que dicha clave sea mantenida en buen resguardo. En interoperabilidad, basta que las partes intercambien la clave de manera segura para establecer una comunicación con un nivel aceptable de cifrado y a un costo computacional bastante bajo (tiempo de procesamiento).
 
El algoritmo más utilizado para realizar el cifrado simétrico es AES (Advanced Encryption Standard o estándar avanzado de cifrado), que es bastante eficiente y al procesarse consume pocos recursos. Puede utilizarse con claves de longitud 128, 192, 256 o de una mayor cantidad de bits, siendo la mayor diferencia entre estas el tiempo que toma descifrar los datos.

Una de las principales desventajas de este tipo de cifrado es el intercambio de la clave, que se convierte en un riesgo cuando deja de ser secreta (cualquiera en posesión de la clave puede descifrar los datos).
 
#### Cifrado Asimétrico.

El cifrado asimétrico usa dos claves: una para el cifrado y otra para el descifrado. Se utiliza una clave pública para aplicar el cifrado y una clave privada para descifrar los datos (solamente se puede realizar el descifrado de los datos con la clave privada).
 
En este tipo de cifrado no existe la necesidad de realizar el intercambio de claves, evitando el problema de distribución de claves.
 
Se recomienda el uso de RSA con una clave de longitud mínima de 2048.
  
#### Recomendaciones Generales.

En ningún caso es recomendable implementar un algoritmo de cifrado propio.
 
Se recomienda utilizar un cifrado simétrico siempre que no se encuentre sobre un canal seguro (TLS o VPN) para evitar que terceros puedan entender los datos enviados.
 
También se recomienda utilizar el cifrado asimétrico si los datos que se quieren intercambiar son sensibles y solamente pueden ser conocidos por usuarios específicos.
 
En general, si se requiere de mayor seguridad para los datos, se sugiere usar el cifrado asimétrico.
  
### Auditoría.

La auditoría es la revisión y comprobación de las acciones realizadas para reconstruir una serie de eventos que generaron un hecho específico. La manera más común para efectuar estas auditorías es a través de registros de eventos (logs) en servidores seguros y solamente accesibles por personal autorizado.
 
Se recomienda utilizar siempre los registros de eventos con toda la información posible. En este marco, lo mínimo que deberían contener son: información temporal, información de la aplicación que está realizando el registro del evento, quién realizó el evento (datos del cliente), el tipo de evento que se haya realizado y la solicitud y respuesta del servicio.
 
No se debe incluir en los registros de eventos información sensible del cliente (contraseña por ejemplo), rutas a archivos o cadenas de conexión a la base de datos, ya que esto constituye un riesgo de seguridad.

Se debe documentar en informes las acciones correctivas que se tomaron en caso de cualquier suceso que haya afectado al servicio, con la finalidad de que si los mismos sucesos se repitieran, estos se resuelvan fácilmente.
 
Se recomienda utilizar un centralizador de registros de eventos para facilitar su administración y posterior análisis (ELK, Apache Kafka u otro).

También se puede realizar la auditoría con el registro centralizado de hashes en caso de haberse implementado este mecanismo; véase el punto (Registro centralizado de hashes).
 
Además, se pueden utilizar tecnologías de sincronización de relojes de sistemas (NTP, Network Time Protocol) con la finalidad de posibilitar un seguimiento cronológico de los eventos.



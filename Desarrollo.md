# Estandares de Desarrollo de Servicios Web

Con base a estándares y mejores prácticas utilizadas a nivel internacional se sugiere la utilización de los siguientes lineamientos para la construcción de servicios web.

## Índice

* [Definición de Parámetros de Entrada/Salida](#definición-de-parámetros-de-entradasalida)
* [Buenas Prácticas](#buenas-prácticas)
* [Validación de Mensajes](#validación-de-mensajes)
* [Versionamiento](#versionamiento)
* [Manejo de Errores](#manejo-de-errores)
* [Codificación](#codificación)
* [Zona Horaria](#zona-horaria)
* [Ficha del Servicio](#ficha-del-servicio)
* [Anexos](#anexos)
    * [Tipos de formatos de representación de datos](#tipos-de-formatos-de-representación-de-datos)
        * [JSON (JavaScript Object Notation o Notación de Objetos JavaScript)](#json-javascript-object-notation-o-notación-de-objetos-javascript)
        * [XML (eXtensible Markup Language o Lenguaje de Marcado Extensible)](#xml-extensible-markup-language-o-lenguaje-de-marcado-extensible)
    * [Tipos de Servicios Web](#tipos-de-servicios-web)
        * [REST](#rest)
            * [Buenas Prácticas](#buenas-prácticas-1)
            * [Validación de Mensaje](#validación-de-mensajes-1)
            * [Versionamiento](#versionamiento-1)
            * [Manejo de Errores](#manejo-de-errores-1)
            * [Codificación](#codificación-1)  
        * [SOAP](#soap)
            * [Buenas Prácticas](#buenas-prácticas-2)
            * [Validación de Mensajes](#validación-de-mensajes-2)
            * [Versionamiento](#versionamiento-2)
            * [Manejo de Errores](#manejo-de-errores-2)
            * [Codificación](#codificación-2)
    * [Códigos de Respuesta HTTP](#códigos-de-respuesta-http)
* [Referencias](#referencias)


## Definición de Parámetros de Entrada/Salida.

Es recomendable que la institución establezca los parámetros de entrada y salida del servicio de acuerdo a su naturaleza. Cada parámetro será definido claramente y describirá su propósito; esta definición facilitará, posteriormente, la generación de la documentación respectiva.

## Buenas Prácticas.

Al momento de implementar un servicio web es importante tomar en cuenta experiencias de implementación con resultados positivos que ayuden a mejorar o solucionar problemas al poner en funcionamiento los servicios. La sistematización de estas experiencias es lo que se denomina una buena práctica.

Se recomienda ser consistentes en la implementación de servicios web, manteniendo las buenas prácticas en todos los servicios de acuerdo a la tecnología utilizada.

## Validación de Mensajes.

La validación de los mensajes se realiza para verificar que la estructura de los objetos que se utilizan en el servicio web sea la correcta.

Validar los mensajes evita problemas de funcionamiento no previstos cuando los clientes consumen el servicio.

Se recomienda validar la estructura de los mensajes, tanto de los parámetros de entrada como los de salida.

## Versionamiento.

En ocasiones es necesario tener varias versiones de un mismo servicio. Esto puede ocurrir cuando el servicio presenta nuevas características de funcionamiento (o en el caso de necesitar otros parámetros de entrada/salida).

Se recomienda siempre versionar los servicios web para evitar inconvenientes a los consumidores que ya usan el servicio. El versionamiento debe considerarse desde el inicio de la implementación.

Los cambios o modificaciones entre versiones se documentan y se publican de acuerdo a lo establecido en su Documentación.

## Manejo de Errores.

Todos los problemas que presenten los servicios web deben ser identificados, de modo que la institución consumidora de los mismos interprete los motivos de las fallas.

Se recomienda que el mensaje de error tenga como mínimo un código y una descripción que permita comprenderlo de manera clara.

## Codificación.

Las instituciones que participen en el intercambio de datos de un servicio web (aún si estuviera en otro idioma) tienen que interpretar de la misma manera los caracteres utilizados para la transmisión de mensajes.

Por este motivo, se recomienda siempre utilizar la codificación (encoding) UTF-8 en todos los servicios web.

## Zona Horaria.

Se recomienda que todos los servicios web de interoperabilidad utilicen la misma zona horaria, esto con el fin de que todas las instituciones conciban los tiempos de la misma manera. Para nuestro caso GMT-6.

## Ficha del Servicio.

Es necesario documentar los servicios ofrecidos por cada institución. Para cada servicio de debe detallar datos como url para realizar el consumo, parámetros de entrada y datos de salida.

| | Información Técnica | |
| ------------ | ------------- | ------------- |
| Dirección Física del Servicio | URL de consumo del servicio | |
| Tipo | Tecnología  utilizada  para  la  obtención  de  la información del servicio (SOAP, REST u otro) | Requerido |
| Entorno |Entorno de desarrollo, pruebas, producción u otro | Requerido |
| Datos de Entrada | Detalle de los parámetros o modificadores de entrada del servicio | Requerido |
| Datos de Salida | Detalle de la estructura de respuesta del servicio | Requerido |
| Tipo de Conexión | Medio  por  el  cual  se  transmiten  los  datos  del proveedor al cliente | Requerido |
| Software Relacionado | Vínculos de software relacionado al servicio | |

## Anexos.

### Tipos de formatos de representación de datos.

Los principales tipos de formatos de datos de representación de la información en un servicio de interoperabilidad son JSON y XML, y se detallan a continuación:


#### JSON (JavaScript Object Notation o Notación de Objetos JavaScript).

Es un formato de representación de datos liviano, simple de ser leído y entendido tanto por humanos como por máquinas. Es el principal tipo de formato de dato para el intercambio de información en un servicio de interoperabilidad REST y, en su forma más simple, se caracteriza por el uso de una colección de pares nombre/valor que podrían ser anidados. A continuación se observa su estructura:
```
{
    "nombre1": "valor1", // par nombre valor
    "nombre2": "valor2",
    "nombre3": {
        "nombre4": "valor4",
        "nombre5": ["val1", "val2"] // par nombre valor, donde el valor es una colección (array)
    }
}
```

Como ejemplo se describe el objeto “persona” en formato JSON:
```json
{
    "dui": "12345678-9",
    "nombres": "Juan",
    "apellidos": "Perez Gomez",
    "fechaNacimiento": "22/05/2017"
}
```

#### XML (eXtensible Markup Language o Lenguaje de Marcado Extensible).

Es un formato de representación de datos flexible que define un conjunto de reglas para formar documentos que puedan ser entendibles por humanos y por máquinas. Este formato de tipo de dato se utiliza generalmente con servicios de interoperabilidad SOAP, aunque también es posible utilizarlo con un servicio de interoperabilidad REST.

La estructura del documento XML tiene que contener la declaración <xml> que especifique la versión (version) y la codificación (encoding) del documento, esto con el fin de mejorar la interoperabilidad de los datos (al conocer la versión y la codificación se evitan errores de interpretación).

Como ejemplo se detalla el objeto “persona” en formato XML:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<persona>
    <dui>012345678-9</dui>
    <nombres>Juan</nombres>
    <apellidos>Perez Gomez</apellidos>
    <fechaNacimiento>22/05/2017</fechaNacimiento>
</persona>
```

### Tipos de Servicios Web.

Al momento de la redacción del documento los tipos de servicios web más utilizados al implementar un proceso de interoperabilidad son REST y SOAP. A continuación se exponen las definiciones y características principales de cada uno:

#### REST.

REST es un estilo de arquitectura para sistemas distribuidos y, si bien no depende de ningún protocolo, en su gran mayoría se utiliza sobre HTTP (Hypertext Transfer Protocol).
Este estilo de arquitectura define un conjunto de principios para su implementación:
* Interfaz uniforme. Todos los recursos son identificados por una URI (Uniform Resource Identifier).
* Interacciones sin almacenamiento del estado (stateless). Cada mensaje tiene información suficiente para ser procesado sin necesidad de guardar un estado en el servidor de anteriores mensajes.
* Permite el uso de caché. Las respuestas pueden ser cacheadas o no por el cliente para optimizar las consultas.
* Es una arquitectura cliente-servidor. El servidor desconoce los clientes que se conectarán al mismo. Ambos lados pueden desarrollarse independientemente.
* Arquitectura por capas. El cliente desconoce si está conectado directamente al servicio, a una caché o a cualquier otra capa intermedia.

El servicio basado en estos principios se denomina RESTful.

Si bien técnicamente un servicio REST puede transferir la información en cualquier formato, se recomienda utilizar JSON para el intercambio de datos.

##### Buenas Prácticas.

Para mantener la consistencia en el desarrollo de los servicios REST, se sugiere implementar las siguientes buenas prácticas:
* Contar con manejo de respuestas de tipo JSON por defecto, y solo en caso de necesidad, otro tipo de contenido (XML, CSV u otro)
* Los URI (Uniform Resource Identifier) son nombres o sustantivos en plural y en minúscula para todos los recursos; esto porque el protocolo HTTP ya maneja los verbos que corresponden a las acciones de CRUD (POST, PUT, PATCH, GET, u otros).
* Usar la notación “camello” (camelCase), que es la práctica de escribir frases compuestas de manera que cada palabra en medio de la frase comience con una letra mayúscula (por ejemplo, fraseEnCamelCase). Utilizar esta notación para nombrar recursos, atributos y parámetros.
* Aprovechar la naturaleza jerárquica de la URL siempre que un objeto tenga relación con otro.

**Listar elementos**

Al consumir este recurso y no agregar un filtro de búsqueda a la URL, el servicio debe de listar tódos los elementos pertenecientes al recurso que se esta consumiendo. Para no sobrecargar la obtención de los elementos se puede limitar el resultado agregando una paginación por defecto al servicio, la cual puede ser modificada a través de filtros en la URL.

```
GET /servicios 
# HTTP 200 OK
```

**Filtrar lista de elementos**

Usar el símbolo "?" para filtrar los recursos y "&" para añadir más filtros en el URL.
```
GET /servicios?{filtro1}=valor&{filtroN}=valor

# Filtrando por el id de la Entidad y su estado
GET /servicios?idEntidad=2345&estado=pendiente

# HTTP 200 OK
```

**Consultar un elemento**

La consulta a un elemento específico debe de realizarse enviando a través de la URL el parámetro que servirá como llave o identificador del elemento a consultar y ningun otro parámetro de filtro, paginación u ordenamiento.

```
GET /servicios/{id}

# Obteniendo el elemento 12345 del servicio
GET /servicio/12345

# HTTP 200 OK
```

**Paginación**

Para las paginaciones (en caso de listas con una cantidad alta de datos) se sugiere contar con los parámetros “pagina” (numero de página del primer elemento a devolver por el recurso) y "elementosPorPagina" (cantidad de datos a devolver por página por el recurso)  en el URL.

```
# Obteniendo los registros del 61 - 90 (elementosPorPagina=30 por defecto)
GET /servicio?pagina=3
# HTTP 200 OK

# Obteniendo los registros del 21 - 30
GET /servicio?pagina=3&elementosPorPagina=10
# HTTP 200 OK
```

Si se utiliza paginación se debe establecer un número de **elementosPorPagina** por defecto (el número normalmente utilizado es de 30 elementos)

Además, se sugiere enviar opcionalmente en la respuesta el header link con información referente a la paginación ("first" la primera página, "prev" la página anterior, "next" la siguiente página y "last" la última página).

```html
Link: <https://miempresa.gob.sv/servicio?limite=20&intervalo=0>;rel="first", 
      <https://miempresa.gob.sv/servicio?limite=20&intervalo=40>;rel="prev", 
      <https://miempresa.gob.sv/servicio?limite=20&intervalo=80>;rel="next",
      <https://miempresa.gob.sv/servicio?limite=20&intervalo=180>;rel="last"
```

**Ordenamiento**

Para ordenar los recursos se utiliza el parámetro "orden" seguido del nombre de elemento por el cuál se desea ordenar; por defecto los recursos están ordenados ascendentemente. Los elementos por los cuales se es permitido ordenar deberá estar definido en la documentaicón técnica de recurso de la API.

```
GET /servicio?orden[elemento1]=asc|desc&orden[elementoN]=asc|desc

# Ordenando por estado Ascendente y fechaRegistro descendente
GET /servicio?orden[estado]=asc&[fechaRegistro]=desc

# HTTP 200 OK
```

**Límite de Consultas**

En el caso de manejar un límite de solicitudes por cliente (rate-limiting), es necesario enviar en la respuesta una cabecera (header) HTTP extra, con información de la cantidad de solicitudes permitidas, la cantidad de solicitudes restantes y el tiempo (timestamp) en el cual estos límites volverán a su estado inicial.

```
X-LimiteSolicitudes-Limite: 100
X-LimiteSolicitudes-Restante: 14
X-LimiteSolicitudes-Reset: 1499875025
```

**Creación de un elmento**

La creación de un elemento implica el envio de un registro o un conjunto de estos que cumplan con los lineamientos establecidos en la documentación Técnica de la API a la cual se le esta solicitando dicha acción. El registro viaja a través del cuerpo de la petición y se recomienda el uso del formato JSON para los valores de entrada.

```
POST /servicios

# Cuerpo de la petición
[{
    "nombre": "Nombre",
    "descripcion": "Descripcion del registro"
}]

# HTTP 201 CREATED
```

Para la validación de los datos de entrada se recomienda el uso de [json-schema](http://json-schema.org/). En el caso del método POST el envío de los registros a crear deberán de estar dentro de un array ya sea que se cree uno o más elementos.

**Modificación de un elemento**

Las modificaciones de los registros se pueden realizar a través de los protocolos PUT o PATCH, la diferencia entre estos es que PUT actualiza todos los campos del registro, mientras que PATCH permite actualizar uno o mas campos del registro. Para poder realizar la actualización es necesario brindar la llave o identificador del registro a modificar a través de la URL.

**PUT**

```
PUT /servicio/{id}

# Cuerpo de la petición
{
    "nombre": "Nombre",
    "descripcion": "Descripcion del registro"
}

# HTTP 200 OK
```

**PATCH**

```
PATCH /servicio/{id}

# Cuerpo de la petición
{
    "descripcion": "Descripcion del registro"
}

# HTTP 200 OK
```

Para la validación de los datos de entrada se recomienda el uso de [json-schema](http://json-schema.org/).

**Eliminación de un elemento**

Para la eliminación de un registro es necesario brindar la llave o identificador del registro a modificar a través de la URL.

```
DELETE /servicio/{id}

# HTTP 204 NO CONTENT
```

Utilizar los [códigos HTTP](#códigos-respuesta-http) correspondientes para responder a las consultas realizadas por el cliente.

Considerar el cifrado de los parámetros enviados en el URI si estos fueran de alguna manera sensibles.

##### Validación de Mensajes

Utilizar JSON Schema para validación de mensajes en REST de acuerdo a lo descrito por la IETF16.

JSON Schema está descrita también en formato JSON; sin embargo, se utiliza para describir la estructura de otros datos. En su núcleo, JSON Schema define los siguientes tipos básicos de datos:
* string: que se utiliza para cadenas de texto.
* number o integer: se utilizan para definir valores numéricos, siendo la principal diferencia que “number” acepta tanto números enteros como números decimales, mientras que “integer” se usa solamente para validar números enteros.
* object: se utiliza para validar estructuras JSON anidadas (una estructura dentro de otra).
* array: se usa para definir un conjunto de elementos.
* boolean: este tipo de dato se utiliza para verificar dos valores especiales, true (valor verdadero) y false (valor falso).
* null: este valor especial se utiliza generalmente para representar la ausencia de un valor.

Se recomienda que cada objeto identificado en la semántica tenga asociado y publicado su JSON Schema respectivo.

Por ejemplo, para validar la estructura JSON utilizar:
```json
{
    "title": "Persona",
    "type": "object",
    "properties": {
        "dui": {
            "type": "integer"
        },
        "nombres": {
            "type": "string"
        },
        "apellidos": {
            "type": "string"
        },
        "fechaNacimiento": {
            "type": "string"
        }
    }
}
```
Herramientas de desarrollo de JSON Schema: 

* Ejmeplos de esquemas: http://json-schema.org/examples.html
* Validador de esquema en línea: https://www.jsonschemavalidator.net/
* Validación de JSON Schema para Java, Python, PHP, Ruby, etc.: http://json-schema.org/implementations.html#validators

##### Versionamiento.

El versionamiento se aplica en la URL. Se podrán tener hasta dos versiones al mismo tiempo.
```
GET /v1/servicios
GET /v2/servicios
```

##### Manejo de Errores.

Todos los problemas que presenten los servicios de interoperabilidad deben ser identificados, de modo que la entidad consumidora de los mismos comprenda los motivos de las fallas.

Para el manejo de errores, se recomienda utilizar la siguiente estructura mínima JSON:
```json
{
    "codigo": "Código del error",
    "error": "Descripción detallada del error"
}
```

En caso de que existan muchos errores se puede utilizar la siguiente estructura JSON:
```
{
    "codigo": "Código del error",
    "error": "Descripción detallada del error",
    "errores": [
        {
            "codigo": "identificador del contexto del error",
            "error": "Descripción detallada del error"
        },
        {
            "codigo": "identificador del contexto del error",
            "error": "Descripción detallada del error"
        },
        ...
    ]
}
```

Por ejemplo, en un servicio de inserción de trámites que se hace de forma masiva y que haya presentado un error, la respuesta esperada es:
```json
{
    "codigo": "0003",
    "error": "Error en el procesamiento de la inserción masiva de servicios",
    "errores": [
        {
            "codigo": 1568548,
            "error": "El servicio no tiene el atributo monto"
        },
        {
            "codigo": 4894564,
            "error": "El monto del servicio no puede ser negativo"
        },
        {
            "codigo": 8598568,
            "error": "La cuenta no corresponde a la entidad"
        },
    ]
}
```

Estos códigos de error deben de retornase en respuesta al cliente utilizando los [códigos HTTP](#códigos-respuesta-http) correspondientes.

```
POST /servicio

# Respuesta de error del servidor
{
    "codigo": "0003",
    "error": "Error en el procesamiento de la inserción masiva de servicios",
    "errores": [
        {
            "codigo": 1568548,
            "error": "El servicio no tiene el atributo monto"
        },
        {
            "codigo": 4894564,
            "error": "El monto del servicio no puede ser negativo"
        }
    ]
}

# HTTP 400 Bad Request
```

##### Codificación.

La codificación en el encabezado “content-type” del protocolo HTTP se establecerá de la siguiente manera:
```
content-type: application/json; charset=utf-8
```

#### SOAP.

SOAP es un protocolo creado para realizar el intercambio estructurado de datos en un entorno descentralizado (no todos los participantes de la comunicación están en el mismo lugar). Se trata de un protocolo de acceso a servicios basado en estándares que define un conjunto de reglas para estructurar los mensajes en XML. Es independiente del protocolo de transporte, del lenguaje de implementación, de la plataforma y del sistema operativo.

Se recomienda utilizar la versión 1.2 de SOAP siempre que sea posible.

##### Buenas Prácticas.

Para mantener la consistencia en el desarrollo de los servicios SOAP, se sugiere implementar las siguientes buenas prácticas:

* Las operaciones y mensajes se definen de acuerdo a lo detallado en el archivo WSDL (Web Service Definition Language o lenguaje de definición de servicio web), que tiene la siguiente estructura:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<wsdl:definitions xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/"> 
	<wsdl:types>
		<!-- definiciones de los tipos de datos (XSD) -->
	</wsdl:types>
	<wsdl:message>
		<!-- definiciones de los datos que se intercambian -->
	</wsdl:message>
	<wsdl:portType>
		<!-- conjunto de operaciones soportadas -->
	</wsdl:portType>
	<wsdl:binding>
		<!-- especificación del protocolo y formato de dato para un portType --> 
	</wsdl:binding>
	<wsdl:service>
		<!-- colección de recursos finales (endpoints) --> 
	</wsdl:service>
</wsdl:definitions>
```

Es importante hacer notar que usualmente este WSDL es generado de manera automática a partir del código en el lenguaje de programación que se desee utilizar.

El archivo WSDL se tiene que publicar y debe ser accesible por la entidad consumidora.

* Existen diferentes formas de traducir el WSDL al mensaje SOAP, esto se define en los estilos. Es recomendable utilizar el estilo documento con uso literal (document/literal), ya que todo lo que se encuentra en el cuerpo del mensaje SOAP se define en el esquema lo que permite validarlo. Este estilo cumple con la especificación WS-I para interoperabilidad.

Los estilos de documentos se definen en el elemento <binding> del archivo
WSDL como se puede observar a continuación:
```xml
<wsdl:binding name="TramiteBinding" type="ns:TramitePortType">
	<soap:binding transport="http://schemas.xmlsoap.org/soap/http" style="document"/> 
<wsdl:operation name="obtenerTramite">
    <soap:operation soapAction="urn:obtenerTramite" style="document"/>
        <wsdl:input>
            <soap:body use="literal" />
        </wsdl:input>
        <wsdl:output>
            <soap:body use="literal" />
        </wsdl:output>
    </wsdl:operation>
</wsdl:binding>
```

* Se recomienda usar notación “camello” (camelCase) para nombrar las operaciones del servicio web.
* Los nombres de las operaciones son verbos descriptivos que denotan acciones a realizar.
* Se recomienda que en el archivo WSDL se tenga operaciones relacionadas a un solo objeto.
* En la implementación de un servicio de interoperabilidad SOAP se recomienda no mantener un estado entre peticiones al servicio (stateless), lo que permite que sea reusable por distintos consumidores.

##### Validación de Mensajes

La validación de la estructura y las restricciones de contenido de XML se la realiza mediante XSD(XML Schema Definition Language), que es una recomendación de la W3C. La versión actual de esta recomendación es la XML Schema 1.1, que consta de dos partes: XML Schema 1.1 Part 1 Structures y XML Schema 1.1 Part 2 Datatypes.

XSD es el lenguaje de definición de esquemas representado mediante XML. Entre sus principales componentes usados se tiene: definiciones de tipo simple, definiciones de tipo complejo, declaración de atributos y declaración de elementos.

Para las restricciones sobre el contenido de los elementos XML se tienen los siguientes tipos de datos más utilizados:

* string: representa cadenas de caracteres.
* boolean: representa valores lógicos.
* dateTime: representa una instancia de tiempo.
* decimal: representa un conjunto de números reales.
* base64binary: representa datos binarios codificados en base 64.

Ejemplo de XSD:
```xml
<xs:element name="persona">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="dui" type="string"/>
            <xs:element name="nombres" type="string"/>
            <xs:element name="apellidos" type="string"/>
            <xs:element name="fechaNacimiento" type="dateTime"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

Es recomendable que se separe la definición de los tipos de datos del archivo WSDL, permitiendo hacer más legible el archivo WSDL; trabajar el archivo XSD (XML Schema Definition) separadamente y reutilizar esquemas y nombres de espacio (namespaces).

##### Versionamiento.

Para el versionamiento en SOAP existen tres opciones que son las más utilizadas:

Versionamiento de la operación: cuando un servicio que tiene muchas operaciones desea modificar solamente una de ellas; para este caso se recomienda aplicar el versionamiento en el nombre de la operación, lo que previene cambios drásticos en el WSDL.
```xml
<wsdl:operation name="operacionV1"></wsdl:operation>
<wsdl:operation name="operacionV2"></wsdl:operation>
```

Versionamiento del servicio: cuando una entidad cambia muchas de las operaciones en un servicio es preferible crear una nueva definición; en este caso se definirá un nuevo WSDL.

La definición de un nuevo WSDL implica que existirá un nuevo recurso final (endpoint).

Agregando al XML la propiedad “version”, de tal manera que el consumidor pueda elegir la versión que requiera de acuerdo al valor enviado en el XML.

Se recomienda mantener el tipo de versionamiento que ya se esté utilizando, sin embargo para los nuevos servicios de interoperabilidad se sugiere realizar el versionamiento agregando al XML la propiedad “version“.

##### Manejo de Errores

Todos los problemas que presenten los servicios de interoperabilidad deben ser identificados, de modo que la entidad consumidora del servicio comprenda el motivo de la falla. Para el tratamiento de errores se recomienda la siguiente estructura XML:
```xml
<respuesta>
	<codigo>Código del error</codigo>
    <error>Descripción detallada del error</error>
</respuesta>
```

En caso de que existan muchos errores se puede utilizar la siguiente estructura XML:
```xml
<respuesta>
	<codigo>Código del error</codigo>
	<error>Descripción detallada del error</error>
	<errores>
		<error>
            <codigo>Identificador del contexto del error</codigo>
            <descripcion>Descripción detallada del error</descripcion>
        </error>
        <error>
            <codigo>Identificador del contexto del error</codigo>
            <descripcion>Descripción detallada del error</descripcion>
        </error>
        …
    </errores>
</respuesta>
```

A continuación se puede ver un ejemplo del manejo de errores en SOAP:
```xml
<respuesta>
    <codigo>0003</codigo>
    <error>Error en el procesamiento de la inserción masiva de trámites</error>
    <errores>
        <error>
            <codigo>15561561</codigo>
            <descripcion>El trámite no tiene el atributo monto</descripcion>
        </error>
        <error>
            <codigo>4455621</codigo>
            <descripcion>El monto del trámite no puede ser negativo</descripcion>
        </error>
        <error>
            <codigo>15267548</codigo>
	        <descripcion>La cuenta no corresponde a la entidad</descripcion>
        </error>
    </errores>
</respuesta>
```

##### Codificación.

Es necesario establecer la codificación en el encabezado <xml> del documento XML de la siguiente manera:
```
<?xml version="1.0" encoding="UTF-8"?>
```

### Códigos de Respuesta HTTP.

Si bien existe una gran cantidad de códigos HTTP, los más utilizados son:

| Código | Detalle | Definición |
| --- | --- | --- |
| 200 | OK | Código básico de éxito. Funciona para los casos generales. Usado especialmente en la respuesta exitosa de GET o el contenido actualizado. |
| 201 | Created | Indica que el recurso fue creado. Típicamente es la respuesta a solicitudes PUT de creación o POST. |
| 202 | Accepted | Indica que la solicitud ha sido aceptada para procesamiento. Típicamente es la respuesta para una llamada a procesamiento asíncrono. |
| 204 | No Content | La solicitud ha tenido éxito, pero no hay nada que mostrar. Frecuentemente enviado luego de DELETE exitoso. |
| 206 | Partial Content | El recurso devuelto está incompleto. Típicamente usado con recursos paginados.|
| 301 | Moved Permanently | El URI solicitado ha sido redireccionado permanentemente a otro recurso. El consumidor debe direccionar estas solicitudes a otro URI. |
| 302 | Found | El  URI  solicitado  ha  sido  redireccionado temporalmente, el consumidor debe seguir pidiendo este recurso en el futuro. |
| 400 | Bad Request | Error general para una solicitud que no puede ser procesada (el consumidor no debe repetir la solicitud sin modificarla). |
| 401 | Unauthorized | Indica que el consumidor no tiene una identidad definida en el servicio. |
| 403 | Forbidden | Indica que el consumidor tiene una identidad definida en el servicio, pero no tiene los permisos para la solicitud que ha realizado. |
| 404 | Not Found | El recurso solicitado no existe. |
| 405 | Method Not Allowed | O el método no está soportado o lo relacionado a este recurso no tiene el permiso. |
| 406 | Not Acceptable | No existe el recurso en el formato solicitado. Por ejemplo, se solicita un recurso en XML pero sólo está disponible en JSON. |
| 500 | Internal Server Error | La solicitud parece correcta, pero un problema ha ocurrido en el servidor. El cliente no puede hacer nada al respecto. |

### Referencias:
* [Estándares de APIs de la Casa Blanca, EE.UU.](https://github.com/WhiteHouse/api-standards)
* [Estándares de APIs Gobierno de Argentina](https://github.com/argob/estandares/blob/master/estandares-apis.md)

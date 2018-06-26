# Estandares de Desempeño y Disponibilidad

La institución publicadora del servicio de web se esforzará para que el servicio esté disponible de forma continua y sin interrupción. A continuación se detallan las características más importantes sobre la disponibilidad de los servicios web.

## Índice
* [Redundancia](#redundancia)
* [Pruebas de Rendimiento](#pruebas-de-rendimiento)
* [Balanceo de Carga](#balanceo-de-carga)
* [Cacheado](#cacheado)
* [Monitoreo](#monitoreo)

## Redundancia.

Para garantizar el estado de los servicios web es recomendable eliminar los puntos únicos de fallo. Esto se logra incorporando componentes redundantes (servidores, enrutadores, energía, software, microservicios, refrigeración, IPs, nombre de dominio y otros), para que en caso de catástrofes o incidencias, el componente pueda reemplazar las tareas del otro que hubiese presentado fallas. Es recomendable poner en práctica este punto para que así se tolere la pérdida o desperfectos funcionales de algún componente de la infraestructura.

No siempre es posible eliminar todos los puntos únicos de fallo debido al costo que esto implica (hacer una evaluación de riesgo contra costo); sin embargo, de acuerdo a la criticidad del servicio web, se recomienda contar con un inventario de toda la infraestructura necesaria para el funcionamiento del servicio y evaluar qué componentes son los que tienen más probabilidad de fallo, para comenzar a aplicar la redundancia.

Cabe mencionar que existen arquitecturas de software que facilitan la redundancia de los elementos más utilizados de un servicio web, como los microservicios.

## Pruebas de Rendimiento.

Es recomendable que los servicios web sean sometidos a un conjunto de pruebas de rendimiento para verificar su escalabilidad, fiabilidad y uso de recursos. Se recomienda utilizar los siguientes tipos:

* Pruebas de carga: realizadas para monitorear el comportamiento de la aplicación bajo una cantidad de peticiones alta. Esto nos permite conocer el límite de peticiones que pueden ser respondidas, lo que a su vez permitirá establecer un límite de consultas o utilizar un balanceador de carga, para mejorar el rendimiento del servicio web evitando su interrupción para los consumidores.
* Pruebas de estrés: con estas pruebas se puede verificar que el servicio web responda de manera adecuada cuando sobrepasa las condiciones normales de consumo.

En base a las mediciones de los resultados de las pruebas de rendimiento (carga y estrés), tomar decisiones en cuanto a los elementos que necesitarán redundancia, ya sean de software o hardware. 

Además es posible verificar el rendimiento de los servicios web realizando un análisis de los tiempos de respuesta en los registros de eventos. 

## Balanceo de Carga.

La infraestructura encargada de proveer los servicios web debe tener la capacidad de distribuir el trabajo entre los recursos con los que cuenta, a fin de evitar problemas en el momento de gestionar una cantidad considerable de solicitudes. Esta necesidad puede ser satisfecha con servidores de proxy reverso (reverse proxy), balanceadores de carga, enrutadores o grupos de servidores (clusters).

Se recomienda aplicar el balanceo de carga en los servicios web que se espera tengan una cantidad alta de instituciones consumidoras. Hay que evaluar la cantidad de solicitudes que el servicio web puede manejar en base a pruebas de rendimiento y de acuerdo a ese límite establecer nuevos recursos que permitan manejar una mayor cantidad de solicitudes.

Si bien esto aumentará la cantidad de solicitudes que se puede manejar, es conveniente revisar si el servicio web no tiene algún problema que evite que pueda responder a más solicitudes, como conexiones no cerradas a la base de datos, no limpiar recursos en la memoria, consultas lentas a la base de datos u otros que pudieran estar afectando el rendimiento del servicio web. La principal desventaja es que se necesita una mayor configuración para poner en marcha el balanceo de carga y el costo que esto implica.

## Cacheado.

Es necesario identificar los servicios web consumidos con una frecuencia considerablemente alta, estos sean almacenados provisionalmente en una memoria extra para aligerar el proceso de consulta y respuesta en los servidores.

El cacheado se emplea comúnmente en operaciones idempotentes y puede efectuarse dentro del mismo servicio web (cargando datos que se soliciten con frecuencia a una estructura en memoria como redis) o como parte de su arquitectura (un servicio extra entre el cliente y el servicio web como varnish).

La arquitectura REST, al ser multicapa, permite la inclusión de manera sencilla de una caché.

Se recomienda el uso del cacheado en servicios web de lectura que requieran un alto rendimiento (se necesita responder a una alta cantidad de solicitudes al mismo tiempo).

Es importante tomar en cuenta que, en caso de modificación de datos, la caché también debe actualizarse ya que una caché no actualizada respondería con datos incorrectos.


## Monitoreo.

Un factor importante a considerar en los servicios web para garantizar su disponibilidad es el constante monitoreo de su estado, esto facilita tomar las acciones pertinentes en caso de problemas, registrandolos y alertando a los administradores del servicio para poder aplicar acciones correctivas y tener un informe estadístico de incidencias en un lapso determinado tiempo.

Las estadísticas contemplan: número total de peticiones por cliente, número total de peticiones correctas y número total de peticiones con error. Deben incluir los filtros por criterios que se consideren más importantes, como la fecha o rangos de fechas para estas peticiones.

También se recomienda verificar los registros de eventos con el propósito de monitorear si el servicio está funcionando correctamente.

Se recomienda siempre aplicar algún mecanismo de monitoreo automático para los servicios web.

Para facilitar el monitoreo automático del estado del servicio se recomienda publicar una operación especial que devuelva una respuesta que permita verificar si el servicio se encuentra disponible. Esta operación debería tener solamente la restricción de autenticación.

Por ejemplo en REST:
```
GET	/estado 
 
HTTP/1,1 200 OK
{
“estado”: “El servicio se encuentra disponible”
}
```

En SOAP se recomienda que esta operación se llame “verificarEstado” y que retorne la siguiente estructura XML:
```
<?xml version="1.0" encoding="UTF-8"?>
<respuesta>
    <estado>El servicio se encuentra disponible</estado> 
</respuesta>
``` 

Adicionalmente, se recomienda publicar una página del estado del servicio con un detalle de los errores que se hubieran registrado y el estado general de salud del mismo.

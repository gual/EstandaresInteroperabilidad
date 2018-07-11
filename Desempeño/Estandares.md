# Estandares de Desempeño y Disponibilidad

La institución publicadora del servicio de web se esforzará para que el servicio esté disponible de forma continua y sin interrupción. A continuación se detallan las características más importantes sobre la disponibilidad de los servicios web.

## Índice
* [Disponibilidad](#disponibilidad)
    * [Modos de fallo](#modo-de-fallo)
    * [Cadena de fallos](#cadena-de-fallos)

* [Desempeño](#desempeño)
    * [Restricciones](#restricciones)
    * [Interrelaciones](#interrelaciones)
    * [Escalabilidad](#escalabilidad)
    * [Mitos](#mitos)

* [Networking](#networking)
    * [Balanceo de carga](#balanceo-de-carga)
    * [Monitoreo](#monitoreo)
- - - -

## Disponibilidad
### Modos de fallo
### Cadena de fallos
- - - -
## Desempeño
### Restricciones
### Interrelaciones
### Escalabilidad
### Mitos
- - - -
## Networking
### Balanceo de Carga
La infraestructura encargada de proveer los servicios web debe tener la capacidad de distribuir el trabajo entre los recursos con los que cuenta, a fin de evitar problemas en el momento de gestionar una cantidad considerable de solicitudes. Esta necesidad puede ser satisfecha con servidores de proxy reverso (reverse proxy), balanceadores de carga, enrutadores o grupos de servidores (clusters).

Se recomienda aplicar el balanceo de carga en los servicios web que se espera tengan una cantidad alta de instituciones consumidoras. Hay que evaluar la cantidad de solicitudes que el servicio web puede manejar en base a pruebas de rendimiento y de acuerdo a ese límite establecer nuevos recursos que permitan manejar una mayor cantidad de solicitudes.

Si bien esto aumentará la cantidad de solicitudes que se puede manejar, es conveniente revisar si el servicio web no tiene algún problema que evite que pueda responder a más solicitudes, como conexiones no cerradas a la base de datos, no limpiar recursos en la memoria, consultas lentas a la base de datos u otros que pudieran estar afectando el rendimiento del servicio web. La principal desventaja es que se necesita una mayor configuración para poner en marcha el balanceo de carga y el costo que esto implica.

Herramientas de balanceo de carga:

[Nginx](http://nginx.org/en/docs/http/load_balancing.html)

### Monitoreo
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

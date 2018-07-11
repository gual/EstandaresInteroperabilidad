# Patrones y antipatrones para los Estandares de Desempeño y Disponibilidad

## Índice
* [Disponibilidad](#disponibilidad)
    * [Antipatrones](#antipatrones)
        * [Puntos de integración](#puntos-de-integración)
        * [Reacciones en cadena](#reacciones-en-cadena)
        * [Fallos en cascada](#fallos-en-cascada)
        * [Usuarios](#usuarios)
        * [Hilos bloqueados](#hilos-bloqueados)
        * [Ataques de auto-negación](#ataques-de-auto-negación)
        * [Efectos de escala](#efectos-de-escala)
        * [Capacidades desbalanceadas](#capacidades-desbalanceadas)
        * [Respuestas lentas](#respuestas-lentas)
        * [Conjunto ilimitado de resultados](#conjunto-ilimitado-de-resultados)
    * [Patrones](#patrones)
        * [Tiempos de espera](#tiempos-de-espera)
        * [Cortacircuitos](#cortacircuitos)
        * [Mamparos](#mamparos)
        * [Estado estable](#estado-estable)
        * [Fallar rápido](#fallar-rápido)
        * [Saludo](#saludo)
        * [Arnés de prueba](#arnés-de-prueba)
        * [Desacoplar Middleware](#desacoplar-middleware)

* [Desempeño](#desempeño)
    * [Antipatrones](#antipatrones)
        * [Contención de grupo de recursos](#contención-de-grupo-de-recursos)
        * [Sobreuso de AJAX](#sobreuso-de-AJAX)
        * [Exceso de tiempo en sesiones](#exceso-de-tiempo-en-sesiones)
        * [Botón de recargar](#botón-de-recargar)
        * [SQL manual](#SQL-manual)
        * [Etroficación de la base de datos](#etroficación-de-la-base-de-datos)
        * [Latencia de puntos de integración](#latencia-de-puntos-de-integración)
        * [Cookie Monster](#cookie-monster)
    * [Patrones](#patrones)
        * [Grupo de conexiones](#grupo-de-conexiones)
        * [Caché](#caché)
        * [Contenido precomputado](#contenido-precomputado)
        * [Afinar el recolector de basura](#afinar-el-recolector-de-basura)

- - - -

## Disponibilidad
### Antipatrones
#### Puntos de integración
Para garantizar el estado de los servicios web es recomendable eliminar los puntos únicos de fallo. Esto se logra incorporando componentes redundantes (servidores, enrutadores, energía, software, microservicios, refrigeración, IPs, nombre de dominio y otros), para que en caso de catástrofes o incidencias, el componente pueda reemplazar las tareas del otro que hubiese presentado fallas. Es recomendable poner en práctica este punto para que así se tolere la pérdida o desperfectos funcionales de algún componente de la infraestructura.

No siempre es posible eliminar todos los puntos únicos de fallo debido al costo que esto implica (hacer una evaluación de riesgo contra costo); sin embargo, de acuerdo a la criticidad del servicio web, se recomienda contar con un inventario de toda la infraestructura necesaria para el funcionamiento del servicio y evaluar qué componentes son los que tienen más probabilidad de fallo, para comenzar a aplicar la redundancia.

Cabe mencionar que existen arquitecturas de software que facilitan la redundancia de los elementos más utilizados de un servicio web, como los microservicios.

#### Reacciones en cadena
#### Fallos en cascada
#### Usuarios
#### Hilos bloqueados
#### Ataques de auto-negación
#### Efectos de escala
#### Capacidades desbalanceadas
#### Respuestas lentas
#### Conjunto ilimitado de resultados
### Patrones
#### Tiempos de espera
#### Cortacircuitos
#### Mamparos
#### Estado estable
#### Fallar rápido
#### Saludo
#### Arnés de prueba
Es recomendable que los servicios web sean sometidos a un conjunto de pruebas de rendimiento para verificar su escalabilidad, fiabilidad y uso de recursos. Se recomienda utilizar los siguientes tipos:

* Pruebas de carga: realizadas para monitorear el comportamiento de la aplicación bajo una cantidad de peticiones alta. Esto nos permite conocer el límite de peticiones que pueden ser respondidas, lo que a su vez permitirá establecer un límite de consultas o utilizar un balanceador de carga, para mejorar el rendimiento del servicio web evitando su interrupción para los consumidores.
* Pruebas de estrés: con estas pruebas se puede verificar que el servicio web responda de manera adecuada cuando sobrepasa las condiciones normales de consumo.

En base a las mediciones de los resultados de las pruebas de rendimiento (carga y estrés), tomar decisiones en cuanto a los elementos que necesitarán redundancia, ya sean de software o hardware. Además es posible verificar el rendimiento de los servicios web realizando un análisis de los tiempos de respuesta en los registros de eventos. 

Herramientas de pruebas de rendimiento:

[Locus](https://locust.io/)

#### Desacoplar Middleware
- - - -
## Desempeño
### Antipatrones
#### Contención de grupo de recursos
#### Sobreuso de AJAX
#### Exceso de tiempo en sesiones
#### Botón de recargar
#### SQL Manual
#### Etroficación de la base de datos
#### Latencia de puntos de integración
#### Cookie Monster
### Patrones
#### Grupo de conexiones
#### Caché
Es necesario identificar los servicios web consumidos con una frecuencia considerablemente alta, estos sean almacenados provisionalmente en una memoria extra para aligerar el proceso de consulta y respuesta en los servidores.

El cacheado se emplea comúnmente en operaciones idempotentes y puede efectuarse dentro del mismo servicio web (cargando datos que se soliciten con frecuencia a una estructura en memoria como redis) o como parte de su arquitectura (un servicio extra entre el cliente y el servicio web como varnish).

La arquitectura REST, al ser multicapa, permite la inclusión de manera sencilla de una caché.

Se recomienda el uso del cacheado en servicios web de lectura que requieran un alto rendimiento (se necesita responder a una alta cantidad de solicitudes al mismo tiempo).

Es importante tomar en cuenta que, en caso de modificación de datos, la caché también debe actualizarse ya que una caché no actualizada respondería con datos incorrectos.

#### Contenido precomputado
#### Afinar el recolector de basura
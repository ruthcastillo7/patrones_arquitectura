# PATRONES DE ARQUITECTURA
> [!NOTE]
> 👍 Un **patron arquitectonico** es una solucion general y reutilizable a un problema comun en la arquitectura de sofware dentro de un contexto dado. Los patrones arquitectura son la habilidad de organizacion a nivel de carpeta dentro del proyecto de sofware.

**PATRONES ARQUITECTONICOS MAS CONOCIDOS😲:**

1. PATRON DE CAPAS
2. PATRON CLIENTE-SERVIDOR
3. PATRON MAESTRO-ESCLAVO
4. `PATRON FILTRO DE TUBERIA`
5. PATRON INTERMEDIARIO
6. PATRON DE IGUAL A IGUAL
7. PATRON DE BUS EVENTO
8. MODELO-VISTA-CONTROLADOR
9. ARQUITECTURA LIMPIA
10. ARQUITECTURA HEXEGONAL


## PATRON INTERMEDIARIO O PATRON DEL AGENTE (Mediador (Broker pattern))
> [!CONCEPTO]
> ## PATRON INTERMEDIARIO O PATRON DEL AGENTE
> [!CONCEPTO]
Este patrón se usa para estructurar sistemas distribuidos con componentes desacoplados. Estos componentes pueden interactuar entre sí mediante invocaciones de servicios remotos. Un componente de intermediario es responsable de la coordinación de la comunicación entre los componentes. 
Los servidores publican sus capacidades (servicios y características) a un intermediario. Los clientes solicitan un servicio del intermediario y el intermediario redirecciona al cliente a un servicio adecuado desde su registro.
![alt text](image.png)

## El Broker:
El Broker es un patrón de arquitectura que se utiliza para estructurar sistemas de software distribuidos con componentes desacoplados que interactúan por invocaciones de servicios remotos. Esto quiere decir que, si un componente necesita un servicio de otro que está en otra ubicación que no conoce, el broker se encarga de proporcionar la conexión.

## PROBLEMA
Construir un sistema de software usando un sistema distribuido con componentes desacoplados aporta una flexibilidad al mantenimiento y al cambio, pero para ello es necesario un sistema de comunicación. Si los componentes manejaran la comunicación por sí mismos, el sistema se enfrentaría a diversas dependencias y limitaciones.

Se necesitan servicios para añadir, quitar, intercambiar, activar y localizar componentes. Las aplicaciones que utilizan estos servicios no deben depender de los detalles específicos del sistema a fin de garantizar interoperabilidad, aún en una red heterogénea.

## SOLUCIÓN
El patrón Broker ofrece una solución al problema anterior actuando como «mediado» entre los diferentes componentes. Así, una aplicación puede acceder a los servicios distribuidos enviando mensajes al objeto apropiado, en vez de enfocarse en la comunicación entre procesos de bajo nivel. También facilita el cambio y la adición de objetos y funciones.


Se pueden clasificar en dos tipos:

- Servidores que ofrecen servicios comunes a muchos dominios de aplicación
- Servidores específicos para dominios específicos
## Cliente:
Los clientes son aplicaciones que accesan los servicios de, al menos, un servidor. La interacción entre clientes y servidores se basa en un modelo dinámico, lo cual significa que los servidores también pueden actuar como clientes. Los clientes no necesitan conocer la ubicación de los servidores que accesan; esto es importante porque permite la agregación de nuevos servicios, y el movimiento de los servicios existentes a otras ubicaciones, aún mientras el sistema este ejecutándose.

## Broker:
El Broker es el responsable de la comunicación entre los clientes y servidores. Cuando un cliente necesita un servicio de un servidor, envía una petición al broker, que a su vez se la envía al servidor. El servidor realiza la funcionalidad correspondiente y envía la respuesta (o excepción) de vuelta al broker, que se la devuelve al cliente. También ofrece API’s a clientes y servidores que incluyen operaciones para el registro de servidores, y la invocación de métodos de servidores.

Si el servidor especificado es mantenido por otro broker, el broker local encuentra una ruta al broker remoto y le envía la solicitud.

## Proxies:
Podemos distinguir dos tipos de proxies: los proxies del lado del cliente y los proxies del lado del servidor:

- Proxies del cliente: Se ubican entre el cliente y el broker para esconder detalles de implementación como el marshalling (empaquetado de parámetros), la creación y eliminación de bloques de memoria y el mecanismo de comunicación utilizado para enviar el mensaje.
- Proxies del servidor: Son análogos a los proxies del cliente, con el añadido de que reciben las solicitudes, las desempaquetan, llaman al servicio apropiado y hacen el marshalling de la respuesta o excepción.
## Puentes:
Son un componente opcional utilizado para esconder detalles de implementación cuando dos brokers interoperan.

## ALGUNAS VARIANTES
- Sistema de comunicación directa:
En esta variante los clientes pueden comunicarse directamente con los servidores. El broker indica a los clientes los canales de comunicación que provee el servidor, entonces el cliente puede establecer un enlace directo al servidor solicitado.

- Sistemas de Paso de Mensajes:
Esta variante es apropiada para sistemas que se enfocan en la transmisión de datos. Los servidores utilizan un tipo de mensaje para determinar lo que deben hacer, en vez de ofrecer servicios que los clientes pueden invocar.

- Sistemas Callback:
En vez de implementar un modelo de comunicación activa donde los clientes producen solicitudes y los servidores las consumen, se puede utilizar un modelo reactivo que se maneja por eventos sin hacer distinción entre clientes y servidores. Cuando un evento llega, el broker invoca el método callback del componente registrado para reaccionar ante ese evento, cuya ejecución, a su vez puede generar nuevos eventos causando que el broker dispare nuevas invocaciones de métodos callback.



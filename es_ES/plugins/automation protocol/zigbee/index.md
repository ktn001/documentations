# Complemento de Zigbee

**El complemento Zigbee para Jeedom** se basa en el excelente trabajo realizado en torno a **la biblioteca Zigpy de código abierto** para ofrecer un **compatibilidad general con diferentes hardware Zigbee**. Permite la comunicación con los siguientes controladores Zigbee :

-	**Deconz** : Probado y validado por el equipo de Jeedom. *(No es necesario instalar la aplicación deCONZ)*
-	**EZSP (laboratorios de silicio)** : Probado y validado por el equipo de Jeedom.
-	**XBee** : No probado por el equipo de Jeedom.
-	**Zigate** : No probado por el equipo. *(en experimental en Zigpy)*
-	**ZNP (Texas Instruments, pila Z 3.X.X)** : No probado por el equipo. *(en experimental en Zigpy)*
-	**CC (Texas Instruments, pila Z 1.2.X)** : No probado por el equipo. *(en experimental en Zigpy)*

Además, el complemento contiene muchas herramientas que permiten :

- hacerse cargo de **varios controladores al mismo tiempo**,
- la **copia de seguridad y restaurar** un controlador,
- la **Actualización de firmware** un controlador,
- la **actualización de módulos** en OTA,
- visualización de nodos y **gráfico de red**,
- administración de **grupos**,
- la administración de **Unión**,
- hacerse cargo de **Touchlink**,
- o incluso para integrar sus propias configuraciones para los más experimentados...

# Configuration

## Configuración del plugin

**El complemento Zigbee** utiliza dependencias que deberán instalarse primero. Una vez instaladas las dependencias, puede configurar uno o más controladores Zigbee ingresando **el tipo de controlador, el puerto del controlador y el canal a utilizar**, luego (re) iniciar el demonio.     

![Configuración contrôleur Zigbee](./images/zigbee_controllerConfig.png)

>**Importante**
>
>Cualquier cambio de canal requerirá un reinicio del demonio. Un cambio de canal también puede requerir la reincorporación de ciertos módulos.

### Configuración avanzada de Zigpy (reservada para expertos !)

Es posible configurar parámetros específicos para el subsistema Zigbee *(Zigpy)*. Esta parte está estrictamente reservada para expertos, por lo que el equipo de Jeedom no proporciona la lista de posibles parámetros *(hay cientos de ellos dependiendo del tipo de controlador)*.

El campo de entrada acepta código en formato `json` de este tipo :

''''''''
{
    "ezsp": {
        "CONFIG_ADDRESS_TABLE_SIZE": "16"
    }
}
''''''''

>**Importante**
>
>Cualquier solicitud de soporte será rechazada automáticamente si se completa este campo.

## Configuración del equipo

### Inclusión de un módulo Zigbee

La inclusión es la parte más compleja de Zigbee. Aunque simple, la operación a menudo se repite varias veces para lograr. El lado del complemento Jeedom es fácil, solo haga clic en el botón **Modo de inclusión** después de lo cual tienes 3 minutos para incluir el equipo.

El procedimiento de inclusión es específico para cada módulo. Consulte la documentación del fabricante para lograrlo.

>**TRUCO**
>
>No olvides hacer un reinicio *(reset)* del módulo antes de cualquier inclusión.

### Configurar un módulo Zigbee

Una vez incluido, se supone que Jeedom reconoce automáticamente el módulo y crea los comandos correspondientes. Si este no es el caso, consulte el siguiente párrafo : **Módulo no reconocido**.

>**Importante**
>
>Debido a un error en algún firmware *(Ikea, Sonoff, etc)*, a veces es necesario elegir el tipo de módulo directamente de la lista **Dispositivos** luego guarde para que los pedidos se creen correctamente.

Como de costumbre, puede darle un nombre a su equipo, ingresar una categoría o un objeto principal y activarlo o hacerlo visible.

También se pueden acceder a otros parámetros más específicos :

- **Identificación** : identificador único del equipo. Incluso durante una reincorporación o si cambia el tipo de controlador Zigbee.
- **Controlador Zigbee** : utilizado para seleccionar el controlador Zigbee en comunicación con el equipo.
- **Control de comunicación** : le permite seleccionar el modo de verificación de la buena comunicación entre el controlador y el módulo.
- **Ignorar la confirmación de ejecución** : marque la casilla para ignorar la ejecución correcta del comando. Esto le permite recuperar el control más rápidamente, pero no garantiza que el pedido se haya realizado correctamente.
- **Permitir hacer cola** : marque la casilla para permitir la cola de pedidos. Esto le permite volver a intentarlo en caso de que la orden no se haya ejecutado.

La parte **Información** permite la selección manual de fabricante y equipo. También está la visualización del equipo así como dos botones que permiten la regeneración de los comandos o el acceso a las opciones de configuración del módulo.

En la pestaña **Pedidos**, encontramos, como es habitual, los comandos que permiten la interacción con el módulo.

### Módulo no reconocido

Si Jeedom no reconoce automáticamente su módulo *(no se crearon pedidos)* pero bien incluido, por lo que tienes que pedir que lo agreguen al equipo de Jeedom.

>**INFORMACIÓN**
>
>El equipo de Jeedom se reserva el derecho a rechazar cualquier solicitud de integración. Siempre es preferible optar por equipos cuya compatibilidad ya esté confirmada.

Para solicitar la incorporación de nuevos equipos, es necesario aportar los siguientes elementos :

- **el modelo exacto** del módulo con un enlace al sitio de compra,
- En la página del equipo, haga clic en el botón azul **Configuración del módulo** luego tabula **Información en bruto**. Copia el contenido para transmitirlo al equipo de Jeedom,
- Ponga el demonio en `debug` desde la página de configuración del complemento y reinícielo. Realizar acciones en el equipo *(si es un sensor de temperatura, variar la temperatura por ejemplo, si es una válvula, variar el setpoint, etc...)* y envía el registro `zigbee` *(no `zigbeed`)*.

>**INFORMACIÓN**
>
>Cualquier solicitud incompleta será rechazada sin una respuesta del equipo de Jeedom.

### Cómo funcionan los controles para los expertos

Explicamos a continuación cómo funcionan los comandos en el complemento para los usuarios más avanzados :

- ''''attributes::ENDPOINT::CLUSTER_TYPE::CLUSTER::ATTRIBUT::VALUE'''' te permite escribir el valor de un atributo *(tenga cuidado, no se pueden cambiar todos los atributos)* con :
  - ''''ENDPOINT'''' : número de punto final,
  - ''''CLUSTER_TYPE'''' : tipo de clúster *(EN \| OUT)*,
  - ''''CLUSTER'''' : número de grupo,
  - ''''ATTRIBUT'''' : número de atributo,
  - ''''VALUE'''' : valor para escribir.

**Ejemplo** : ''''attributes::1::in::513::18::#slider#*100'''' que escribirá el atributo en el punto final `1`, clúster entrante (''''in'''') `513`, atributo` 18` con el valor del ''''slider*100''''.

- ''''ENDPOINT::CLUSTER:COMMAND::PARAMS'''' le permite ejecutar un comando de servidor con :
  - ''''ENDPOINT'''' : número de punto final,
  - ''''CLUSTER'''' : nombre del clúster,
  - ''''COMMAND'''' : Nombre de la orden,
  - ''''PARAMS'''' parámetro en el orden correcto separado por `::''.

**Ejemplo** : ''''1::on_off::on'''', ejecutar el comando ''''on'''' en el punto final "1" del clúster ''''on_off'''' sin parámetros.        
**Ejemplo** : ''''1::level::move_to_level::#slider#::0'''', ejecutar el comando ''''move_to_level'''' en el punto final "1" del clúster ''''level'''' Con parámetros ''''#slider#'''' y ''''0''''.

# Outils

Se puede acceder a diferentes herramientas que ofrecen una mejor interactividad con su red Zigbee desde la página de configuración del complemento :

![Herramientas contrôleur Zigbee](./images/zigbee_controllerTools.png)

## Copia de seguridad / restauración de un controlador

Es posible hacer una copia de seguridad de la red Zigbee desde controladores de tipo EZSP *(Elelabs por ejemplo)* y ZNP. Esta copia de seguridad se puede restaurar en otro controlador del mismo tipo.

>**Importante**
>
> En llaves de tipo EZSP *(Elelabs)*, solo es posible realizar una única restauración de copia de seguridad en todos y para todos durante toda la vida útil de la clave.

La copia de seguridad no contiene la lista de módulos sino solo la información básica de la red Zigbee. Por lo tanto, no es necesario realizarlo con regularidad, una sola copia de seguridad suele ser suficiente porque esta información no cambia durante la vida útil del controlador.

>**INFORMACIÓN**
>
>Los demonios de Zigbee se detienen durante el proceso de copia de seguridad o restauración.

## Actualización del firmware del controlador

Es posible actualizar el firmware del controlador Zigbee desde Jeedom *(actualmente solo se aplica a los controladores Elelabs)*. Siendo el firmware imprescindible en Zigbee porque gestiona el enrutamiento entre otras cosas, es importante actualizarlo.

>**INFORMACIÓN**
>
>Los demonios de Zigbee se detienen durante una actualización de firmware.

## Actualización de módulos OTA

Actualizaciones de OTA *(Over-The-Air)* son las actualizaciones de firmware de los módulos. El proceso puede llevar un tiempo determinado (varias horas dependiendo de la cantidad de módulos) pero permite una mayor confiabilidad de la red Zigbee en general. Para poder actualizar un módulo, el fabricante debe comunicar el firmware :

- Con respecto a **Ikea** y **El avance**, los firmwares están disponibles directamente en línea donde el complemento los recuperará.
- Para otros (ver [aquí](https://github.com/Koenkk/zigbee-OTA/tree/master/images)), el fabricante proporciona informalmente una actualización en algunos casos.
- Para todos los demás, no es posible actualizar el módulo desde el complemento.

Para beneficiarse de las actualizaciones de OTA, debe marcar la casilla correspondiente en la página de configuración del complemento y luego guardar. Luego debe hacer clic en el botón **Actualizar archivos de módulo** para recuperar los últimos archivos actualizados y finalmente reiniciar el demonio Zigbee.

Las actualizaciones se realizan automáticamente en caso de disponibilidad o si el módulo lo solicita. Es posible forzar la actualización de un módulo desde la pestaña **Comportamiento** desde la ventana de configuración del módulo en la página del dispositivo.

Desafortunadamente, no hay un indicador simple para seguir el progreso de la actualización, la única solución es consultar los registros de `zigbee_X` en la depuración y buscar el término` OTA`. Podrá ver este tipo de registro cuando se actualice un módulo :

''''''''
2020-02-27 15:51:10 [DEBUG][0x7813:1:0x0019] OTA query_next_image handler for 'IKEA of Sweden TRADFRI control outlet': field_control=1, manufacture_id=4476, image_type=4353, current_file_version=536974883, hardware_version=60
2020-02-27 15:51:10 [DEBUG][0x7813:1:0x0019] OTA image version: 537011747, size: 204222. Update needed: True
2020-02-27 15:51:18 [DEBUG][0x7813:1:0x0019] OTA image_block handler for 'IKEA of Sweden TRADFRI control outlet': field_control=0, manufacturer_id=4476, image_type=4353, file_version=537011747, file_offset=0, max_data_size=63, request_node_addr=Noneblock_request_delay=None
2020-02-27 15:51:18 [DEBUG][0x7813:1:0x0019] OTA upgrade progress: 0.0
''''''''

# Touchlink

**Touchlink** *(o Lightlink)* es una función particular de Zigbee que permite al controlador enviar órdenes de gestión a un módulo con la condición de estar muy cerca de él *(menos de 50 centímetros)*. Esto es útil, por ejemplo, para restablecer bombillas que no tienen botón físico.

Esta función está disponible en bombillas tipo Zigbee **Philips Hue, Ikea, Osram, Icasa y muchos más...** El principio es muy simple, para poder asociar este tipo de módulo con una red Zigbee, primero debes realizar un reset. Al reiniciar, el módulo intentará asociarse automáticamente con la primera red Zigbee disponible.

## Restablecer en Touchlink

Como suele ocurrir en Zigbee, pueden surgir dificultades durante el proceso de reinicio o asociación. Hay varios métodos disponibles para lograr esto :

- **Realice rápidamente 5/6 ciclos de encendido / apagado** *(encendido apagado)*. La bombilla debe parpadear al final del procedimiento para indicar el reconocimiento correcto.
- **Usa un control remoto zigbee**, y :
  - **para mandos a distancia Philips Hue**, presione simultáneamente los botones de ENCENDIDO y APAGADO durante 5 a 10 segundos cerca de la bombilla encendida *(a veces tienes que apagar / encender la bombilla justo antes en algunos modelos)*,
  - **para mandos a distancia de Ikea**, presione el botón de reinicio" *(al lado de la batería)* durante 5 a 10 segundos cerca de la bombilla encendida *(a veces tienes que apagar / encender la bombilla justo antes en algunos modelos)*.
- Acerca de **Bombillas Philips Hue**, también puede incluirlos en Hue Bridge y luego eliminarlos de él.

# Binding

El enlace le permite vincular 2 módulos directamente entre sí sin que las órdenes pasen por Jeedom. El enlace se realiza desde un clúster al mismo clúster de otro módulo. El enlace siempre debe realizarse desde el control (tipo de control remoto) al actuador.

Encontrará los elementos de gestión de enlaces, si es compatible con su módulo, en la pestaña **Información** desde la ventana de configuración del módulo.

Algunos módulos no son compatibles con la encuadernación y otros *(como los módulos de Ikea)* Solo soporta la vinculación del comando a un grupo, por lo tanto, es necesario comenzar por hacer un grupo en el que tendrás que poner el actuador.

# Red Zigbee

La constitución de una red Zigbee de buena calidad es de gran ayuda gracias a las herramientas disponibles en el complemento. Vaya a la página general del complemento que enumera todos los equipos y haga clic en el botón **Redes Zigbee** para acceder a diversas informaciones y acciones en torno a la red Zigbee así como a la gráfica representativa de la misma.

## Gráfico de red

El gráfico de red proporciona una descripción general de la red Zigbee y la calidad de las comunicaciones con los diferentes módulos.

>**INFORMACIÓN**
>
>El gráfico de la red Zigbee es indicativo y se basa en los vecinos que declaran los módulos. Esto no representa necesariamente el enrutamiento real, sino un enrutamiento posible.

## Optimizando la red

Para optimizar la confiabilidad de su red Zigbee, es más que recomendable tener al menos 3 módulos de enrutador permanentemente alimentados y evitar desenchufarlos. De hecho, durante nuestras pruebas notamos una clara mejora en la confiabilidad y resistencia de la red Zigbee al agregar módulos de enrutador. También es aconsejable incluirlos primero, de lo contrario, el "dispositivo final" tardará entre 24 y 48 horas" *(módulos sin enrutador)* descúbrelos.

Otro punto importante, es posible, al retirar un módulo de enrutador, que parte del "dispositivo final" *(módulos sin enrutador)* ya sea perdido por un tiempo más largo o más corto *(en diez horas o más)* o incluso definitivamente y tienes que volver a incluirlos.
Desafortunadamente, esto se debe a la forma en que el fabricante ha planeado la integración de su equipo dentro de una red Zigbee y, por lo tanto, no puede ser corregido por el complemento que no gestiona la parte de enrutamiento.

Finalmente, y aunque pueda parecer obvio para algunos, te recordamos que las pasarelas Zigbee en Wifi son menos confiables que las pasarelas USB. Por lo tanto, el equipo de Jeedom recomienda el uso de una puerta de enlace Zigbee en USB.  

# FAQ

>**LQI o RSSI es N / A**
>
>Normalmente es después de reiniciar la red Zigbee que se vacían los valores. Tienes que esperar a que el módulo se comunique nuevamente para que se ingresen los valores.


>**Tengo problemas de inclusión o errores en los registros de tipos ''''TXStatus.MAC_CHANNEL_ACCESS_FAILURE''''**
>
>Debe intentar quitar o cambiar la extensión USB si usa una o poner una si no usa una.


>**Tengo errores ''''can not send to device'''' o ''''send error'''' o ''''Message send failure''''**
>
>Por lo general, esto se debe a un problema de enrutamiento. el enrutamiento es más o menos fijo en Zigbee y no simétrico, un módulo puede usar una ruta diferente para responder a la que se usa para hablar con él. A menudo, el corte eléctrico *(quitar las pilas, por ejemplo)* y enciende la energía *(o reemplazo de baterías)* es suficiente para solucionar el problema.


>**Tengo errores extraños en los módulos de batería o problemas de inclusión**
>
>Hemos notado que una buena parte de los problemas de Zigbee en los módulos de batería se deben a las baterías o posiblemente a problemas al restablecer los módulos antes de su inclusión. Aunque parezcan nuevas, es recomendable probarlas con baterías nuevas para descartar esta hipótesis.


>**Me preocupa actualizar los valores del equipo**
>
> 2 posibilidades :
> - este es un "módulo antiguo" en ZLL *(ver la configuración del equipo Jeedom que indica si es ZHA o ZLL)*. En este caso, es absolutamente necesario un comando "Actualizar" para que usted o Jeedom fuercen la actualización de los valores. Si este comando no existe en el equipo, debe comunicarse con el soporte de Jeedom para que se agregue en la próxima versión estable. Una vez fuera, haga clic en el botón **Recrear comandos** sin borrar.
> -	el módulo está en ZHA, por lo que es una preocupación de inclusión. En la pestaña **Acción** de la configuración del módulo, hay un botón **Restablecer módulo** permitiendo forzar acciones posteriores a la inclusión. Se debe tener cuidado para mantener el módulo activo si está en batería.
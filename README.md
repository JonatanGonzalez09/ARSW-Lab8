### Escuela Colombiana de Ingeniería
### Arquitecturas de Software - ARSW

## Escalamiento en Azure con Maquinas Virtuales, Scale Sets y Service Plans

## Autores
- David Caycedo
- Jonatan Gonzalez

## Solución a preguntas parte 1
**1. ¿Cuántos y cuáles recursos crea Azure junto con la VM?**

_Al momento de crear una maquina una virtual en Azure, se crean los siguientes recursos :_
- _La maquina virtual_
- _Una red virtual (VNet)_
- _Una dirección IP publica_
- _Un grupo de seguridad de red_
- _Una cuenta de almacenamiento_
- _Una interfaz de red_
- _Un disco_


**2. ¿Brevemente describa para qué sirve cada recurso?**

**Maquina Virtual: (VM)** _Son computadoras de software que proporcionan la misma funcionalidad que las computadoras físicas, tambien ejecutan aplicaciones y constan de un sistema operativo y se caracterizan por comportarse como sistemas informáticos separados._

**Red virtual (VNet):** _Es una representación de su propia red en la nube, y es usada generalmente para aprovisionar y administrar redes privadas virtuales (VPN). Al crear una red virtual se crea su propio bloque **CIDR** y se puede vincular a otras redes virtuales y redes locales siempre que los bloques CIDR no se superpongan, ademas tiene control de la configuración del servidor DNS para redes virtuales y segmentación de la red virtual en subredes._

**Direccion IP publica:** _Una direccion IP permite la ubicación de dispositivos digitales que están conectados a Internet para ser identificados y diferenciados de otros dispositivos. En Azure existen dos tipos de direcciones IP las **privadas** que se usan para la comunicación dentro de una red virtual (VNet) de Azure y en la red local, cuando se usa una puerta de enlace de VPN o un circuito ExpressRoute para ampliar la red a Azure y existen las **publicas** que se usan para la comunicación con Internet, incluidos los servicios de acceso público de Azure._

**Grupo de seguridad de red:** _Un grupo de seguridad de red es utilizado para filtrar el tráfico de red hacia y desde los recursos que existan. Un grupo de seguridad de red contiene reglas de seguridad que otorgan o prohíben el tráfico de red entrante o el tráfico de red saliente, de varios tipos de recursos. Otro punto interesante para los grupos de seguridad, es que por cada regla, puede especificar el origen y el destino, el puerto y el protocolo._

**Cuenta de almacenamiento (storage account):** _Una cuenta de almacenamietno se crea para brindar acceso a los servicios en Azure Storage, eso quiere decir que para usar los servicios de Azure necesitamos tener una cuenta de almacenamient, ya que las aplicaciones usan esta cuenta para obtener acceso a los servicios. Por lo general una cuenta de almacenamiento está asociada con una ubicación geográfica específica._

**Interfaz de red (Network interface controller):** _Es el software específico de red que se comunica con el controlador de dispositivo específico de red y la capa IP a fin de proporcionar a la capa IP una interfaz coherente con todos los adaptadores de red que puedan estar presentes. En pocas palabras es el que permite al recurso comunicarse mediante Ethernet o Wi-Fi._

**Disco:** _Los discos administrados de Azure se almacenan como blobs en páginas, que son un objeto de almacenamiento de E/S aleatorio en Azure. Estos discos son una abstracción sobre los blobs en páginas, los contenedores de blobs y las cuentas de almacenamiento de Azure. Con los discos administrados, lo único que debe hacer es aprovisionar el disco y Azure se encarga del resto._

**3. ¿Al cerrar la conexión ssh con la VM, por qué se cae la aplicación que ejecutamos con el comando ```npm FibonacciApp.js```? ¿Por qué debemos crear un *Inbound port rule* antes de acceder al servicio?**

* _La aplicación **se cae debido a** que el proceso esta vinculado a la conexion ssh y al cerrar esta el proceso se da por terminado._
* _La creacción de **Inbound port rule** nos permitira asignarle al servicio un puerto en especifico para que todo el trafico de este pase por dicho puerto, es decir con el inbound podemos permitir o denegar el trafico de red._

**4. Adjunte tabla de tiempos e interprete por qué la función tarda tando tiempo.**

![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/tiempos.JPG)

**5. Adjunte imágen del consumo de CPU de la VM e interprete por qué la función consume esa cantidad de CPU.**

B1ls

![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/cpu1.png)

B2ms

![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/cpu2.png)

**6. Adjunte la imagen del resumen de la ejecución de Postman. Interprete:**
    **- Tiempos de ejecución de cada petición.**
    **- Si hubo fallos documentelos y explique.**
    
 B1ls
 
 ![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/postman1.png)   
 ![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/res1b.png) 
 
 B2ms
 
  ![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/res2a.png) 
    ![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/res2b.png) 

Se presentaba el siguiente error: ECONNRESET: Significa que el servidor cerró la conexión de una manera que probablemente no era normal.

**7. ¿Cuál es la diferencia entre los tamaños `B2ms` y `B1ls` (no solo busque especificaciones de infraestructura)?**
* _Una instancia de **B2ms** cuenta con **2 vCPU**, **8 GiB de RAM**, **16 GiB de Almacenamiento Temporal**, **tiene una Base CPU perf of VM del 60%** y **tiene una Max CPU perf of VM del 200%**._
* _Una instancia de **B1ls** cuenta con **1 vCPU**, **0.5 GiB de RAM**, **4 GiB de Almacenamiento Temporal**, **tiene una Base CPU perf of VM del 5%** y **tiene una Max CPU perf of VM del 100%**._

**8. ¿Aumentar el tamaño de la VM es una buena solución en este escenario?, ¿Qué pasa con la FibonacciApp cuando cambiamos el tamaño de la VM?**

_Al aumentar el tamaño de la VM solucionamos el consumo de CPU ya que se disminuye este consumo pero no mejora el tiempo de ejecucion, tiene una leve disminución pero en general este se mantiene constante._

**9. ¿Qué pasa con la infraestructura cuando cambia el tamaño de la VM? ¿Qué efectos negativos implica?**

_Al aplicar el cambio de tamaño a la VM debemos de reiniciar la maquina, y esto implica que los servicios se terminen, generando una perdida de disponibilidad por un periodo de tiempo, mientras se vuelven a iniciar los servicios._

**10. ¿Hubo mejora en el consumo de CPU o en los tiempos de respuesta? Si/No ¿Por qué?**

_Si Hubo mejora en el consumo de CPU, ya que como existen mas nucleos puede procesar mas solicitudes. Pero en los tiempos de respuesta no hubo mejoras, ya que esto depende de la aplicación en si y no del procesador que tenga que sistema._

**11. Aumente la cantidad de ejecuciones paralelas del comando de postman a `4`. ¿El comportamiento del sistema es porcentualmente mejor?**

## Solución preguntas parte 2
**1. ¿Cuáles son los tipos de balanceadores de carga en Azure y en qué se diferencian?, ¿Qué es SKU, qué tipos hay y en qué se diferencian?, ¿Por qué el balanceador de carga necesita una IP pública?**

_En Azure existen dos tipos de balanceadores de carga:_

_**Un Balanceador de Carga Publico:** Que puede proporcionar conexiones salientes para máquinas virtuales (VM) dentro de su red virtual.Estas conexiones se logran traduciendo sus direcciones IP privadas a direcciones IP públicas, en general estos balanceadores de carga son usados para equilibrar la carga del tráfico de Internet a sus máquinas virtuales._

_**Un Balanceador de Carga Interno (Privado):** Los cuales necesitan IP privadas solo en la interfaz. Estos balanceadores utilizan para equilibrar el tráfico dentro de una red virtual._

_**¿Qué es SKU, qué tipos hay y en qué se diferencian?**_

_SKU : Sus siglas significan Unidad de mantenimiento de existencias y es un número o código asignado a un elemento para poder identificarlo._
_Existen 6 tipos diferentes de SKU:_
- _**Standard:** Es asignado a un producto estandar, y estos se pueden vender individualmente o como partes de conjuntos, paquetes o colecciones._
- _**Component:** Son piezas incluidas en ensamblajes, paquetes y colecciones y  no se pueden vender como productos independientes._
- _**Assembly:** Son necesarios para el ensamblaje deben ubicarse dentro de la misma instalación, ya sea su instalación local o la de un proveedor de Dropship / JIT / 3PL y para benderlos todas las cantidades las SKU asociadas deben estar disponibles._
- _**Bundle:** Son SKU que tienen SKU asociados que no necesitan ensamblarse antes del envío, estas pueden enviarse a los clientes desde diferentes fuentes de cumplimiento, y para venderlos todas las cantidades necesarias de todos los SKU asociados deben estar disponibles._
- _**Collection:** Son SKU asociadas vinculadas con fines de marketing para vender o vender productos relacionados, y estos SKU no pueden ser vendidos._
- _**Virtual:** Estos SKU no requieren inventario y funcionan con un nivel de inventario de 0, tienen SKU virtuales los cuales no se sincronizan actualmente en el catálogo, pero se asociarán con pedidos que se importen con una SKU coincidente._

**2. ¿Cuál es el propósito del *Backend Pool*?**

_El Backend Pool hace referencia al conjunto de backends que reciben tráfico similar para su aplicación.El propósito de este backend pool es alojar la maquina virtua que seran dependendientes del balanceador de carga, tambien tiene un SKU asociado el cual dependiendo la zona tiene cierta capacidad, por ejemplo el SKU basico el back-end pool tiene una capacidad de 100 instancias de maquinas virtuales mientras que el SKU estandar cuenta con una capacidad de 1000 instancias._

**3. ¿Cuál es el propósito del *Health Probe*?**

_El proposito del Healt Probe es informar al balanceador de carga que instancias en el back-end pool estan en un estado adecuado para recibir una peticion, y asi verificar que ninguna sonda falle, ya que si falla el balanceador de carga detiene el flujo hacia estas instancias._

**4. ¿Cuál es el propósito de la *Load Balancing Rule*? ¿Qué tipos de sesión persistente existen, por qué esto es importante y cómo puede afectar la escalabilidad del sistema?.**

_El propósito de las reglas del balanciador de carga es llevar a cabo su principal funcionalidad, es decir especificar cuando se crea una nueva instancia de acuerdo a la cantidad de flujo que haya en la red y asi poder distribuir de manera eficiente las solicitudes entre las maquinas._

**5. ¿Qué es una *Virtual Network*? ¿Qué es una *Subnet*? ¿Para qué sirven los *address space* y *address range*?**

_**Virtua Network:** Es la capacidad de los usuarios para comunicarse de forma transparente local y remotamente a través de redes similares y diferentes mediante una interfaz de usuario simple y consistente._

_**Subnet:** Una subred es un rango de direcciones lógicas. es muy util utilizarlas cuando las redes se vulven demasiado grandes y es optimo dividirlas en subredes._

_**Address Space:** Es la cantidad de memoria asignada para todas las direcciones posibles para una entidad computacional, tambien se dice que un espacio de direcciones puede referirse a un rango de direcciones físicas o virtuales accesibles para un procesador o reservadas para un proceso._

_**Address Range:** Es el numero que indica cuantas direcciones tenemos en ese espacio de direcciones y depende de la cantidad de recursos que se necesiten en la red virtual, el rango sera mayor o menor._

**6. ¿Qué son las *Availability Zone* y por qué seleccionamos 3 diferentes zonas?. ¿Qué significa que una IP sea *zone-redundant*?**

 * _**Availability Zones:** Son ubicaciones físicas únicas dentro de una región de Azure. Cada zona está compuesta por uno o más centros de datos equipados con alimentación, refrigeración y redes independientes, para garantizar la resistencia._
 
 * _Se seleccionan tres zonas diferentes ya que protege las aplicaciones y los datos de fallas del centro de datos._
 
 * _Una **IP zone-redundant**, es una ip que esta replicada en varias zonas de disponibilidad._

**7. ¿Cuál es el propósito del *Network Security Group*?**

_El propósito principal de un grupo de seguridad de red es configurar las reglas de seguridad que permiten o prohíben el tráfico de red entrante o el tráfico de red saliente de varios tipos de recursos de Azure._

**8. Informe de newman 1 (Punto 2)**

Al realizar las pruebas se presentaron algunos fallos igual que en la parte 1, pero igualmente se ven que puede manejar una gran cantidad de peticiones exitosas gracias al equilibrador de carga.

![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/2a.png)

![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/2b.png)

![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/2c.png)

![Imágen 2](https://github.com/JonatanGonzalez09/ARSW-Lab8/blob/master/images/part1/2d.png)


**9. Presente el Diagrama de Despliegue de la solución.**


### Dependencias
* Cree una cuenta gratuita dentro de Azure. Para hacerlo puede guiarse de esta [documentación](https://azure.microsoft.com/en-us/free/search/?&ef_id=Cj0KCQiA2ITuBRDkARIsAMK9Q7MuvuTqIfK15LWfaM7bLL_QsBbC5XhJJezUbcfx-qAnfPjH568chTMaAkAsEALw_wcB:G:s&OCID=AID2000068_SEM_alOkB9ZE&MarinID=alOkB9ZE_368060503322_%2Bazure_b_c__79187603991_kwd-23159435208&lnkd=Google_Azure_Brand&dclid=CjgKEAiA2ITuBRDchty8lqPlzS4SJAC3x4k1mAxU7XNhWdOSESfffUnMNjLWcAIuikQnj3C4U8xRG_D_BwE). Al hacerlo usted contará con $200 USD para gastar durante 1 mes.

### Parte 0 - Entendiendo el escenario de calidad

Adjunto a este laboratorio usted podrá encontrar una aplicación totalmente desarrollada que tiene como objetivo calcular el enésimo valor de la secuencia de Fibonnaci.

**Escalabilidad**
Cuando un conjunto de usuarios consulta un enésimo número (superior a 1000000) de la secuencia de Fibonacci de forma concurrente y el sistema se encuentra bajo condiciones normales de operación, todas las peticiones deben ser respondidas y el consumo de CPU del sistema no puede superar el 70%.

### Parte 1 - Escalabilidad vertical

1. Diríjase a el [Portal de Azure](https://portal.azure.com/) y a continuación cree una maquina virtual con las características básicas descritas en la imágen 1 y que corresponden a las siguientes:
    * Resource Group = SCALABILITY_LAB
    * Virtual machine name = VERTICAL-SCALABILITY
    * Image = Ubuntu Server 
    * Size = Standard B1ls
    * Username = scalability_lab
    * SSH publi key = Su llave ssh publica

![Imágen 1](images/part1/part1-vm-basic-config.png)

2. Para conectarse a la VM use el siguiente comando, donde las `x` las debe remplazar por la IP de su propia VM.

    `ssh scalability_lab@xxx.xxx.xxx.xxx`

3. Instale node, para ello siga la sección *Installing Node.js and npm using NVM* que encontrará en este [enlace](https://linuxize.com/post/how-to-install-node-js-on-ubuntu-18.04/).
4. Para instalar la aplicación adjunta al Laboratorio, suba la carpeta `FibonacciApp` a un repositorio al cual tenga acceso y ejecute estos comandos dentro de la VM:

    `git clone <your_repo>`

    `cd <your_repo>/FibonacciApp`

    `npm install`

5. Para ejecutar la aplicación puede usar el comando `npm FibinacciApp.js`, sin embargo una vez pierda la conexión ssh la aplicación dejará de funcionar. Para evitar ese compartamiento usaremos *forever*. Ejecute los siguientes comando dentro de la VM.

    `npm install forever -g`

    `forever start FibinacciApp.js`

6. Antes de verificar si el endpoint funciona, en Azure vaya a la sección de *Networking* y cree una *Inbound port rule* tal como se muestra en la imágen. Para verificar que la aplicación funciona, use un browser y user el endpoint `http://xxx.xxx.xxx.xxx:3000/fibonacci/6`. La respuesta debe ser `The answer is 8`.

![](images/part1/part1-vm-3000InboudRule.png)

7. La función que calcula en enésimo número de la secuencia de Fibonacci está muy mal construido y consume bastante CPU para obtener la respuesta. Usando la consola del Browser documente los tiempos de respuesta para dicho endpoint usando los siguintes valores:
    * 1000000
    * 1010000
    * 1020000
    * 1030000
    * 1040000
    * 1050000
    * 1060000
    * 1070000
    * 1080000
    * 1090000    

8. Dírijase ahora a Azure y verifique el consumo de CPU para la VM. (Los resultados pueden tardar 5 minutos en aparecer).

![Imágen 2](images/part1/part1-vm-cpu.png)

9. Ahora usaremos Postman para simular una carga concurrente a nuestro sistema. Siga estos pasos.
    * Instale newman con el comando `npm install newman -g`. Para conocer más de Newman consulte el siguiente [enlace](https://learning.getpostman.com/docs/postman/collection-runs/command-line-integration-with-newman/).
    * Diríjase hasta la ruta `FibonacciApp/postman` en una maquina diferente a la VM.
    * Para el archivo `[ARSW_LOAD-BALANCING_AZURE].postman_environment.json` cambie el valor del parámetro `VM1` para que coincida con la IP de su VM.
    * Ejecute el siguiente comando.

    ```
    newman run ARSW_LOAD-BALANCING_AZURE.postman_collection.json -e [ARSW_LOAD-BALANCING_AZURE].postman_environment.json -n 10 &
    newman run ARSW_LOAD-BALANCING_AZURE.postman_collection.json -e [ARSW_LOAD-BALANCING_AZURE].postman_environment.json -n 10
    ```

10. La cantidad de CPU consumida es bastante grande y un conjunto considerable de peticiones concurrentes pueden hacer fallar nuestro servicio. Para solucionarlo usaremos una estrategia de Escalamiento Vertical. En Azure diríjase a la sección *size* y a continuación seleccione el tamaño `B2ms`.

![Imágen 3](images/part1/part1-vm-resize.png)

11. Una vez el cambio se vea reflejado, repita el paso 7, 8 y 9.
12. Evalue el escenario de calidad asociado al requerimiento no funcional de escalabilidad y concluya si usando este modelo de escalabilidad logramos cumplirlo.
13. Vuelva a dejar la VM en el tamaño inicial para evitar cobros adicionales.

**Preguntas**

1. ¿Cuántos y cuáles recursos crea Azure junto con la VM?
2. ¿Brevemente describa para qué sirve cada recurso?
3. ¿Al cerrar la conexión ssh con la VM, por qué se cae la aplicación que ejecutamos con el comando `npm FibonacciApp.js`? ¿Por qué debemos crear un *Inbound port rule* antes de acceder al servicio?
4. Adjunte tabla de tiempos e interprete por qué la función tarda tando tiempo.
5. Adjunte imágen del consumo de CPU de la VM e interprete por qué la función consume esa cantidad de CPU.
6. Adjunte la imagen del resumen de la ejecución de Postman. Interprete:
    * Tiempos de ejecución de cada petición.
    * Si hubo fallos documentelos y explique.
7. ¿Cuál es la diferencia entre los tamaños `B2ms` y `B1ls` (no solo busque especificaciones de infraestructura)?
8. ¿Aumentar el tamaño de la VM es una buena solución en este escenario?, ¿Qué pasa con la FibonacciApp cuando cambiamos el tamaño de la VM?
9. ¿Qué pasa con la infraestructura cuando cambia el tamaño de la VM? ¿Qué efectos negativos implica?
10. ¿Hubo mejora en el consumo de CPU o en los tiempos de respuesta? Si/No ¿Por qué?
11. Aumente la cantidad de ejecuciones paralelas del comando de postman a `4`. ¿El comportamiento del sistema es porcentualmente mejor?

### Parte 2 - Escalabilidad horizontal

#### Crear el Balanceador de Carga

Antes de continuar puede eliminar el grupo de recursos anterior para evitar gastos adicionales y realizar la actividad en un grupo de recursos totalmente limpio.

1. El Balanceador de Carga es un recurso fundamental para habilitar la escalabilidad horizontal de nuestro sistema, por eso en este paso cree un balanceador de carga dentro de Azure tal cual como se muestra en la imágen adjunta.

![](images/part2/part2-lb-create.png)

2. A continuación cree un *Backend Pool*, guiese con la siguiente imágen.

![](images/part2/part2-lb-bp-create.png)

3. A continuación cree un *Health Probe*, guiese con la siguiente imágen.

![](images/part2/part2-lb-hp-create.png)

4. A continuación cree un *Load Balancing Rule*, guiese con la siguiente imágen.

![](images/part2/part2-lb-lbr-create.png)

5. Cree una *Virtual Network* dentro del grupo de recursos, guiese con la siguiente imágen.

![](images/part2/part2-vn-create.png)

#### Crear las maquinas virtuales (Nodos)

Ahora vamos a crear 3 VMs (VM1, VM2 y VM3) con direcciones IP públicas standar en 3 diferentes zonas de disponibilidad. Después las agregaremos al balanceador de carga.

1. En la configuración básica de la VM guíese por la siguiente imágen. Es importante que se fije en la "Avaiability Zone", donde la VM1 será 1, la VM2 será 2 y la VM3 será 3.

![](images/part2/part2-vm-create1.png)

2. En la configuración de networking, verifique que se ha seleccionado la *Virtual Network*  y la *Subnet* creadas anteriormente. Adicionalmente asigne una IP pública y no olvide habilitar la redundancia de zona.

![](images/part2/part2-vm-create2.png)

3. Para el Network Security Group seleccione "avanzado" y realice la siguiente configuración. No olvide crear un *Inbound Rule*, en el cual habilite el tráfico por el puerto 3000. Cuando cree la VM2 y la VM3, no necesita volver a crear el *Network Security Group*, sino que puede seleccionar el anteriormente creado.

![](images/part2/part2-vm-create3.png)

4. Ahora asignaremos esta VM a nuestro balanceador de carga, para ello siga la configuración de la siguiente imágen.

![](images/part2/part2-vm-create4.png)

5. Finalmente debemos instalar la aplicación de Fibonacci en la VM. para ello puede ejecutar el conjunto de los siguientes comandos, cambiando el nombre de la VM por el correcto

```
git clone https://github.com/daprieto1/ARSW_LOAD-BALANCING_AZURE.git

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
source /home/vm1/.bashrc
nvm install node

cd ARSW_LOAD-BALANCING_AZURE/FibonacciApp
npm install

npm install forever -g
forever start FibonacciApp.js
```

Realice este proceso para las 3 VMs, por ahora lo haremos a mano una por una, sin embargo es importante que usted sepa que existen herramientas para aumatizar este proceso, entre ellas encontramos Azure Resource Manager, OsDisk Images, Terraform con Vagrant y Paker, Puppet, Ansible entre otras.

#### Probar el resultado final de nuestra infraestructura

1. Porsupuesto el endpoint de acceso a nuestro sistema será la IP pública del balanceador de carga, primero verifiquemos que los servicios básicos están funcionando, consuma los siguientes recursos:

```
http://52.155.223.248/
http://52.155.223.248/fibonacci/1
```

2. Realice las pruebas de carga con `newman` que se realizaron en la parte 1 y haga un informe comparativo donde contraste: tiempos de respuesta, cantidad de peticiones respondidas con éxito, costos de las 2 infraestrucruras, es decir, la que desarrollamos con balanceo de carga horizontal y la que se hizo con una maquina virtual escalada.

3. Agregue una 4 maquina virtual y realice las pruebas de newman, pero esta vez no lance 2 peticiones en paralelo, sino que incrementelo a 4. Haga un informe donde presente el comportamiento de la CPU de las 4 VM y explique porque la tasa de éxito de las peticiones aumento con este estilo de escalabilidad.

```
newman run ARSW_LOAD-BALANCING_AZURE.postman_collection.json -e [ARSW_LOAD-BALANCING_AZURE].postman_environment.json -n 10 &
newman run ARSW_LOAD-BALANCING_AZURE.postman_collection.json -e [ARSW_LOAD-BALANCING_AZURE].postman_environment.json -n 10 &
newman run ARSW_LOAD-BALANCING_AZURE.postman_collection.json -e [ARSW_LOAD-BALANCING_AZURE].postman_environment.json -n 10 &
newman run ARSW_LOAD-BALANCING_AZURE.postman_collection.json -e [ARSW_LOAD-BALANCING_AZURE].postman_environment.json -n 10
```

**Preguntas**

* ¿Cuáles son los tipos de balanceadores de carga en Azure y en qué se diferencian?, ¿Qué es SKU, qué tipos hay y en qué se diferencian?, ¿Por qué el balanceador de carga necesita una IP pública?
* ¿Cuál es el propósito del *Backend Pool*?
* ¿Cuál es el propósito del *Health Probe*?
* ¿Cuál es el propósito de la *Load Balancing Rule*? ¿Qué tipos de sesión persistente existen, por qué esto es importante y cómo puede afectar la escalabilidad del sistema?.
* ¿Qué es una *Virtual Network*? ¿Qué es una *Subnet*? ¿Para qué sirven los *address space* y *address range*?
* ¿Qué son las *Availability Zone* y por qué seleccionamos 3 diferentes zonas?. ¿Qué significa que una IP sea *zone-redundant*?
* ¿Cuál es el propósito del *Network Security Group*?
* Informe de newman 1 (Punto 2)
* Presente el Diagrama de Despliegue de la solución.





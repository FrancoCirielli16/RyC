1. ¿Qué servicios presta la capa de red? ¿Cuál es la PDU en esta capa? ¿Qué dispositivo es considerado sólo de la capa de red?

### **Servicios de la Capa de Red:**

La capa de red (Capa 3 del modelo OSI) proporciona los siguientes servicios principales:

1. **Enrutamiento (Routing):** Determina la mejor ruta para enviar paquetes desde el origen al destino a través de diferentes redes.
2. **Direccionamiento Lógico:** Asigna direcciones IP (IPv4 o IPv6) para identificar dispositivos en una red.
3. **Fragmentación y Reensamblado:** Divide paquetes en unidades más pequeñas si es necesario (por limitaciones de la capa de enlace) y los reensambla en el destino.
4. **Control de Congestión:** Regula el flujo de datos para evitar saturación en la red.

### **PDU (Unidad de Datos de Protocolo) de la Capa de Red:**

La PDU de esta capa es el **paquete** (por ejemplo, un paquete IP en redes TCP/IP).

### **Dispositivo Exclusivo de la Capa de Red:**

El **enrutador (router)** es el dispositivo principal que opera exclusivamente en la capa de red, ya que su función principal es el enrutamiento de paquetes entre redes diferentes.


2. ¿Por qué se lo considera un protocolo de mejor esfuerzo?

El protocolo IP (**Internet Protocol**) es considerado de **"mejor esfuerzo" (best-effort delivery)** porque no garantiza la entrega confiable de los paquetes, ni su orden correcto, ni la ausencia de duplicados. Su funcionamiento se basa en intentar entregar los datos de la mejor manera posible, pero sin asegurar resultados.

### **Razones por las que IP es "best-effort":**

1. **Sin confirmación de entrega:**
    - IP no tiene mecanismos para confirmar si un paquete llegó a su destino (a diferencia de TCP, que sí lo hace).
2. **Sin control de flujo ni congestión:**
    - No regula la velocidad de transmisión para evitar saturación en la red.
3. **Sin reenvío automático de paquetes perdidos:**
    - Si un paquete se pierde, IP no lo retransmite (eso lo hace TCP en una capa superior si es necesario).
4. **Paquetes pueden llegar desordenados o duplicados:**
    - No garantiza el orden de llegada ni evita duplicados (esto lo manejan protocolos como TCP si es necesario).
5. **Sin garantía de calidad de servicio (QoS) nativa:**
    - IP trata todos los paquetes por igual, a menos que se usen extensiones como **DiffServ** o **MPLS**.

3. ¿Cuántas redes clase A, B y C hay? ¿Cuántos hosts como máximo pueden tener cada
una?

En el esquema de direccionamiento **clase A, B y C** (hoy obsoleto, reemplazado por CIDR), las redes y hosts se definían así:

---

### **1. Número de redes por clase:**

| **Clase** | **Rango del primer octeto** | **Número de redes** |
| --- | --- | --- |
| **A** | 1.0.0.0 – 126.0.0.0 | **126 redes** |
| **B** | 128.0.0.0 – 191.255.0.0 | **16,384 redes** |
| **C** | 192.0.0.0 – 223.255.255.0 | **2,097,152 redes** |


**Notas:**

- **Clase A:** El primer octeto va de **1 a 126** (0.0.0.0 y 127.0.0.0 están reservados).
- **Clase B:** Se usan los primeros dos octetos (rango del primer octeto: 128–191).
- **Clase C:** Se usan los primeros tres octetos (rango del primer octeto: 192–223).


4. ¿Qué son las subredes? ¿Por qué es importante siempre especificar la máscara de
subred asociada?

¿Qué son las subredes?
Una subred (subnetwork) es una división lógica de una red IP más grande. Se crea para:

Optimizar el tráfico: Limitar el alcance de las transmisiones broadcast (evitando congestión).

Mejorar la seguridad: Aislar segmentos sensibles (ej: finanzas vs. personal).

Organizar jerárquicamente: Agrupar dispositivos por ubicación/función (ej: piso 1, servidores).

Reducir desperdicio de direcciones: Asignar bloques IP ajustados al tamaño real de cada segmento.

Ejemplo:
La red 192.168.0.0/16 (65,534 hosts) puede dividirse en subredes como:

192.168.1.0/24 (254 hosts para oficina).

192.168.2.0/24 (254 hosts para servidores).


🔍 ¿Cómo funcionan?
Máscara de subred: Define qué parte de una IP es la red y qué parte es el host.
Ej: Máscara 255.255.255.0 (/24) en 192.168.1.10 indica:

Red: 192.168.1 (primeros 24 bits).

Host: 10 (últimos 8 bits).



5. ¿Cuál es la finalidad del campo Protocol en la cabecera IP? ¿A qué campos de la capa
de transporte se asemeja en su funcionalidad?

El campo **Protocol** (8 bits) en la cabecera IPv4 (o el campo **Next Header** en IPv6) identifica **qué protocolo de capa superior está encapsulado en el paquete IP**. Su propósito es permitir que el dispositivo receptor sepa cómo procesar los datos:

- **Ejemplos comunes:**
    - **TCP** (valor `6`).
    - **UDP** (valor `17`).
    - **ICMP** (valor `1`).
    - **IGMP** (valor `2`).

**Funcionalidad clave:**

- **Demultiplexación:** Indica al sistema operativo del destino qué protocolo de la capa de transporte (TCP, UDP, etc.) o de otra capa (ej: ICMP) debe recibir el paquete.
- **Sin este campo**, el receptor no sabría si el payload es un segmento TCP, un datagrama UDP, o un mensaje de control como ICMP.

### **2. Campos de la capa de transporte con funcionalidad similar:**

El campo **Protocol** de la capa de red se asemeja a los campos **Puerto de destino** en los encabezados de **TCP** y **UDP**, ya que ambos sirven para:

| **Capa** | **Campo** | **Propósito** |
| --- | --- | --- |
| **Red (IP)** | Protocol | Identifica el protocolo de capa superior (TCP, UDP, etc.). |
| **Transporte** | Puerto de destino | Identifica la aplicación o servicio específico que debe recibir los datos. |

**Analogía:**

- El campo **Protocol** dirige el paquete a la capa de transporte correcta (TCP/UDP/ICMP).
- Los **puertos de destino** en TCP/UDP dirigen los datos a la aplicación correcta (ej: HTTP en puerto 80, DNS en puerto 53).




División en subredes
6. Para cada una de las siguientes direcciones IP (172.16.58.223/26, 163.10.5.49/27,
128.10.1.0/23, 10.1.0.0/24, 8.40.11.179/12) determine:
a. ¿De qué clase de red es la dirección dada (Clase A, B o C)?
b. ¿Cuál es la dirección de subred?
c. ¿Cuál es la cantidad máxima de hosts que pueden estar en esa subred?
d. ¿Cuál es la dirección de broadcast de esa subred?
e. ¿Cuál es el rango de direcciones IP válidas dentro de la subred?
7. Su organización cuenta con la dirección 128.50.10.0. Indique:
a. ¿Es una dirección de red o de host?
b. Clase a la que pertenece y máscara de clase.
c. Cantidad de hosts posibles.
d. Se necesitan crear, al menos, 513 subredes. Indique:
i. Máscara necesaria.
ii. Cantidad de redes asignables.
iii. Cantidad de hosts por subred.
iv. Dirección de la subred 710.
v. Dirección de broadcast de la subred 710.
8. Si usted estuviese a cargo de la administración del bloque IP 195.200.45.0/24
a. ¿Qué máscara utilizaría si necesita definir al menos 9 subredes?
1
Redes y Comunicaciones LINTI - UNLP
b. Indique la dirección de subred de las primeras 9 subredes.
c. Seleccione una e indique dirección de broadcast y rango de direcciones asignables
en esa subred.
9. Dado el siguiente gráfico:
a. Verifique si es correcta la asignación de direcciones IP y, en caso de no serlo,
modifique la misma para que lo sea.
b. ¿Cuántos bits se tomaron para hacer subredes en la red 10.0.10.0/24? ¿Cuántas
subredes se podrían generar?
c. Para cada una de las redes utilizadas indique si son públicas o privadas.
CIDR
10. ¿Qué es CIDR (Class Interdomain routing)? ¿Por qué resulta útil?
11. ¿Cómo publicaría un router las siguientes redes si se aplica CIDR?
a. 198.10.1.0/24
b. 198.10.0.0/24
c. 198.10.3.0/24
d. 198.10.2.0/24
2
Redes y Comunicaciones LINTI - UNLP
12. Listar las redes involucradas en los siguientes bloques CIDR:
● 200.56.168.0/21
● 195.24.0.0/13
● 195.24/13
13. El bloque CIDR 128.0.0.0/2 o 128/2, ¿Equivale a listar todas las direcciones de red de
clase B? ¿Cuál sería el bloque CIDR que agrupa todas las redes de clase A?
VLSM
14. ¿Qué es y para qué se usa VLSM?
15. Describa, con sus palabras, el mecanismo para dividir subredes utilizando VLSM.
16. Suponga que trabaja en una organización que tiene la red que se ve en el gráfico y debe
armar el direccionamiento para la misma, minimizando el desperdicio de direcciones IP.
Dicha organización posee la red 205.10.192.0/19, que es la que usted deberá utilizar.
a. ¿Es posible asignar las subredes correspondientes a la topología utilizando
subnetting sin VLSM? Indique la cantidad de hosts que se desperdicia en cada
subred.
b. Asigne direcciones a todas las redes de la topología. Tome siempre en cada paso la
primera dirección de red posible.
c. Para mantener el orden y el inventario de direcciones disponibles, haga un listado de
todas las direcciones libres que le quedaron, agrupándolas utilizando CIDR.
d. Asigne direcciones IP a todas las interfaces de la topología que sea posible.
3
Redes y Comunicaciones LINTI - UNLP
17. Utilizando la siguiente topología y el bloque asignado, arme el plan de direccionamiento
IPv4 teniendo en cuenta las siguientes restricciones:
a. Utilizar el bloque IPv4 200.100.8.0/22.
b. La red A tiene 125 hosts y se espera un crecimiento máximo de 20 hosts.
c. La red X tiene 63 hosts.
d. La red B cuenta con 60 hosts
e. La red Y tiene 46 hosts y se espera un crecimiento máximo de 18 hosts.
f. En cada red, se debe desperdiciar la menor cantidad de direcciones IP posibles. En
este sentido, las redes utilizadas para conectar los routers deberán utilizar
segmentos de red /30 de modo de desperdiciar la menor cantidad posible de
direcciones IP.
18. Asigne direcciones IP en los equipos de la topología según el plan anterior.
ICMP y Configuraciones IP
19. Describa qué es y para qué sirve el protocolo ICMP.
a. Analice cómo funciona el comando ping.
i. Indique el tipo y código ICMP que usa el ping.
ii. Indique el tipo y código ICMP que usa la respuesta de un ping.
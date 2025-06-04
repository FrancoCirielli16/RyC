1. ¿Cuál es el puerto por defecto que se utiliza en los siguientes servicios?
Web / SSH / DNS / Web Seguro / POP3 / IMAP / SMTP
Investigue en qué lugar en Linux y en Windows está descrita la asociación utilizada por
defecto para cada servicio.

| Servicio | Puerto por defecto | Protocolo |
| --- | --- | --- |
| Web (HTTP) | 80 | TCP |
| SSH | 22 | TCP |
| DNS | 53 | UDP/TCP |
| Web Seguro (HTTPS) | 443 | TCP |
| POP3 | 110 | TCP |
| IMAP | 143 | TCP |
| SMTP | 25 (o 587 para envío seguro) | TCP |

¿Dónde están descritas estas asociaciones por defecto?
🐧 En Linux:
Estas asociaciones están definidas en el archivo:
/etc/services

​
Este archivo contiene una lista de servicios conocidos con sus puertos y protocolos asociados. Por ejemplo, si haces:
grep ssh /etc/services

​
Verás una línea como:
ssh             22/tcp

### **En Windows:**

En Windows, las asociaciones de puertos por defecto no están centralizadas en un solo archivo como en Linux, pero puedes consultarlas de estas formas:

1. **Archivo equivalente:**
    
    ```
    C:\Windows\System32\drivers\etc\services
    
    ```
    
    Este archivo es muy similar al de Linux y también incluye asignaciones de servicios a puertos.
    
2. **Registro del sistema (opcionalmente modificable):**
    
    Algunas configuraciones específicas pueden estar en el registro, pero el archivo `services` es la fuente estándar.

2. Investigue qué es multicast. ¿Sobre cuál de los protocolos de capa de transporte
funciona? ¿Se podría adaptar para que funcione sobre el otro protocolo de capa de
transporte? ¿Por qué?

**Multicast** es un método de transmisión de datos en redes IP donde un emisor envía un solo paquete que puede ser recibido por múltiples destinatarios **interesados** (es decir, que se han suscrito al grupo multicast). A diferencia de:

- **Unicast**: uno a uno (emisor a un solo receptor).
- **Broadcast**: uno a todos (emisor a todos los nodos de la red local).
- **Multicast**: uno a muchos, pero solo a los que lo han solicitado.

Este enfoque es **eficiente**, ya que **no duplica paquetes** para cada receptor, sino que el paquete viaja una sola vez hasta que se bifurca lo necesario cerca de los destinatarios.

3. Investigue cómo funciona el protocolo de aplicación FTP teniendo en cuenta las
diferencias en su funcionamiento cuando se utiliza el modo activo de cuando se utiliza el
modo pasivo ¿En qué se diferencian estos tipos de comunicaciones del resto de los
protocolos de aplicación vistos?

**FTP (File Transfer Protocol)** es un protocolo de **aplicación** diseñado para transferir archivos entre un cliente y un servidor. Usa una arquitectura cliente-servidor y opera sobre **TCP/IP**.

Una particularidad clave de FTP frente a otros protocolos de aplicación es que **usa dos conexiones TCP separadas**:

1. **Conexión de control** (puerto 21, iniciada por el cliente): para comandos (login, cambiar de directorio, etc.).
2. **Conexión de datos**: para transferir archivos (puerto y dirección dependen del modo: activo o pasivo).

---

### Modos de funcionamiento: **Activo vs Pasivo**

### Modo **activo** (Active Mode):

- **Cliente inicia** la conexión de control al **puerto 21** del servidor.
- Luego, **el cliente abre un puerto aleatorio** y espera la conexión de datos.
- El cliente **envía el número de puerto al servidor** (con el comando `PORT`).
- **El servidor inicia la conexión de datos desde su puerto 20** hacia ese puerto del cliente.

Problema:

- Este modo suele fallar si el cliente está detrás de un **firewall o NAT**, que bloquea conexiones entrantes.

---

### Modo **pasivo** (Passive Mode):

- **Cliente inicia** la conexión de control al **puerto 21** del servidor.
- Luego, envía un comando `PASV`.
- El **servidor abre un puerto aleatorio** y le comunica al cliente qué puerto usar.
- **El cliente inicia la conexión de datos** a ese puerto.

Ventaja:

- Este modo **funciona mejor con firewalls y NAT**, ya que **el cliente inicia ambas conexiones** (control y datos).

###  ¿En qué se diferencia FTP de otros protocolos de aplicación?

| Característica | FTP | HTTP / SMTP / POP3 / IMAP / SSH |
| --- | --- | --- |
| Número de conexiones TCP | 2 (control + datos) | 1 |
| Puertos | 21 (control) + 20/pasivo (datos) | Normalmente solo uno |
| Quién inicia la conexión de datos | Servidor (modo activo) o cliente (modo pasivo) | Siempre el cliente |
| Compatibilidad con firewalls | Complicada en modo activo | Generalmente buena |


### Resumen:

- **FTP usa dos conexiones TCP**, a diferencia de otros protocolos que usan solo una.
- En **modo activo**, el servidor inicia la conexión de datos → puede fallar con firewalls/NAT.
- En **modo pasivo**, el cliente inicia ambas conexiones → más compatible con redes modernas.

4. Suponiendo Selective Repeat; tamaño de ventana 4 y sabiendo que E indica que el mensaje llegó con errores. Indique en el siguiente gráfico, la numeración de los ACK que el host B envía al Host A.

![a](./image%20(4).webp)


##  ¿Qué es Selective Repeat?
**Selective Repeat** es un protocolo de control de errores en la capa de transporte. Se usa para garantizar la **entrega confiable y en orden** de datos entre dos dispositivos en una red, incluso si algunos paquetes se pierden o llegan fuera de orden.

## ¿Qué problema soluciona?

En redes reales, los paquetes:

- pueden **llegar desordenados**
- pueden **perderse**
- pueden **llegar dañados**

Selective Repeat se encarga de:

- **retransmitir solo los paquetes dañados o perdidos**,
- y **almacenar los paquetes que llegaron fuera de orden** hasta que puedan reordenarse.

## ¿Qué es una ventana deslizante?

Una **ventana** representa el **rango de paquetes** que se pueden enviar (en el emisor) o recibir (en el receptor) **sin necesidad de confirmación inmediata**.

### 🔹 En el **emisor**:

- Tiene una **ventana de envío** que abarca N paquetes (por ejemplo, del 0 al 3 si N=4).
- Puede enviar todos esos paquetes sin esperar ACKs.
- Cuando recibe un ACK, **corre la ventana** hacia adelante.

### 🔹 En el **receptor**:

- Tiene una **ventana de recepción** también de tamaño N.
- Puede **aceptar paquetes fuera de orden** dentro de esa ventana.
- Los **almacena temporalmente**, y **envía ACKs por cada uno**.
- Entrega los datos al usuario **solo en orden**.

Y empieza a enviar:

- Envía 0 → receptor recibe → ACK 0
- Envía 1 → receptor recibe → ACK 1
- Envía 2 → ❌ se pierde o llega dañado → NO hay ACK
- Envía 3 → receptor recibe → **ACK 3 (sí, aunque el 2 falló)**

El receptor **almacena** el 3, aunque no tiene el 2 todavía.

Cuando el emisor detecta el **timeout del 2**, lo **reenvía**:

- Receptor recibe el 2 → ahora tiene 2 y 3 → los puede entregar en orden
- Envía **ACK 2**

## ¿Cómo se diferencia de otros protocolos?

| Protocolo | ACKs por cada paquete | Permite paquetes fuera de orden | Reenvía solo paquetes con error |
| --- | --- | --- | --- |
| Stop & Wait | Sí | No | Sí (pero solo uno a la vez) |
| Go-Back-N | Solo por último correcto | No | No (reenvía todo desde el error) |
| Selective Repeat | Sí | Sí | Sí |

![b](./image%20(5).webp)

5. ¿Qué restricción existe sobre el tamaño de ventanas en el protocolo Selective Repeat?


En el protocolo **Selective Repeat (SR)**, la **restricción principal sobre el tamaño de la ventana** está relacionada con el **número de secuencias posibles** para evitar ambigüedades en la recepción de tramas.

### Restricción:

> El tamaño de la ventana (W) debe ser menor o igual a la mitad del número total de números de secuencia posibles (N):
> 

### ¿Por qué?

Porque en Selective Repeat, tanto el emisor como el receptor mantienen ventanas, y las tramas se pueden recibir fuera de orden. Si el tamaño de la ventana fuera mayor que N/2, el receptor podría confundir tramas nuevas con tramas viejas debido al **reuso de números de secuencia** (ya que estos se reciclan cuando se llega a N).


6. De acuerdo a la captura TCP de la siguiente figura, indique los valores de los campos borroneados.

![c](./image%20(6).webp)

## **¿Qué es un Handshake TCP?**

Es un "apretón de manos" en 3 pasos que hace tu computadora (cliente) para conectarse a un servidor (por ejemplo, una página web). Los pasos son:

1. **SYN** → Cliente inicia la conexión.
2. **SYN-ACK** → Servidor responde aceptando.
3. **ACK** → Cliente confirma y se establece la conexión.

---

## **2. Explicación de tus Paquetes**

### **📦 Paquete 1 (Cliente → Servidor) - SYN**

- **Origen:** **`172.20.1.1`** (tu computadora).
- **Destino:** **`172.20.1.100`** (un servidor, como una web).
- **Protocolo:** TCP (el protocolo de conexión confiable).
- **Info:**
    - **`41749 > vce`** → Puerto **`41749`** (cliente) se conecta al puerto **`vce`** (11111, servidor).
    - **`[SYN]`** → Significa *"Hola, ¿podemos hablar?"*.
    - **`Seq=3933822137`** → Número de secuencia inicial (como un ID de la conversación).
    - **`Win=5840`** → Tamaño del buffer de recepción (cuántos datos puede aceptar tu PC).
    - **`TSval=270132`** → Marca de tiempo (timestamp) de tu computadora.

---

### **📦 Paquete 2 (Servidor → Cliente) - SYN-ACK**

- **Origen:** **`172.20.1.100`** (el servidor).
- **Destino:** **`172.20.1.1`** (tu PC).
- **Info:**
    - **`[SYN, ACK]`** → *"¡Hola! Recibí tu SYN, aquí está mi SYN y ACK de confirmación."*
    - **`Seq=1047471501`** → Número de secuencia del servidor.
    - **`Ack=3933822138`** → *"Recibí tu Seq (**`3933822137`**) y espero el siguiente byte (**`+1`**)."*
    - **`Win=5792`** → Tamaño de ventana del servidor.
    - **`TSval=1877442`** → Hora actual del servidor.
    - **`TSecr=270132`** → Refleja el timestamp que tú enviaste (para sincronización).

---

### **📦 Paquete 3 (Cliente → Servidor) - ACK**

- **Origen:** **`172.20.1.1`** (tu PC).
- **Destino:** **`172.20.1.100`** (servidor).
- **Info:**
    - **`[ACK]`** → *"¡Perfecto, conexión establecida!"*
    - **`Seq=3933822138`** → *"Ahora voy a enviar datos desde este número."*
    - **`Ack=1047471502`** → *"Recibí tu Seq (**`1047471501`**) y espero el siguiente byte (**`+1`**)."*
    - **`Win=5888`** → Tamaño de ventana actualizado.
    - **`TSval=270132`** → Tu timestamp.
    - **`TSecr=1877442`** → Refleja el timestamp del servidor.

---

## **3. Resumen Gráfico**

```
1. Cliente (172.20.1.1)  → [SYN] → Servidor (172.20.1.100)
   - Seq=3933822137, Win=5840

2. Servidor → [SYN-ACK] → Cliente
   - Seq=1047471501, Ack=3933822138, Win=5792

3. Cliente → [ACK] → Servidor
   - Seq=3933822138, Ack=1047471502, Win=5888
```

✅ **¡Conexión establecida!** Ahora pueden intercambiar datos.

---

## **4. ¿Para qué sirve cada campo?**

| **Campo** | **Significado** |
| --- | --- |
| **SYN** | Inicia la conexión ("¿Podemos hablar?"). |
| **ACK** | Confirmación ("Recibí tus datos, espero el siguiente"). |
| **Seq** | Número de secuencia (lleva el control de los bytes enviados). |
| **Ack** | Número de confirmación (indica qué byte espera recibir). |
| **Win** | Tamaño de la ventana (cuántos datos puede recibir sin confirmación). |
| **TSval/TSecr** | Timestamps (para calcular retrasos y evitar paquetes duplicados). |

---

### **¿Por qué +1 en los ACK?**

Porque el **`ACK`** siempre confirma **el próximo byte que espera recibir**.

- Si envías **`Seq=100`**, el **`ACK`** será **`101`**.

## **¿Por qué el `Seq` del servidor (Paquete 2) es totalmente diferente al `Seq` del cliente (Paquete 1)?**

### **1. Los números de secuencia (Seq) son independientes en cada dirección**

- El **`Seq` del cliente** y el **`Seq` del servidor** son **generados por separado** y no tienen relación matemática entre sí.
- Cada dispositivo (cliente y servidor) elige un número de secuencia inicial (**ISN: Initial Sequence Number**) de forma aleatoria por seguridad.

### **2. ¿Cómo se generan estos números?**

- **Antes:** En el pasado, los sistemas usaban un contador simple (fácil de predecir y vulnerable a ataques).
- **Ahora:** Se generan de forma **pseudoaleatoria** (basados en hora del sistema + algoritmo criptográfico) para evitar:
    - Ataques de spoofing (suplantación de conexiones).
    - Paquetes maliciosos inyectados en la comunicación.

### **3. Ejemplo de tu captura**

| **Paquete** | **Dirección** | **Seq (Número de Secuencia)** | **Explicación** |
| --- | --- | --- | --- |
| 1 (SYN) | Cliente → Servidor | **`Seq=3933822137`** | Número aleatorio generado por el cliente. |
| 2 (SYN-ACK) | Servidor → Cliente | **`Seq=1047471501`** | Número aleatorio generado por el servidor. **No depende del Seq del cliente**. |
| 3 (ACK) | Cliente → Servidor | **`Seq=3933822138`** | **Sí depende del Seq inicial del cliente (`3933822137 + 1`)** porque confirma el SYN-ACK. |

---

### **4. ¿Qué sí está relacionado? El campo `Ack`**

Mientras que los **`Seq`** son independientes, los **`Ack` sí reflejan la secuencia recibida del otro dispositivo**:

- En el **Paquete 2 (SYN-ACK)**, el servidor confirma el **`Seq`** del cliente con:CopyDownload
    
    ```
    Ack = Seq_cliente + 1 = 3933822137 + 1 = 3933822138
    ```
    
- En el **Paquete 3 (ACK)**, el cliente confirma el **`Seq`** del servidor con:CopyDownload
    
    ```
    Ack = Seq_servidor + 1 = 1047471501 + 1 = 1047471502
    ```

![d](./image%20(7).webp)

7. Dada la sesión TCP de la figura, completar los valores marcados con un signo de
interrogación.

![e](./image%20(8).webp)

## **📌 Tabla Corregida (Versión Ideal)**

| Time | Origen | Tipo | Seq | Ack | Len | Comentario |
| --- | --- | --- | --- | --- | --- | --- |
| 1.360 | 10.0.0.10 | **SYN** | 0 | - | - | Cliente inicia conexión. Seq inicial = 0. |
| 1.360 | 10.0.1.10 | **SYN-ACK** | 0 | 1 | - | Servidor responde: *"Acepto. Mi Seq=0, espero tu Seq=1."* |
| 1.360 | 10.0.0.10 | **ACK** | 1 | 1 | - | Cliente confirma: *"Recibí tu SYN. Ahora enviaré datos desde Seq=1."* |
| 3.581 | 10.0.0.10 | **PSH, ACK** | 1 | 1 | 7 | Cliente envía **7 bytes** (ej: "HOLA"). Seq=1, Ack=1. |
| 3.581 | 10.0.1.10 | **ACK** | 1 | 8 | - | Servidor confirma: *"Recibí hasta Seq=1 + Len=7 → Espero Seq=8."* |
| 8.796 | 10.0.0.10 | **PSH, ACK** | 8 | 1 | 9 | Cliente envía **9 bytes más** (ej: "MUNDO"). Seq=8, Ack=1. |
| 8.797 | 10.0.1.10 | **ACK** | 1 | 17 | - | Servidor confirma: *"Recibí hasta Seq=8 + Len=9 → Espero Seq=17."* |
| 14.382 | 10.0.0.10 | **PSH, ACK** | 17 | 1 | 5 | Cliente envía **5 bytes** (ej: "TCP!"). Seq=17, Ack=1. |
| 14.382 | 10.0.1.10 | **ACK** | 1 | 22 | - | Servidor confirma: *"Recibí hasta Seq=17 + Len=5 → Espero Seq=22."* |
| 15.190 | 10.0.0.10 | **FIN, ACK** | 22 | 1 | - | Cliente cierra: *"Terminé. Último Seq=22."* |
| 15.190 | 10.0.1.10 | **FIN, ACK** | 1 | 23 | - | Servidor responde: *"Ok, cierro. Espero Seq=23."* |
| 15.190 | 10.0.0.10 | **ACK** | 23 | 2 | - | Cliente confirma cierre. |


8. ¿Qué es el RTT y cómo se calcula? Investigue la opción TCP timestamp y los campos
TSval y TSecr.

### **1. ¿Qué es el RTT (Round-Trip Time)?**

El **RTT** es el tiempo que tarda un paquete en ir desde el origen al destino **y volver** (incluyendo la confirmación). Es clave para:

- Optimizar la velocidad de transmisión TCP.
- Detectar pérdida de paquetes.
- Ajustar timeouts en la comunicación.

### **📌 Cálculo del RTT (sin timestamps)**

1. **Cliente** envía un paquete (ej: `SYN` o `PSH`) y registra el tiempo de envío (`T1`).
2. **Servidor** responde con un `ACK` (que confirma la recepción).
3. **Cliente** recibe el `ACK` y registra el tiempo (`T2`).
4. **RTT = T2 - T1**.

---

### **2. TCP Timestamp Option (Mejora del RTT)**

Para calcular el RTT con mayor precisión, TCP usa **timestamps** (opción definida en [RFC 1323](https://tools.ietf.org/html/rfc1323)). Cada paquete TCP incluye:

- **`TSval` (Timestamp Value)**: Hora actual del dispositivo que envía el paquete (en milisegundos o ticks de reloj).
- **`TSecr` (Timestamp Echo Reply)**: Refleja el último `TSval` recibido del otro extremo (o `0` si no hay timestamp previo).

### **📌 Campos en los paquetes TCP**

```
Opción TCP (12 bytes):
| Kind=8 | Length=10 | TSval (4 bytes) | TSecr (4 bytes) |

```

- **Ejemplo**:
    - Cliente envía `TSval=1000`, `TSecr=0` (primer paquete).
    - Servidor responde con `TSval=2000`, `TSecr=1000`.
    - Cliente calcula el RTT usando el `TSecr` reflejado.

---

### **3. Cálculo del RTT con Timestamps**

1. **Cliente** envía un paquete con:
    - `TSval = T1` (ej: `270132`).
    - `TSecr = 0` (si es el primer paquete).
2. **Servidor** responde con:
    - `TSval = T2` (su hora actual, ej: `1877442`).
    - `TSecr = T1` (refleja el `TSval` del cliente).
3. **Cliente** calcula el RTT al recibir el `ACK`:
    - **RTT = Tiempo actual - TSecr recibido**.
    - Ejemplo: Si el cliente recibe `TSecr=270132` y su hora actual es `270150` → **RTT = 18 ms**.

### **📌 Ventajas de usar timestamps**

- **Precisión**: No depende del reloj del sistema, sino de valores internos.
- **Protección contra wraparound**: Los números de secuencia de 32 bits pueden "dar la vuelta" en conexiones rápidas; los timestamps evitan confusiones.
- **Múltiples mediciones**: Permite calcular el RTT para cada `ACK`, no solo para el handshake.

---

### **4. Ejemplo Práctico en tu Captura**

En tu tabla original:

```
1.360 | 10.0.0.10 | SYN     | Seq=0 | TSval=270132 | TSecr=0
1.360 | 10.0.1.10 | SYN-ACK | Seq=0 | TSval=1877442 | TSecr=270132

```

- **RTT = TSval del servidor (1877442) - TSecr reflejado (270132)**.
- **Pero esto es incorrecto**: Los timestamps son valores arbitrarios, no tiempos absolutos. El cálculo real se hace en el cliente al recibir el `SYN-ACK`:
    - Cliente resta su `TSval` original (`270132`) del tiempo actual al recibir el `SYN-ACK`.

---

### **5. ¿Por qué usar TCP Timestamps?**

- **Evita el "retraso acumulado"** en redes con buffers grandes (Bufferbloat).
- **Mejora la detección de paquetes duplicados** (útil en redes con alta latencia).
- **Habilita escalado de ventana TCP** (para conexiones de alta velocidad).

---

### **Resumen Final**

| Concepto | Detalle |
| --- | --- |
| **RTT clásico** | `T2 - T1` (tiempo de ida y vuelta sin timestamps). |
| **RTT con TS** | `Tiempo actual - TSecr reflejado`. |
| **TSval** | Timestamp del emisor (valor local). |
| **TSecr** | Echo del último `TSval` recibido (o `0`). |
| **RFC 1323** | Define esta opción para mejorar el rendimiento en redes modernas. |




#### 9. Para la captura tcp-captura.pcap, responder las siguientes preguntas.

a. ¿Cuántos intentos de conexiones TCP hay?

b. ¿Cuáles son la fuente y el destino (IP:port) para c/u?

c. ¿Cuántas conexiones TCP exitosas hay en la captura? ¿Cómo diferencia las
exitosas de las que no lo son? ¿Cuáles flags encuentra en cada una?
d. Dada la primera conexión exitosa responder:

i. ¿Quién inicia la conexión?
ii. ¿Quién es el servidor y quién el cliente?
iii. ¿En qué segmentos se ve el 3-way handshake?
iv. ¿Cuáles ISNs se intercambian?
v. ¿Cuál MSS se negoció?
vi. ¿Cuál de los dos hosts envía la mayor cantidad de datos (IP:port)?
e. Identificar primer segmento de datos (origen, destino, tiempo, número de fila y
número de secuencia TCP).
i. ¿Cuántos datos lleva?
ii. ¿Cuándo es confirmado (tiempo, número de fila y número de secuencia
TCP)?
iii. La confirmación, ¿qué cantidad de bytes confirma?
f. ¿Quién inicia el cierre de la conexión? ¿Qué flags se utilizan? ¿En cuáles
segmentos se ve (tiempo, número de fila y número de secuencia TCP)?


10. Responda las siguientes preguntas respecto del mecanismo de control de flujo.
a. ¿Quién lo activa? ¿De qué forma lo hace?
b. ¿Qué problema resuelve?
c. ¿Cuánto tiempo dura activo y qué situación lo desactiva?


11. Responda las siguientes preguntas respecto del mecanismo de control de congestión.
a. ¿Quién activa el mecanismo de control de congestión? ¿Cuáles son los posibles
disparadores?
b. ¿Qué problema resuelve?
c. Diferencie slow start de congestion-avoidance.

12. Para la captura udp-captura.pcap, responder las siguientes preguntas.
a. ¿Cuántas comunicaciones (srcIP,srcPort,dstIP,dstPort) UDP hay en la captura?
b. ¿Cómo se podrían identificar las exitosas de las que no lo son?
c. ¿UDP puede utilizar el modelo cliente/servidor?
d. ¿Qué servicios o aplicaciones suelen utilizar este protocolo?¿Qué requerimientos
tienen?
e. ¿Qué hace el protocolo UDP en relación al control de errores?
f. Con respecto a los puertos vistos en las capturas, ¿observa algo particular que lo
diferencie de TCP?

g. Dada la primera comunicación en la cual se ven datos en ambos sentidos
(identificar el primer datagrama):
i. ¿Cuál es la dirección IP que envía el primer datagrama?,¿desde cuál
puerto?
ii. ¿Cuántos datos se envían en un sentido y en el otro?

13. Dada la salida que se muestra en la imagen, responda los ítems debajo.
● Suponga que ejecuta los siguientes comandos desde un host con la IP
10.100.25.90. Responda qué devuelve la ejecución de los siguientes comandos y, en
caso que corresponda, especifique los flags.
a. hping3 -p 3306 –udp 10.100.25.135
b. hping3 -S -p 25 10.100.25.135
c. hping3 -S -p 22 10.100.25.135
d. hping3 -S -p 110 10.100.25.135
● ¿Cuántas conexiones distintas hay establecidas? Justifique.

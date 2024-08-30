# Práctica 1

#### 1. ¿Qué es una red? ¿Cuál es el principal objetivo para construir una red?

    Una red se refiere a un conjunto de computadoras/dispositivos interconectados con el objetivo de compartir recursos tales como dispositivos, información y servicios
    El conjunto computadoras, software de red, medios y dispositivos de interconexión forma un sistema de comunicación.

#### 2. ¿Qué es Internet? Describa los principales componentes que permiten su funcionamiento.

    Es una red de redes de computadoras, descentralizada, publica, que ejecutan
    el conjunto abierto de protocolos (suite) TCP/IP. Integra diferentes protocolos
    de un nivel más bajo: INTERNETWORKING.
    Es una red global de dispositivos informáticos que interconecta computadoras,
    dispositivos móviles, electrodomésticos y más.
    
    Sus principales componentes incluyen:

    - Dispositivos Terminales: Incluyen computadoras, dispositivos móviles,
    televisores, entre otros, que acceden a Internet.
    Protocolos de Comunicación: Reglas que rigen la comunicación en la red,
    como el Protocolo de Internet (IP) y el Protocolo de Control de Transmisión
    (TCP).
    - Direcciones IP: Identificadores únicos para dispositivos en la red, permitiendo el enrutamiento de datos.
    Nombres de Dominio y DNS: Traducen nombres de dominio en direcciones
    IP.
    - Servidores y Hosts: Almacenan y proporcionan servicios y contenido a través
    de Internet.
    - Routers y Conmutadores: Dirigen y gestionan el tráfico de datos entre redes
    y dentro de ellas.
    - Backbones y Enlaces de Comunicación: Infraestructura de alta velocidad
    que conecta regiones y países.
    - ISP: Proveedores de Servicios de Internet que brindan acceso a la red.
    - Servicios y Aplicaciones: Ofrecen funciones como navegación web, correo
    electrónico y redes sociales.
    La comunicación se logra mediante segmentación de datos en paquetes, que
    viajan a través de enlaces y conmutadores hasta su destino final. Los
    dispositivos terminales se conectan a Internet a través de ISP, que forman una
    red de conmutadores y enlaces de comunicación. Los protocolos, como el
    TCP/IP, controlan la transmisión de información. Los estándares para estos
    componentes se definen en documentos RFC desarrollados por organizaciones
    como IETF y IEEE. Internet facilita la conectividad global y el intercambio de
    información entre usuarios y dispositivos.

#### 3. ¿Qué son las RFCs?

    Las RFCs, o "Request for Comments" (Solicitud de Comentarios), son una
    serie de documentos públicos que contienen especificaciones técnicas,
    estándares y protocolos relacionados con Internet y las tecnologías de la
    información y la comunicación. Las RFCs son mantenidas por la "Internet
    Engineering Task Force" (IETF), una organización que se dedica al desarrollo y
    promoción de estándares para Internet.
#### 4. ¿Qué es un protocolo?

    Un protocolo define el formato y el orden de los mensajes intercambiados entre
    dos o más entidades que se comunican, así como las acciones tomadas al
    producirse la transmisión y/o recepción de un mensaje u otro suceso.
    Protocolo de Red: conjunto de reglas que especifican el intercambio de datos u
    ordenes durante la comunicación entre las entidades que forman parte de una
    red. Permiten la comunicación y están implementados en las componentes.
#### 5. ¿Por qué dos máquinas con distintos sistemas operativos pueden formar parte de una misma red?
    Dos máquinas con distintos sistemas operativos pueden formar parte de una
    misma red debido a la naturaleza de los protocolos de red y las capas de
    abstracción que se utilizan en la comunicación entre dispositivos en una red.
#### 6. ¿Cuáles son las 2 categorías en las que pueden clasificarse a los sistemas finales o End Systems? Dé un ejemplo del rol de cada uno en alguna aplicación distribuida que corra sobre Internet.

    Se pueden clasificar en dos categorías: clientes y servidores. De un modo
    informal, podríamos decir que los clientes suelen ser las computadoras de
    escritorio y portátiles, los teléfonos inteligentes, etc., mientras que los
    servidores suelen ser equipos más potentes que almacenan y distribuyen
    páginas web, flujos de vídeo, correo electrónico, etc. Hoy en día, la mayoría de
    los servidores desde los que recibimos resultados de búsqueda, correo
    electrónico, páginas web y vídeos, residen en grandes centros de datos. Por
    ejemplo, Google tiene entre 50 y 100 centros de datos, incluyendo unos 15
    grandes centros, cada uno con más de 100.000 servidores.
    Los sistemas clientes son dispositivos finales que solicitan y consumen
    servicios o recursos proporcionados por otros sistemas en la red, que
    generalmente son servidores. Los clientes envían solicitudes a los servidores
    para acceder a datos, servicios o aplicaciones.
    Los sistemas servidores son dispositivos finales que proporcionan recursos,
    servicios o contenido a otros sistemas en la red, que suelen ser clientes. Los
    servidores responden a las solicitudes de los clientes y les entregan los datos o
    servicios que necesitan.
#### 7. ¿Cuál es la diferencia entre una red conmutada de paquetes de una red conmutada de circuitos?

    - Red Conmutada de Circuitos:
        En una red conmutada de circuitos, se establece una ruta dedicada y continua
        entre los dispositivos que se comunican antes de que comience la
        transferencia de datos. Durante toda la duración de la comunicación, esta ruta
        se mantiene exclusivamente para los dispositivos que se están comunicando.
    - Red Conmutada de Paquetes:
        En una red conmutada de paquetes, los datos se dividen en pequeñas
        unidades llamadas paquetes antes de ser transmitidos. Cada paquete se envía
        de manera independiente y puede tomar rutas diferentes a través de la red
        para llegar al destino. En lugar de establecer conexiones dedicadas y
        continuas, las redes conmutadas de paquetes envían los paquetes por
        separado y los reensamblan en el destino.
        La conmutación de paquetes es mas eficiente. La conmutación de circuitos
        preasigna el uso del enlace de transmisión independientemente de la
        demanda, con lo que el tiempo de enlace asignado, pero innecesario, se
        desperdicia. Por el contrario, la conmutación de paquetes asigna el uso del
        enlace bajo demanda. La capacidad de transmisión del enlace se compartirá
        paquete a paquete solo entre aquellos usuarios que tengan paquetes que
        transmitir a través del enlace.
        (Debería leer más del libro)
#### 8. Analice qué tipo de red es una red de telefonía y qué tipo de red es Internet.

    Una red de telefonía es una red conmutada de circuitos y el Internet es una red
    conmutada de paquetes.
    Las redes telefónicas tradicionales son ejemplos de redes de conmutación de
    circuitos. Considere lo que ocurre cuando una persona desea enviar
    información (de voz o faxsímil) a otra a través de una red telefónica. Antes de
    que el emisor pueda transmitir la información, la red debe establecer una
    conexión entre el emisor y el receptor. Se trata de una conexión de buena fe en
    la que los conmutadores existentes en la ruta entre el emisor y el receptor
    mantienen el estado de la conexión para dicha comunicación. En la jerga del
    campo de la telefonía, esta conexión se denomina circuito.
    Cuando la red establece el circuito, también reserva una velocidad de
    transmisión constante en los enlaces de la red (que representa una fracción de
    la capacidad de transmisión de cada enlace) para el tiempo que dure la
    conexión. Dado que ha reservado una determinada velocidad de transmisión
    para esta conexión emisor-receptor, el emisor puede transferir los datos al
    receptor a la velocidad constante garantizada.
    Internet, por otro lado, es un ejemplo de una red conmutada de paquetes. En
    esta red, los datos se dividen en pequeñas unidades llamadas paquetes antes
    de ser transmitidos. Cada paquete se envía de manera independiente y puede
    seguir rutas variables a través de la red para llegar a su destino. No se
    establecen conexiones físicas dedicadas antes de la transmisión, lo que
    permite un uso más eficiente de los recursos de red. Internet utiliza el Protocolo
    de Internet (IP) y otros protocolos para enrutar y entregar los paquetes
    correctamente.

#### 9. Describa brevemente las distintas alternativas que conoce para acceder a Internet en su hogar.

    Existen varias alternativas para acceder a Internet en el hogar. Estas incluyen
    banda ancha por cable, DSL, fibra óptica, internet satelital, conexiones
    inalámbricas (Wi-Fi y móvil), redes de banda ancha móvil, redes 5G,
    conexiones por línea eléctrica, opciones de bajo costo y conexiones
    comunitarias. La elección depende de la ubicación geográfica y las
    preferencias del usuario.
#### 10. ¿Qué ventajas tiene una implementación basada en capas o niveles?

    • Reduce complejidad en componente más pequeñas.
    • Las capas de abajo ocultan la complejidad a las de arriba, abstracción.
    • Las capas de arriba utilizan servicios de las de abajo: Interfaces, similar a
    APIs.
    • Los cambios en una capa no deberían afectar a las demás si la interfaz se
    mantiene.
    • Facilita el desarrollo, evolución de las componentes de red asegurando
    interoperabilidad.
    • Facilita aprendizaje, diseño y administración de las redes.
#### 11. ¿Cómo se llama la PDU de cada una de las siguientes capas: Aplicación,Transporte, Red y Enlace? 

|     Capa     |   PDU     |
|:------------:|:---------:| 
|Aplicación    |Mensaje    |
|Transporte    |Segmento   |
|Red Paquete   |           |
|Enlace Trama  |           |


#### 12. ¿Qué es la encapsulación? Si una capa realiza la encapsulación de datos,¿qué capa del nodo receptor realizará el proceso inverso?

    La encapsulación implica agregar encabezados y, posiblemente, remates a los
    datos provenientes de una capa superior para prepararlos para su transmisión
    a través de una red.
    La capa del receptor que se encarga de desencapsular el mensaje es la misma
    que encapsuló los datos en el emisor.
#### 13. Describa cuáles son las funciones de cada una de las capas del stack
    TCP/IP o protocolo de Internet.
    Capa Función
    Aplicación La capa de aplicación aloja aplicaciones y sus protocolos en la red.
    En Internet, abarca protocolos como HTTP (para solicitar
    documentos web), SMTP (para correo electrónico) y FTP (para
    transferencia de archivos). La conversión de nombres
    comprensibles por humanos a direcciones IP de 32 bits se realiza a
    través del Sistema de Nombres de Dominio (DNS), un protocolo de
    capa de aplicación. Los protocolos de esta capa se utilizan en
    sistemas terminales diferentes, permitiendo intercambiar
    información entre aplicaciones en distintos sistemas.
    Transporte La capa de transporte en Internet transporta mensajes de la capa
    de aplicación entre puntos finales de la aplicación. Hay dos
    protocolos de transporte en Internet: TCP y UDP, cada uno apto
    para transportar mensajes de la capa de aplicación. TCP ofrece un
    servicio orientado a la conexión con entrega garantizada y control
    de flujo. Divide mensajes largos en segmentos y controla la
    congestión en la red. UDP, en cambio, ofrece un servicio sin
    conexión básico sin garantía de fiabilidad, control de flujo ni control
    de congestión.
    Red La capa de red en Internet dirige datagramas (paquetes de la capa
    de red) de un host a otro. Los protocolos de transporte (TCP o
    UDP) de un host de origen pasan un segmento y una dirección de
    destino a la capa de red. La capa de red envía el segmento a la
    capa de transporte en el host de destino. El protocolo IP es clave en
    esta capa, definiendo campos del datagrama y reglas para sistemas
    terminales y routers. Todos los componentes de Internet con capa
    de red usan el protocolo IP. La capa de red también tiene protocolos
    de enrutamiento, que determinan rutas de datagramas entre
    orígenes y destinos.
    Enlace La capa de red en Internet dirige datagramas a través de routers
    entre el origen y el destino. Para mover un paquete de un nodo a
    otro en la ruta, la capa de red depende de la capa de enlace. En
    cada nodo, la capa de red pasa el datagrama a la capa de enlace,
    que lo transmite al siguiente nodo. La capa de enlace varía según el
    protocolo empleado, como Ethernet o WiFi. Puesto que los
    datagramas atraviesan múltiples enlaces, pueden ser manejados
    por diferentes protocolos de capa de enlace, como Ethernet y PPP,
    en distintos puntos.
    Física La capa de enlace se ocupa de mover tramas entre nodos
    adyacentes, mientras que la capa física se encarga de transmitir los
    bits individuales que componen la trama entre nodos consecutivos.
    Los protocolos en esta capa son específicos del tipo de enlace y
    medio de transmisión, como Ethernet con múltiples protocolos para
    diferentes tipos de cables. Cada protocolo de la capa física está
    diseñado para transmitir bits de manera única según el medio de
    transmisión utilizado, como cable de cobre, coaxial o fibra óptica.
#### 14. Compare el modelo OSI con la implementación TCP/IP.

    Similitudes:
    • Ambos se dividen en capas.
    • Ambos tienen capas de aplicación, aunque incluyen servicios distintos.
    • Ambos tienen capas de transporte similares.
    • Ambos tienen capa de red similar pero con distinto nombre.
    • Ambos utilizan conmutación de paquetes

    Diferencias:
    • TCP/IP combina las funciones de la capa de presentación y de sesión en la capa de aplicación.
    • TCP/IP combina las capas de enlace de datos y la capa física del modelo OSI en una sola capa.
    • TCP/IP más simple porque tiene menos capas.
    • Los protocolos TCP/IP son los estándares en torno a los cuales se desarrolló Internet, de modo que la credibilidad del modelo
    • TCP/IP se debe en gran parte a sus protocolos.
    • El modelo OSI es un modelo “más” de referencia, teórico, aunque hay implementaciones.
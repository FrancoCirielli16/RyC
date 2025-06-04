1. ¿Qué protocolos se utilizan para el envío de mails entre el cliente y su servidor de
correo? ¿Y entre servidores de correo?

Para él envió de mails entre cliente y servidor se utiliza SMTP. Entre servidores
de correo también se utiliza el protocolo SMTP.
Los clientes suelen usar puertos seguros como 587 (con TLS/STARTTLS) o 465 (SMTPS, SMTP sobre SSL) para autenticarse y cifrar la comunicación
Entre servidores se usa el puerto 25

2. ¿Qué protocolos se utilizan para la recepción de mails? Enumere y explique
características y diferencias entre las alternativas posibles.

Para la recepcion de mails se utiliza POP3 y IMAC

POP3 - Post Office Protocol Version 3

- definido en RFC 1939
- seinicia cuando el agente de usuario (cliente) abre una conexión TCP en el puerto 110 al servidor de correo (servidor)
- u- una vez establecida, POP3 pasa por 3 fases
    - autorización
        - el AU envia un username y password en texto legible para autenticar al usuario
        
        ```reason
        user <nombredeusuario>
        pass <contraseña>
        ```
        
        - ejemplo estableciendo conexi´n telnet en un servidor pop3 usando el puerto 110
            
            ```reason
             telnet mailServer 110
             +OK POP3 server ready
             user benito
             +OK
             pass hambre
             +OK user successfully logged on
            ```
            
    - transacción
        - el AU recupera los mensajes
        - puede
            - marcar msj para borrado
            - eliminar marcas de borrado
            - obtener estadísticas de correo
        - un AU suele configurarse por el usuario para
            - descargar y borrar
            - descargar y guardar
        - la secuencia de comandos que ejecute depende de cual de los dos modos esté
            - modo descargar y borrar
                - list, retr y dele
                - ejemplo
                
                ```reason
                C: list
                 S: 1 498
                 S: 2 912
                 S: .
                 C: retr 1
                 S: (bla bla ...
                 S: .................
                 S: ..........bla)
                 S: .
                 C: dele 1
                 C: retr 2
                 S: (bla bla ...
                 S: .................
                 S: ..........bla)
                 S: .
                 C: dele 2
                 C: quit
                 S: +OK POP3 server signing off
                ```
                
                - AU pide al servidor que le informe el tamaño de cada mensaje, luego el AU recuera y borra todos los mensajes del servidor
                - problema → si el usuario tiene 3 PC, en el modo este si los borra en una maquina, no va a poder leerlo en otra
            - modo de descargar y guardar
                - deja los mensajes en el servidor de correo después de que se hayan descargado
    - actualización
        - luego de que el cliente ejecute el comando quit (terminando con la sesión POP3) el servidor de correo borra los mensajes que han sido marcados para borrado
    
    el AU ejecuta comandos y el servidor devuelve para cada comando una rta
    
    - + ok a veces seguida por una serie de datos servidor-cliente
        - usada por el servidor para indicar que el comando anterior era correcto
    - -ERR indica que había algún error en el comando anterior

     durante una sesión el servidor mantiene cierta info de estado, mantiene la relación de los mensajes de usuarios que han sido marcados para ser borrados, sin embargo no conserva la info de estado de una sesión a otra.


IMAP

- definido en RFC 3501
- asociará cada mensaje con una carpeta
- cuando un mensaje llega al servidor, se asocia con la carpeta INBOX del destinatario, el cual puede pasar el mensaje a una nueva carpeta creada por el usuario, leerlo, borrar, etc
- proporciona comandos para
    - crear carpetas y mover mensajes entre ellas
    - realizar busquedas en carpetas remotas
    - obtener partes de componentes de los mensajes

Diferencias

2 .¿Qué protocolos se utilizan para la recepción de mails? Enumere y explique características y diferencias entre las alternativas posibles.

POP3 - Post Office Protocol Version 3

- definido en RFC 1939
- se inicia cuando el agente de usuario (cliente) abre una conexión TCP en el puerto 110 al servidor de correo (servidor)
- una vez establecida, POP3 pasa por 3 fases
    - autorización
        - el AU envia un username y password en texto legible para autenticar al usuario
        
        ```reason
        user <nombredeusuario>
        pass <contraseña>
        ```
        
        - ejemplo estableciendo conexi´n telnet en un servidor pop3 usando el puerto 110
            
            ```reason
             telnet mailServer 110
             +OK POP3 server ready
             user benito
             +OK
             pass hambre
             +OK user successfully logged on
            ```
            
    - transacción
        - el AU recupera los mensajes
        - puede
            - marcar msj para borrado
            - eliminar marcas de borrado
            - obtener estadísticas de correo
        - un AU suele configurarse por el usuario para
            - descargar y borrar
            - descargar y guardar
        - la secuencia de comandos que ejecute depende de cual de los dos modos esté
            - modo descargar y borrar
                - list, retr y dele
                - ejemplo
                
                ```reason
                C: list
                 S: 1 498
                 S: 2 912
                 S: .
                 C: retr 1
                 S: (bla bla ...
                 S: .................
                 S: ..........bla)
                 S: .
                 C: dele 1
                 C: retr 2
                 S: (bla bla ...
                 S: .................
                 S: ..........bla)
                 S: .
                 C: dele 2
                 C: quit
                 S: +OK POP3 server signing off
                ```
                
                - AU pide al servidor que le informe el tamaño de cada mensaje, luego el AU recupera y borra todos los mensajes del servidor
                - problema → si el usuario tiene 3 PC, en el modo este si los borra en una maquina, no va a poder leerlo en otra
            - modo de descargar y guardar
                - deja los mensajes en el servidor de correo después de que se hayan descargado
    - actualización
        - luego de que el cliente ejecute el comando quit (terminando con la sesión POP3) el servidor de correo borra los mensajes que han sido marcados para borrado
    
    el AU ejecuta comandos y el servidor devuelve para cada comando una respuesta
    
    - + ok a veces seguida por una serie de datos servidor-cliente
        - usada por el servidor para indicar que el comando anterior era correcto
    - -ERR indica que había algún error en el comando anterior

     durante una sesión el servidor mantiene cierta info de estado, mantiene la relación de los mensajes de usuarios que han sido marcados para ser borrados, sin embargo no conserva la info de estado de una sesión a otra.

IMAP

- definido en RFC 3501
- asociará cada mensaje con una carpeta
- cuando un mensaje llega al servidor, se asocia con la carpeta INBOX del destinatario, el cual puede pasar el mensaje a una nueva carpeta creada por el usuario, leerlo, borrar, etc
- proporciona comandos para
    - crear carpetas y mover mensajes entre ellas
    - realizar busquedas en carpetas remotas
    - obtener partes de componentes de los mensajes

Diferencias

| POP3  | IMAP |
| --- | --- |
| no proporciona ningún medio para crear carpetas remotas y asociar mensajes a las mismas | lo proporciona |
| no mantiene info del estado entre sesiones  | mantiene info del estado a lo largo de las sesiones IMAP, como los nombres de las carpetas y los mensajes asociados a cada una de ellas |



3. Utilizando la VM y teniendo en cuenta los siguientes datos, abra el cliente de correo
(Thunderbird) y configure dos cuentas de correo. Una de las cuentas utilizará POP para
solicitar al servidor los mails recibidos para la misma mientras que la otra utilizará IMAP.
Al crear cada una de las cuentas, seleccionar Manual config y luego de configurar las
mismas según lo indicado, ignorar advertencias por uso de conexión sin cifrado.

● Datos para POP

Cuenta de correo: alumnopop@redes.unlp.edu.ar
Nombre de usuario: alumnopop
Contraseña: alumnopoppass
Puerto: 110

● Datos para IMAP
Cuenta de correo: alumnoimap@redes.unlp.edu.ar
Nombre de usuario: alumnoimap
Contraseña: alumnoimappass
Puerto: 143

● Datos comunes para ambas cuentas
Servidor de correo entrante (POP/IMAP):
• Nombre: mail.redes.unlp.edu.ar
• SSL: None
• Autenticación: Normal password
Servidor de correo saliente (SMTP):
• Nombre: mail.redes.unlp.edu.ar
• Puerto: 25
• SSL: None
• Autenticación: Normal password
a. Verificar el correcto funcionamiento enviando un email desde el cliente de
una cuenta a la otra y luego desde la otra responder el mail hacia la primera.
b. Análisis del protocolo SMTP


i. Utilizando Wireshark, capture el tráfico de red contra el servidor de
correo mientras desde la cuenta alumnopop@redes.unlp.edu.ar envía
un correo a alumnoimap@redes.unlp.edu.ar

NO PIENSO HACERLO

ii. Utilice el filtro SMTP para observar los paquetes del protocolo SMTP
en la captura generada y analice el intercambio de dicho protocolo
entre el cliente y el servidor para observar los distintos comandos
utilizados y su correspondiente respuesta. Ayuda: filtre por protocolo
SMTP y sobre alguna de las líneas del intercambio haga click derecho
y seleccione Follow TCP Stream. . .

NO PIENSO HACERLO

c. Usando el cliente de correo Thunderbird del usuario
alumnopop@redes.unlp.edu.ar envíe un correo electrónico
alumnoimap@redes.unlp.edu.ar el cual debe tener: un asunto, datos en el
body y una imagen adjunta.

NO PIENSO HACERLO

i. Verifique las fuentes del correo recibido para entender cómo se utiliza
el header “Content-Type: multipart/mixed“ para poder realizar el envío
de distintos archivos adjuntos.

NO PIENSO HACERLO

ii. Extraiga la imagen adjunta del mismo modo que lo hace el cliente de
correo a partir de los fuentes del mensaje.
NO PIENSO HACERLO



4. Análisis del protocolo POP


a. Utilizando Wireshark, capture el tráfico de red contra el servidor de correo
mientras desde la cuenta alumnoimap@redes.unlp.edu.ar le envía una
correo a alumnopop@redes.unlp.edu.ar y mientras
alumnopop@redes.unlp.edu.ar recepciona dicho correo.
b. Utilice el filtro POP para observar los paquetes del protocolo POP en la
captura generada y analice el intercambio de dicho protocolo entre el cliente
y el servidor para observar los distintos comandos utilizados y su
correspondiente respuesta.



5. Análisis del protocolo IMAP

a. Utilizando Wireshark, capture el tráfico de red contra el servidor de correo
mientras desde la cuenta alumnopop@redes.unlp.edu.ar le envía un correo a
alumnoimap@redes.unlp.edu.ar y mientras alumnoimap@redes.unlp.edu.ar
recepciona dicho correo.
b. Utilice el filtro IMAP para observar los paquetes del protocolo IMAP en la
captura generada y analice el intercambio de dicho protocolo entre el cliente
y el servidor para observar los distintos comandos utilizados y su
correspondiente respuesta.



6. IMAP vs POP
a. Marque como leídos todos los correos que tenga en el buzón de entrada de
alumnopop y de alumnoimap. Luego, cree una carpeta llamada POP en la
cuenta de alumnopop y una llamada IMAP en la cuenta de alumnoimap.
Asegúrese que tiene mails en el inbox y en la carpeta recientemente creada
en cada una de las cuentas.

b. Cierre la sesión de la máquina virtual del usuario redes e ingrese
nuevamente identificándose como usuario root y password packer, ejecute el
cliente de correos. De esta forma, iniciará el cliente de correo con el perfil del
superusuario (diferente del usuario con el que ya configuró las cuentas antes
mencionadas). Luego configure las cuentas POP e IMAP de los usuarios
alumnopop y alumnoimap como se describió anteriormente pero desde el
cliente de correos ejecutado con el usuario root. Responda:

i. ¿Qué correos ve en el buzón de entrada de ambas cuentas? ¿Están
marcados como leídos o como no leídos? ¿Por qué?
ii. ¿Qué pasó con las carpetas POP e IMAP que creó en el paso
anterior?
c. En base a lo observado. ¿Qué protocolo le parece mejor? ¿POP o IMAP?
¿Por qué? ¿Qué protocolo considera que utiliza más recursos del servidor?
¿Por qué?


7. ¿En algún caso es posible enviar más de un correo durante una misma conexión TCP?
Considere:
● Destinatarios múltiples del mismo dominio entre MUA-MSA y entre MTA-MTA
● Destinatarios múltiples de diferentes dominios entre MUA-MSA y entre MTA-MTA

Sí, es posible enviar más de un correo durante una misma conexión TCP en el protocolo SMTP (Simple Mail Transfer Protocol), tanto en la comunicación MUA-MSA (cliente-servidor) como MTA-MTA (servidor-servidor). 

1. Entrega a múltiples destinatarios en el mismo dominio
SMTP permite enviar múltiples correos en una sola conexión TCP mediante el uso secuencial de los comandos MAIL FROM, RCPT TO y DATA para cada mensaje.
2. Entrega a múltiples destinatarios de diferentes dominios
Un MTA puede enviar múltiples correos a diferentes dominios en una misma conexión TCP si el MTA receptor actúa como relé o si está configurado para aceptar mensajes para múltiples dominios.

8. Indique sí es posible que el MSA escuche en un puerto TCP diferente a los convencionales y qué implicancias tendría.
Sí, un administrador de sistema puede configurar un MSA para que escuche en cualquier puerto TCP disponible. Pero puede traer problemas de compatibilidad, detección y seguridad 

9. Indique sí es posible que el MTA escuche en un puerto TCP diferente a los convencionales y qué implicancias tendría.
Técnicamente sí, un servidor puede configurarse para aceptar conexiones SMTP entrantes en otro puerto. Pero hacerlo impide que otros servidores lo encuentren y se comuniquen con él correctamente, ya que el funcionamiento de SMTP entre servidores depende fuertemente del uso de ese puerto estándar.

10. Ejercicio integrador HTTP, DNS y MAIL Suponga que registró bajo su propiedad el dominio redes2024.com.ar y dispone de 4 servidores:

● Un servidor DNS instalado configurado como primario de la zona redes2024.com.ar. (hostname: ns1 - IP: 203.0.113.65).
● Un servidor DNS instalado configurado como secundario de la zona redes2024.com.ar. (hostname: ns2 - IP: 203.0.113.66).
● Un servidor de correo electrónico (hostname: mail - IP: 203.0.113.111). Permitirá a los usuarios envíar y recibir correos a cualquier dominio de Internet.
● Un servidor WEB para el acceso a un webmail (hostname: correo - IP: 203.0.113.8). Permitirá a los usuarios gestionar vía web sus correos
electrónicos a través de la URL https://webmail.redes2024.com.ar


a. ¿Qué información debería informar al momento del registro para hacer visible a Internet el dominio registrado?

- Servidores DNS autorizados (Name Servers)

Son los responsables de resolver las peticiones hacia tu dominio

Servidor DNS primario:
   - Hostname: ns1.redes2024.com.ar
   - IP: 203.0.113.65

Servidor DNS secundario:
   - Hostname: ns2.redes2024.com.ar
   - IP: 203.0.113.66

- Registros A (Address Records)

Para resolver los nombres de host a sus direcciones IP
redes2024.com.ar.     IN A     203.0.113.8

- Registro MX (Mail Exchange)
Para que otros servidores puedan enviar correos al dominio
redes2024.com.ar. IN MX 10 mail.redes2024.com.ar.

- Registros CNAME (opcional)
Para alias como webmail, si se prefiere delegar
webmail.redes2024.com.ar. IN CNAME correo.redes2024.com.ar.

- Registros NS dentro de la zona (coherencia interna)
Esto asegura que el contenido del archivo de zona coincide con lo declarado en el registro
redes2024.com.ar. IN NS ns1.redes2024.com.ar.
redes2024.com.ar. IN NS ns2.redes2024.com.ar.


b. ¿Qué registros sería necesario configurar en el servidor de nombres? Indique toda la información necesaria del archivo de zona. Puede utilizar la siguiente tabla de referencia (evalúe la necesidad de usar cada caso los siguientes campos): Nombre del registro, Tipo de registro, Prioridad, TTL, Valor del registro.

Nombre del registro | Tipo | Prioridad | TTL | Valor del registro
@ | SOA | – | 86400 | ns1.redes2024.com.ar. admin.redes2024.com.ar. 
@ | NS | – | 86400 | ns1.redes2024.com.ar.
@ | NS | – | 86400 | ns2.redes2024.com.ar.
ns1 | A | – | 3600 | 203.0.113.65
ns2 | A | – | 3600 | 203.0.113.66
mail | A | – | 3600 | 203.0.113.111
correo | A | – | 3600 | 203.0.113.8
webmail | A | – | 3600 | 203.0.113.8
@ | MX | 10 | 3600 | mail.redes2024.com.ar.
www | CNAME | – | 3600 | correo.redes2024.com.ar.

c. ¿Es necesario que el servidor de DNS acepte consultas recursivas? Justifique.
No, no es necesario que el servidor DNS autoritativo para el dominio redes2024.com.ar acepte consultas recursivas. De hecho, por seguridad, se recomienda que no lo haga.

El servidor DNS primario y secundario para la zona redes2024.com.ar cumple la función de responder exclusivamente con información autoritativa sobre ese dominio. Es decir, responde consultas del tipo:

“¿Cuál es la IP de mail.redes2024.com.ar?”
“¿Quién es el servidor MX de redes2024.com.ar?”

Estas respuestas no requieren resolución recursiva, ya que el servidor simplemente busca en su propia base de datos (archivo de zona) y responde con los datos que posee.

d. ¿Qué servicios/protocolos de capa de aplicación configuraría en cada servidor?

DNS,SMTP,HTTPS

e. Para cada servidor, ¿qué puertos considera necesarios dejar abiertos a Internet?. A modo de referencia, para cada puerto indique: servidor, protocolo de transporte y número de puerto.

Se deben configurar los puertos recomendados

HTTPS -> 443 - Sobre porotoclo TCP
SMTP -> 25 - Sobre TCP (MTA)
SMTP -> 587 - Sobre TCP (MSA)
SMTP(ssl) -> 465 - Sobre TCP (MSA)
IMAP -> 143 - Sobre TCP
IMAP(ssl) -> 993 - Sobre TCP
POP3 -> 110 - Sobre TCP
POP3(ssl) -> 995 - Sobre TCP
DNS -> 53 - TCP/UDP

f. ¿Cómo cree que se conectaría el webmail del servidor web con el servidor de correo? ¿Qué protocolos usaría y para qué?

??

g. ¿Cómo se podría hacer para que cualquier MTA reconozca como válidos los mails provenientes del dominio redes2024.com.ar solamente a los que llegan de la dirección 203.0.113.111? ¿Afectaría esto a los mails enviados desde el Webmail? Justifique.

Usariamos SPF (Sender Policy Framework)
```
v=spf1 ip4:203.0.113.111 -all
```
- v=spf1: Versión del protocolo SPF.
- ip4:203.0.113.111: Solo permite que la dirección IP 203.0.113.111 envíe correos en nombre del dominio.
- -all: Indica que todos los correos que no provengan de la IP especificada deben ser rechazados.

h. ¿Qué característica propia de SMTP, IMAP y POP hace que al adjuntar una imagen o un ejecutable sea necesario aplicar un encoding (ej. base64)?

SMTP, IMAP y POP solo soportan texto(ASCII) por lo que imagenes o archivos binarios necesitan ser convertidos a un formato de texto para ser tratados por estos servicios, por eso se utiliza base64

i. ¿Se podría enviar un mail a un usuario de modo que el receptor vea que el remitente es un usuario distinto? En caso afirmativo, ¿Cómo? ¿Es una indicación de una estafa? Justifique

Sí, es posible enviar un correo electrónico a un usuario de modo que el receptor vea que el remitente es un usuario distinto. Esto se logra mediante una técnica conocida como spoofing

j. ¿Se podría enviar un mail a un usuario de modo que el receptor vea que el destinatario es un usuario distinto? En caso afirmativo, ¿Cómo? ¿Por qué no le llegaría al destinatario que el receptor ve? ¿Es esto una indicación de una estafa? Justifique

??? repetido? casi igual

k. ¿Qué protocolo usará nuestro MUA para enviar un correo con remitente redes@info.unlp.edu.ar? ¿Con quién se conectará? ¿Qué información será necesaria y cómo la obtendría?



l. Dado que solo disponemos de un servidor de correo, ¿qué sucederá con los mails que intenten ingresar durante un reinicio del servidor?

m. Suponga que contratamos un servidor de correo electrónico en la nube para integrarlo con nuestra arquitectura de servicios.

i. ¿Cómo configuraría el DNS para que ambos servidores de correo se comporten de manera de dar un servicio de correo tolerante a fallos?



11. Utilizando la herramienta Swaks envíe un correo electrónico con las siguientes características:

● Dirección destino: Dirección de correo de alumnoimap@redes.unlp.edu.ar
● Dirección origen: redesycomunicaciones@redes.unlp.edu.ar
● Asunto: SMTP-Práctica4
● Archivo adjunto: PDF del enunciado de la práctica
● Cuerpo del mensaje: Esto es una prueba del protocolo SMTP

a. Analice tanto la salida del comando swaks como los fuentes del mensaje recibido para responder las siguientes preguntas:

i. ¿A qué corresponde la información enviada por el servidor destino como respuesta al comando EHLO? Elija dos de las opciones del listado e investigue la funcionalidad de la misma.

ii. Indicar cuáles cabeceras fueron agregadas por la herramienta swaks.

iii. ¿Cuál es el message-id del correo enviado? ¿Quién asigna dicho valor?

iv. ¿Cuál es el software utilizado como servidor de correo electrónico?

v. Adjunte la salida del comando swaks y los fuentes del correo
electrónico.

b. Descargue de la plataforma la captura de tráfico smtp.pcap y la salida del
comando swaks smtp.swaks para responder y justificar los siguientes
ejercicios.
i. ¿Por qué el contenido del mail no puede ser leído en la captura de
tráfico?

c. Realice una consulta de DNS por registros TXT al dominio info.unlp.edu.ar y
entre dichos registros evalúe la información del registro SPF. ¿Por qué cree
que aparecen muchos servidores autorizados?

d. Realice una consulta de DNS por registros TXT al dominio outlook.com y
analice el registro correspondiente a SPF. ¿Cuáles son los bloques de red
autorizados para enviar mails?. Investigue para qué se utiliza la directiva
"~all"

12. Observar el gráfico a continuación y teniendo en cuenta lo siguiente , responder:
● El usuario juan@misitio.com.ar en PC-A desea enviar un mail al usuario
alicia@example.com
● Cada organización tiene su propios servidores de DNS y Mail
● El servidor ns1 de misitio.com.ar no tiene la recursión habilitada
a. El servidor de mail, mail1, y de HTTP, www, de example.com tienen la misma
IP, ¿es posible esto? Si lo es, ¿cómo lo resolvería?
b. Al enviar el mail, ¿por cuál registro de DNS consultará el MUA?
c. Una vez que el mail fue recibido por el servidor smtp-5, ¿por qué registro de
DNS consultará?
d. Si en el punto anterior smtp-5 recibiese un listado de nombres de servidores
de correo, ¿será necesario realizar una consulta de DNS adicional? Si es
afirmativo, ¿por qué tipo de registro y de cuál servidor preguntaría?

e. Indicar todo el proceso que deberá realizar el servidor ns1 de misitio.com.ar
para obtener los servidores de mail de example.com.
f. Teniendo en cuenta el proceso de encapsulación/desencapsulación y
definición de protocolos, responder V o F y justificar:
● Los datos de la cabecera de SMTP deben ser analizados por el
servidor DNS para responder a la consulta de los registros MX
● Al ser recibidos por el servidor smtp-5 los datos agregados por el
protocolo SMTP serán analizados por cada una de las capas
inferiores
● Cada protocolo de la capa de aplicación agrega una cabecera con
información propia de ese protocolo
● Como son todos protocolos de la capa de aplicación, las cabeceras
agregadas por el protocolo de DNS puede ser analizadas y
comprendidas por el protocolo SMTP o HTTP
● Para que los cliente en misitio.com.ar puedan acceder el servidor
HTTP www.example.com y mostrar correctamente su contenido
deben tener el mismo sistema operativo.
g. Un cliente web que desea acceder al servidor www.example.com y que no
pertenece a ninguno de estos dos dominios puede usar a ns1 de
misitio.com.ar como servidor de DNS para resolver la consulta.
h. Cuando Alicia quiera ver sus mails desde PC-D, ¿qué registro de DNS
deberá consultarse?
i. Indicar todos los protocolos de mail involucrados, puerto y si usan TCP o
UDP, en el envío y recepción de dicho mail
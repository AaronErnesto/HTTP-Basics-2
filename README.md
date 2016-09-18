#HTTP Request Métodos


HTTP define un conjunto de métodos de petición. Un cliente puede utilizar uno de estos métodos de petición para enviar un mensaje de petición a un servidor HTTP. Los métodos son:

- GET: Un cliente puede utilizar la solicitud GET para obtener un recurso web desde el servidor.

- HEAD: Un cliente puede utilizar la petición HEAD para obtener el encabezado que una petición GET habría obtenido. Desde el encabezado contiene la fecha de última modificación de los datos, esto se puede utilizar para comprobar contra la copia caché local.

- POST: Se utiliza para enviar los datos al servidor web.

- PUT: Pregunta el servidor para almacenar los datos.

- DELATE: Pregunta el servidor para eliminar los datos.

- TRACE: Pregunta el servidor para devolver un rastreo de diagnóstico de las medidas que adopta.

- OPTIONS: Pregunta al servidor para devolver la lista de métodos de petición que soporta.

- CONNECT: Se utiliza para decirle a un proxy que establezca una conexión con otro host y sólo debe regresar el contenido, sin intentar analizar o almacenar en caché. Esto a menudo se utiliza para hacer la conexión SSL a través del proxy.

- Otros métodos de extensión.

###"GET" Método de solicitud
GET es el método más común de solicitud HTTP. Un cliente puede utilizar el método GET para solicitar (o "get") una pieza de recursos desde un servidor HTTP. 

Un mensaje de petición GET toma la siguiente sintaxis:

	Petición GET - URI HTTP versión
	(Encabezados de solicitud opcional)
	(linea en blanco)
	(Cuerpo de la petición opcional) 
	
- La palabra clave GET mayúsculas y minúsculas y debe estar en mayúsculas.
- URI de solicitud: especifica la ruta del recurso solicitado, la cual debe empezar desde la raíz " / " del directorio de la base de documentos.
- HTTP-version: HTTP / 1.0 o HTTP / 1.1. Este cliente negocia el protocolo a utilizar para la sesión actual. Por ejemplo, el cliente puede solicitar el uso de HTTP / 1.1. Si el servidor no soporta elprotocolo HTTP / 1.1, puede informar al cliente en la respuesta a utilizar HTTP / 1.0.
- El cliente utiliza los encabezados de solicitud opcionales (tales como Accept , Accept-Language , y etc) para negociar con el servidor y pedir al servidor para entregar los contenidos preferidos (por ejemplo, en el idioma que el cliente prefiere).
- El  mensaje  GET de solicitud tiene un cuerpo de opcional que contiene una cadena de consulta (que se explica más adelante).


###Pruebas de las solicitudes HTTP
Hay muchas maneras de poner a prueba las peticiones HTTP. Se pueden utilizar programas de utilidades como " telnet " o " hyperterm " (buscar: " telnet.exe " o " hypertrm.exe ",  en c:\windows ), o escribir tu propio programa de red para enviar mensaje de solicitud en bruto a un servidor HTTP para poner a prueba las diversas peticiones HTTP.
####Telnet
"Telnet" es una utilidad muy útil la creación de redes. Puede utilizar telnet para establecer una conexión TCP con un servidor; y emitir solicitudes HTTP en bruto. Por ejemplo, suponga que ha comenzado su servidor HTTP en la máquina local (la dirección IP 127.0.0.1) en el puerto 8000:

	  telnet 
	  telnet> ayuda
	 ... Menú telnet ayuda ...
	 telnet> 127.0.0.1 abierta 8000
	 Conexión a 127.0.0.1 ...
	 GET /index.html HTTP / 1.0
	 (pulsa enter dos veces para enviar la línea en blanco que termina ...)
	 ... Mensaje de respuesta HTTP ... 
	 
Telnet es un protocolo basado en caracteres. Cada caracter que se introduce en el cliente telnet se enviará inmediatamente al servidor. Por lo tanto, no puede haber error error tipográfico al entrar el comando, como borrar y la tecla de retroceso se envía al servidor. Puede que tenga que activar la opción de "eco local" para ver los caracteres que ingresa. Consulte el manual de telnet (ayuda de búsqueda de Windows ') para obtener más información sobre el uso de telnet.

###Programas de la red

También puede escribir su propio programa de red para emitir petición HTTP  a un servidor HTTP. Tu programa de red deberá establecer primero una conexión TCP / IP con el servidor. Una vez establecida la conexión TCP, puede emitir la solicitud.

Un ejemplo de programa de red escrito en Java se muestra a continuación (suponiendo que el servidor HTTP se ejecuta en el localhost 127.0.0.1 dirección (IP) en el puerto 8000):

```
 import java.net. *;
 import java.io. *;
   
 public class {HttpClient
    principales argumentos (String []) public static void throws IOException {
       // El host y el puerto que va a conectar.
       String host = "127.0.0.1";
       puerto int = 8000;
       // Crear un socket TCP y conectar con el host: puerto.
       socket socket = new Socket (host, puerto);
       // Crear los flujos de entrada y de salida para la toma de red.
       BufferedReader en
          = New BufferedReader (
               nueva InputStreamReader (socket.getInputStream ()));
       PrintWriter a cabo
          = New PrintWriter (socket.getOutputStream (), true);
       // Enviar solicitud al servidor HTTP.
       out.println ( "GET /index.html HTTP / 1.0");
       out.println (); // línea en blanco de cabeza y cuerpo separador
       out.flush ();
       // Leer la respuesta y la pantalla en la consola.
       línea de cuerda;
       // ReadLine () devuelve un valor nulo si el servidor cierra el socket de red.
       while ((línea = in.readLine ())! = null) {
          System.out.println (línea);
       }
       // Cerrar el I / O arroyos.
       cercar();
       out.close ();
    }
 }
```

###Solicitud HTTP / 1.0 GET

A continuación se muestra la respuesta de una petición HTTP / 1.0 GET 
(tema a través de telnet o en su propio programa de la red  suponiendo que haya comenzado su servidor HTTP):

	  GET /index.html HTTP / 1.0
	 (Pulse dos veces para crear una línea en blanco) 
	  HTTP / 1.1 200 OK
	 Fecha: Sun 18 Oct 2009 08:56:53 GMT
	 Servidor: Apache / 2.2.14 (Win32)
	 Última modificación: Sáb 20 Nov 2004 07:16:26 GMT
	 ETag: "10000000565a5-2c-3e94b66c2e680"
	 Accept-Ranges: bytes
	 Content-Length: 44
	 Conexión: cerrar
	 Content-Type: text / html
	 X-Pad: evitar el fallo del navegador
	   
	 <Html> <body> <h1> Así funciona! </ H1> </ body> </ html>
   
	 Conexión al host perdido. 

En este ejemplo, el cliente envía una solicitud GET para pedir un documento llamado " /index.html "; y negocia utilizar HTTP / 1.0. Se necesita una línea en blanco después de la cabecera de la solicitud. Este mensaje de petición no contiene un cuerpo.

El servidor recibe el mensaje de petición, interpreta y asigna la petición URI a un documento bajo su directorio de documentos. Si el documento solicitado está disponible, el servidor devuelve el documento con un código de estado de respuesta "200 OK". Las cabeceras de respuesta proporcionan la descripción necesaria del documento devuelto, tales como la fecha de última modificación ( Last-Modified ), el tipo MIME ( Content-Type ), y la longitud del documento ( Content-Length ). El cuerpo de la respuesta contiene el documento solicitado. El navegador le dará el formato y mostrará el documento de acuerdo con su tipo de medio (por ejemplo, texto plano, HTML, JPEG, GIF, etc) y otra información obtenida de las cabeceras de respuesta.

####Notas:

- El nombre de método de petición "GET" es sensible a mayúsculas y minúsculas, y por ende debe estar en mayúsculas.

- Si el nombre del método solicitud fue escrito incorrectamente, el servidor devolverá un mensaje de error "501 Método no implementado".

- Si no se permite el nombre de método de la petición, el servidor devolverá un mensaje de error "405 Método no permitido". Por ejemplo, DELETE es un nombre de método válido, pero podría no ser permitido (o implementado) por el servidor.

- Si no existe la URI de solicitud, el servidor devolverá un mensaje de error "404 Not Found". Usted tiene que emitir una adecuada URI de solicitud, a partir de la raíz del documento " / ". De lo contrario, el servidor devolverá un mensaje de error "400 Bad Request".
 
 - Si la versión de HTTP o es incorrecto, el servidor devolverá un mensaje de error "400 Bad Request".

- En HTTP / 1.0, de forma predeterminada, el servidor cierra la conexión TCP después de que se entregó la respuesta. Si utiliza telnet para conectarse al servidor, el mensaje "conexión al host perdido" aparece inmediatamente después que se recibe el cuerpo de la respuesta. Se podría utilizar un encabezado de solicitud "opcional Connection: Keep-Alive " para solicitar una persistente (o keep-alive ) de conexión, por lo que otra petición puede ser enviada a través de la misma conexión TCP para lograr una mejor eficiencia de la red. Por otro lado, HTTP utiliza la conexión 1.1 keep-alive  como predeterminada.

###Respuesta Código de estado

La primera línea del mensaje de respuesta (es decir, la línea de estado) contiene el código de estado de la respuesta, que se genera por el servidor para indicar el resultado de la solicitud.

El código de estado es un número de 3 dígitos:

- 1xx (Informativo): Solicitud recibida, el servidor continúa el proceso.

- 2xx (Éxito): La petición fue recibida con éxito, entendido, aceptado y mantenido.

- 3xx (redirección): Además hay que tomar medidas con el fin de completar la solicitud.

- 4xx (Error de cliente): La solicitud contiene sintaxis incorrecta o no se puede entender.

- 5xx (Error del servidor): El servidor no pudo cumplir con una solicitud aparentemente válida.

Algunos códigos de estado que se encuentran comúnmente son:

- Continuar 100: El servidor ha recibido la solicitud y en el proceso esta dando la respuesta.

- 200 OK: La solicitud se ha cumplido.

- 301 movido de manera permanente: el recurso solicitado se ha movido permanentemente a una nueva ubicación. La URL de la nueva ubicación se da en la cabecera de respuesta denominado Location . El cliente debe emitir una nueva petición a la nueva ubicación. La aplicación debe actualizar todas las referencias a esta nueva ubicación.

- 302 Encontrado y redireccionado (o movido temporalmente): Igual que el 301, pero la nueva ubicación está temporalmente en naturaleza. El cliente debe emitir una nueva solicitud, pero las aplicaciones no necesitan actualizar las referencias.

- 304 Sin modificación: En respuesta a la petición condicional GET If-Modified-Since  , el servidor notifica que el recurso solicitado no se ha modificado.

- 400 Bad Request: el servidor no podía interpretar o comprender la solicitud, probablemente error de sintaxis en el mensaje de petición.

- 401 Se requiere autenticación: El recurso solicitado está protegido, y requieren credenciales de cliente (usuario / contraseña). El cliente debe volver a presentar la solicitud con su credencial (usuario / contraseña).

- 403 Prohibido: El servidor se niega a suministrar el recurso, independientemente de la identidad del cliente.

- 404 No encontrado: El recurso solicitado no se encuentra en el servidor.

- 405 Método no permitido: El método de solicitud utilizado, por ejemplo, POST, PUT, DELETE, es un método válido. Sin embargo, el servidor no permite que el método para el recurso solicitado.

- 408 Request Timeout:

- 414 URI de la solicitud demasiado grande:

- 500 Error interno del servidor: El servidor se confunde, a menudo causada por un error en el programa de respuestas del servidor .

- 501 Método no implementado: El método de solicitud utilizado no es válido (podría ser causada por un error de escritura, por ejemplo, "GET"  como "Get").

- 502 Puerto incorrecto: EL proxy o el puerto de enlace indican que  reciben una mala respuesta del servidor en sentido ascendente.

- 503 Servicio no disponible: El servidor no puede respuesta debido a una sobrecarga o mantenimiento. El cliente puede volver a intentarlo más tarde.

- 504 Tiempo de espera agotado de puerta de enlace: el proxy o puerta de enlace indican que reciben un tiempo de espera de un servidor ascendente.

###Más ejemplos de peticiones GET HTTP / 1.0

**Ejemplo: Método de solicitud mal escrito**
En la solicitud, "GET" está mal escrito como "get". El servidor devuelve un error "501 Método no implementado". El encabezado de respuesta " Allow " le dice al cliente los métodos permitidos.

	  get /test.html HTTP / 1.0
	 (Introduzca dos veces para crear una línea en blanco) 
	 
  > HTTP / 1.1 501 Método no implementado
 Fecha: Sun 18 Oct 2009 10:32:05 GMT
 Servidor: Apache / 2.2.14 (Win32)
 Permitir: GET, HEAD, POST, OPCIONES, TRACE
 Content-Length: 215
 Conexión: cerrar
 Content-Type: text / html;  charset = iso-8859-1
   
	 <! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
	 <Html> <head>
	 <Title> 501 Método no implementado </ title>
	 </ Head> <body>
	 <H1> Método no implementado </ h1>
	 <P> llegar a /index.html no es compatible. <br />
	 </ P>
	 </ Body> </ html> 

**Ejemplo: 404 Archivo no encontrado**

En esta solicitud GET, la solicitud de URL " /t.html " no se puede encontrar en el directorio de documentos del servidor. El servidor devuelve un error "404 Not Found".
>  GET /t.html HTTP / 1.0
 (Introduzca dos veces para crear una línea en blanco) 
  HTTP / 1.1 404 Not Found
 Fecha: Sun 18 Oct 2009 10:36:20 GMT
 Servidor: Apache / 2.2.14 (Win32)
 Content-Length: 204
 Conexión: cerrar
 Content-Type: text / html;  charset = iso-8859-1
 
 ```  
 <! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
 <Html> <head>
 <Title> 404 no encontrado </ title>
 </ Head> <body>
 <H1> No se ha encontrado </ h1>
 <P> El /t.html URL solicitada no se encuentra en este servidor. </ P>
 </ Body> </ html> 
 ```
####Ejemplo: HTTP incorrecto número de versión

En esta solicitud GET, la versión HTTP  está mal escrita. El servidor devuelve un error "404 Bad Request". LA versión HTTP  debe ser HTTP / 1.0 o HTTP / 1.1.

>  GET /index.html HTTTTTP / 1.0
 (Introduzca dos veces para crear una línea en blanco) 
  
	  HTTP / 1.1 400 Bad Request
	 Fecha: 08 de Feb de 2004 01:29:40 GMT
	 Servidor: Apache / 1.3.29 (Win32)
	 Conexión: cerrar
	 Content-Type: text / html;  charset = iso-8859-1
	
	<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">

	<HTML><HEAD>
	<TITLE>400 Bad Request</TITLE>
	</HEAD><BODY>
	<H1>Bad Request</H1>
	Your browser sent a request that this server could not understand.<P>
	The request line contained invalid characters following the protocol string.<P><P>
	</BODY></HTML>
	
**Nota**: La última Apache 2.2.14 ignora este error y devuelve el documento con código de estado "200 OK".

####Ejemplo: incorrecto Request-URI

En la solicitud GET siguiente, el URI de solicitud no comenzó desde la raíz " / ", dio lugar a una "solicitud incorrecta".

	  GET test.html HTTP / 1.0
	 (linea en blanco) 
	
>  HTTP / 1.1 400 Bad Request
 Fecha: Sun 18 Oct 2009 10:42:27 GMT
 Servidor: Apache / 2.2.14 (Win32)
 Content-Length: 226
 Conexión: cerrar
 Content-Type: text / html;  charset = iso-8859-1
  
 ``` 
 <! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
 <Html> <head>
 <Title> 400 Bad Request </ title>
 </ Head> <body>
 <H1> Solicitud incorrecta </ ​​h1>
 <P> El navegador envía una petición que este servidor no podía entender. <br />
 </ P>
 </ Body> </ html> 
  ```
####Ejemplo: conexión Keep-Alive

Por defecto, para la petición HTTP / 1.0 GET, el servidor cierra la conexión TCP una vez la respuesta sea ha entregado. Se podría solicitar que se mantenga la conexión TCP, (a fin de enviar otra solicitud a través de la misma conexión TCP, para mejorar la eficiencia de la red), a través de un encabezado de solicitud opcional " Connection: Keep-Alive ". El servidor incluye una cabecera de respuesta "Connection: Keep-Alive "  para informar al cliente de que puede enviar otra solicitud a través de esta conexión, antes de que el tiempo de espera se agote. Otra cabecera de respuesta " Keep-Alive: timeout=x, max=x " indica al cliente el tiempo de espera (en segundos) y el número máximo de solicitudes que se pueden enviar a través de esta conexión persistente.
  
  >GET /test.html HTTP / 1.0
 Conexión: Keep-Alive
 (linea en blanco) 
  HTTP / 1.1 200 OK
 Fecha: Sun 18 Oct 2009 10:47:06 GMT
 Servidor: Apache / 2.2.14 (Win32)
 Última modificación: Sáb 20 Nov 2004 07:16:26 GMT
 ETag: "10000000565a5-2c-3e94b66c2e680"
 Accept-Ranges: bytes
 Content-Length: 44
 Mantenimiento de conexión: tiempo de espera = 5, max = 100
 Conexión: Keep-Alive
 Content-Type: text / html
```
<Html> <body> <h1> It works! </ H1> </ body> </ html> 
```
**notas:**

- El mensaje "Connection to host lost" (para telnet) aparece después de "keep-alive" tiempo agotado.

-Antes de que aparezca el mensaje "Connection to host lost" (por ejemplo: "keep-alive" tiempo agotado) se puede enviar una nueva solicitud a través de la misma conexión TCP.

- El encabezado " Connection: Keep-alive " no distingue entre mayúsculas y minúsculas. El espacio es opcional.

- Si una cabecera opcional está mal escrita o no es válidA, se omite en el servidor.

####Ejemplo: Cómo acceder a un recurso protegido

La siguiente petición GET ha intentado acceder a un recurso protegido. El servidor devuelve un error "403 Forbidden". En este ejemplo, el directorio " htdocs\forbidden " se configura para denegar el acceso completo con el archivo de configuración del servidor HTTP Apache " httpd.conf " de la siguiente manera:
```
 <Directory "C:/apache/htdocs/forbidden">
   Order deny,allow
   deny from all
</Directory> 
```
>  GET /forbidden/index.html HTTP / 1.0
 (linea en blanco) 
 
 > HTTP/1.1 403 Forbidden
Date: Sun, 18 Oct 2009 11:58:41 GMT
Server: Apache/2.2.14 (Win32)
Content-Length: 222
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: text/html; charset=iso-8859-
 
  
	  <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
	<html><head>
	<title>403 Forbidden</title>
	</head><body>
	<h1>Forbidden</h1>
	<p>You don't have permission to access/forbidden/index.html on this server.</p>
	</body></html>
 
####Solicitud HTTP / 1.1 GET

El servidor HTTP / 1.1 es compatible con las llamadas máquinas virtuales. Es decir, el mismo servidor físico podría albergar varios hosts virtuales, con diferentes nombres de host (por ejemplo, www.nowhere123.com y www.test909.com ) y sus propios directorios raíz de documentos dedicados. Por lo tanto, en una petición HTTP / 1.1 GET, es obligatorio incluir un encabezado de solicitud llamado " Host ", para seleccionar uno de los hosts virtuales.

**Ejemplo: HTTP / 1.1 Solicitud**

HTTP / 1.1 mantiene persistente (o keep-alive) la conexión por defecto para mejorar la eficiencia de la red. Se puede utilizar una "solicitud de cabecera Connection: Close " para pedir al servidor para cerrar la conexión TCP una vez que se entrega la respuesta.

>  GET /index.html HTTP / 1.1
 Anfitrión: 127.0.0.1
 (linea en blanco) 
 
 > HTTP / 1.1 200 OK
 Fecha: Sun 18 Oct 2009 12:10:12 GMT
 Servidor: Apache / 2.2.14 (Win32)
 Última modificación: Sáb 20 Nov 2004 07:16:26 GMT
 ETag: "10000000565a5-2c-3e94b66c2e680"
 Accept-Ranges: bytes
 Content-Length: 44
 Content-Type: text / html
   
	 <Html> <body> <h1> Así funciona! </ H1> </ body> </ html> 
####Ejemplo: HTTP / 1.1 falta el encabezado de host

El siguiente ejemplo muestra que el " Host " de cabecera es obligatorio en una petición HTTP / 1.1 . Si " Host " no se encuentra el servidor devuelve un error "400 Bad Request".

>  GET /index.html HTTP / 1.1
 (linea en blanco) 
  HTTP / 1.1 400 Bad Request
 Fecha: Sun 18 Oct 2009 12:13:46 GMT
 Servidor: Apache / 2.2.14 (Win32)
 Content-Length: 226
 Conexión: cerrar
 Content-Type: text / html;  charset = iso-8859-1
   
	 <! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
	 <Html> <head>
	 <Title> 400 Bad Request </ title>
	 </ Head> <body>
	 <H1> Solicitud incorrecta </ ​​h1>
	 <P> El navegador envía una petición que este servidor no podía entender. <br />
	 </ P>
	 </ Body> </ html> 
	 
##Las peticiones GET condicionales

En todos los ejemplos anteriores, el servidor devuelve todo el documento si la petición puede ser satisfecha (es decir incondicional). Es posible utilizar encabezado de la solicitud adicional para emitir una "solicitud condicional". Por ejemplo, para que solicite el documento basado en la fecha de última modificación (a fin de decidir si utilizar la copia caché local), o para pedir una parte del documento (o rango) en lugar de todo el documento (útil para la descarga de documentos de gran tamaño).

Los encabezados de solicitud condicional incluyen:

- If-Modified-Since (comprobación de código de estado de respuesta "304 Not Modified").

- If-Unmodified-Since

- If-Match
- If-None-Match
- If-Range

####Cabeceras de petición

En esta sección se describen algunas de las cabeceras de petición de uso común. Consulte la especificación HTTP para más detalles. La sintaxis del nombre de la cabecera es con mayúscula inicial y se unen utilizando guión ( - ), por ejemplo, Content-Length , If-Modified-Since .

**Host: domain-name** - HTTP / 1.1 soporta máquinas virtuales. Múltiples nombres DNS (por ejemplo, www.nowhere123.com y www.nowhere456.com) pueden residir en el mismo servidor físico, con sus propios directorios raíz de documentos. Host cabecera es obligatoria en HTTP / 1.1 para seleccionar uno de los anfitriones.

Los siguientes encabezados pueden ser utilizados para la negociación de contenido por el cliente para pedir al servidor  entregar el tipo preferido del documento (en términos del tipo de medio, por ejemplo, JPEG vs GIF, o el lenguaje usado por ejemplo Inglés vs francés) si el servidor mantiene múltiples versiones de un mismo documento.

**Accept: mime-type-1 , mime-type-2 , ... **- El cliente puede utilizar la cabecera Accept  para indicar al servidor los tipos MIME que puede manejar y las preferencias. Si el servidor tiene varias versiones del documento solicitado (por ejemplo, una imagen en formato GIF y PNG, o un documento en formato TXT y PDF), se puede comprobar esta cabecera para decidir qué versión de entregar al cliente. (Por ejemplo, PNG es más avanzado que GIF, pero no todas navegador soporta PNG.) Este proceso se denomina de tipo de contenido negociación.

**Accept-Language: language-1 , language-2 , ... -** El cliente puede utilizar la cabecera Accept-Language  para indicar al servidor qué idiomas se puede manejar o que prefiere. Si el servidor tiene varias versiones del documento solicitado (por ejemplo, en Inglés, chino, francés), se puede comprobar esta cabecera para decidir cuál es la versión para volver. Este proceso se llama negociación de idioma.

**Accept-Charset: Charset-1 , Charset-2 , ... **- Para la negociación del conjunto de caracteres, el cliente puede utilizar esta cabecera para indicar al servidor qué conjuntos de caracteres puede manejar. Ejemplos de conjuntos de caracteres ISO-8859-1, ISO-8859-2, ISO-8859-5, Big5, UCS2, UCS4, UTF8.

**Accept-Encoding: encoding-method-1 , encoding-method-2 , ... **- El cliente puede utilizar esta cabecera para indicar al servidor el tipo de codificación que soporta. Si el servidor ha codificado (o comprimido) la versión del documento solicitado, puede devolver una versión codificada soportada por el cliente. El servidor también puede elegir para codificar el documento antes de volver al cliente para reducir el tiempo de transmisión. El servidor debe establecer la cabecera de respuesta " Content-Encoding " para informar al cliente de que se codifica el documento devuelto. Los métodos de codificación son comunes " x-gzip ( .gz , .tgz )" y " x-compress ( .Z )".

**Connection: Close|Keep-Alive **- El cliente puede utilizar esta cabecera para indicar al servidor la posibilidad de cerrar la conexión después de esta solicitud, o para mantener la conexión activa durante otra solicitud. HTTP / 1.1 usa conexión persistente (keep-alive) de forma predeterminada. HTTP / 1.0 cierra la conexión por defecto.

**Referer: referer-URL **- El cliente puede utilizar esta cabecera para indicar el referente de esta solicitud. Si hace clic en un enlace desde la página web de 1 a visitar la página web 2, página web 1 es la de referencia para la solicitud de la página web 2. Todos los navegadores más importantes usan esta cabecera, que puede ser utilizado para hacer un seguimiento cuando la solicitud proviene de (por publicidad en la web o la personalización del contenido). No obstante, esta cabecera no es fiable y se puede suplantar fácilmente. Tenga en cuenta que "referer" está mal escrito como "Referer".

**User-Agent: browser-type -** Identifica el tipo de navegador que se utiliza para realizar la solicitud. El servidor puede utilizar esta información para volver documento diferente dependiendo del tipo de navegadores.

**Content-Length: number-of-bytes - **Usado por  la solicitud POST, para informar al servidor de la longitud del cuerpo de la petición.

**Content-Type: mime-type -** Utilizado por solicitud POST, para informar al servidor el tipo de medio del cuerpo de la petición.

**Cache-Control: no-cache|... **- El cliente puede utilizar esta cabecera para especificar cómo las páginas se van a almacenar en caché por el servidor proxy. " no-cache " requiere proxy para obtener una nueva copia del servidor original, a pesar de que una copia en caché local está disponible.(HTTP / 1.0 servidor no reconoce " Cache-Control: no-cache". En su lugar, utiliza " Pragma: no-cache". Incluye dos cabeceras de la petición si no está seguro acerca de la versión del servidor.)

**Authorization: **Usado por el cliente para suministrar su credencial (usuario / contraseña) para tener acceso a los recursos protegidos. (Esta cabecera se describirá en el capítulo después de la autenticación.)

**Cookie: cookie-name-1 = cookie-value-1 , cookie-name-2 = cookie-value-2 , ...**- El cliente utiliza esta cabecera para devolver la(s) cookie (s) de vuelta al servidor, que fue creado por este servidor antes para el manejo del estado. (Esta cabecera se discutirá en el capítulo más adelante la administración del estado.)

**If-Modified-Since: date -** Le pide al servidor  enviar la página sólo si ha sido modificada después de una fecha específica.

###GET Solicitud de Directorio

Supongamos que un directorio llamado " testdir" está presente en el directorio raíz de documentos " htdocs".

Si un cliente emite una solicitud GET a " /testdir/" (es decir, en el directorio).

1. El servidor devolverá " /testdir/index.html" si el directorio contiene un " index.htmlarchivo".
2. De lo contrario, el servidor devuelve el listado de directorios, si el listado de directorios está habilitada en la configuración del servidor.
3. De lo contrario, el servidor devuelve "404 página no encontrada".

Es interesante tomar nota de que si un problema por parte del cliente en una solicitud GET a " /testdir" (sin especificar la ruta del directorio "/"), el servidor devuelve un" 301 Move Permanently " con un nuevo" Location"del" /testdir/", de la siguiente manera.

> GET / testdir HTTP / 1.1
Anfitrión: 127.0.0.1
(linea en blanco) 
HTTP / 1.1 301 Movido permanentemente
Fecha: Sun 18 Oct 2009 13:19:15 GMT
Servidor: Apache / 2.2.14 (Win32)
Ubicación: http://127.0.0.1:8000/testdir/
Content-Length: 238
 Content-Type: text / html;  charset = iso-8859-1
   
	<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
	 <Html> <head>
	<Title> 301 Movido permanentemente </ title>
	 </ Head> <body>
	<H1> trasladado de manera permanente </ h1>
	<P> El documento se ha movido <a href="http://127.0.0.1:8000/testdir/"> aquí </a>. </ P>

	</ Body> </ html> 
	
La mayoría de los  navegadores seguirá con otra petición de " /testdir/". Por ejemplo, si emite http://127.0.0.1:8000/testdirsin el arrastre " /" desde un navegador, se puede notar que un arrastre " /se añadió" a la dirección después se le dio la respuesta. La moraleja de la historia es: usted debe incluir el " /" a una solicitud GET para la petición de directorio para ahorrar una petición GET adicional.

###Una petición GET a través de un servidor proxy
Para enviar una petición GET a través de un servidor proxy,  (a) establecer una conexión TCP con el servidor proxy; (b) utilizar un absoluto URI de solicitud al servidor de destino.http:// hostname : port / path / fileName.

El siguiente seguimiento fue capturado por medio de telnet. Se establece una conexión con el servidor proxy, y emitió una petición GET. Una  solicitud URI absolutade  se utiliza en la línea de petición.

	GET http://www.amazon.com/index.html HTTP / 1.1
	Anfitrión: www.amazon.com
	 Conexión: Cerrar
	(linea en blanco) 
	  HTTP / 1.1 302 Found
	 Transfer-Encoding: fragmentada
	Fecha: Fri 27 Feb 2004 09:27:35 GMT
	 Content-Type: text / html;  charset = iso-8859-1
	 Conexión: cerrar
		Servidor: Fortaleza / 2.4.2 Apache / 1.3.6 C2NetEU / 2412 (Unix)
	Set-Cookie: = piel; domain = .amazon.com; path = /; expira = Mie, 01-Ago-01 12:00:00 GMT
	 Conexión: close
	Ubicación: 	http://www.amazon.com:80/exec/obidos/subst/home/home.html
	Vía: 1.1 xproxy (NetCache NetApp / 5.3.1R4D5)
   
	 ed
	<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
	<HTML> <HEAD>
	<TITLE> 302 encontrados </ TITLE>
	</ HEAD> <BODY>
	<H1> Encontrados </ h1>
	El documento se ha movido
	<A HREF="http://www.amazon.com:80/exec/obidos/subst/home/home.html">
	</A> aquí. <P>
	</ BODY> </ HTML>
   
	 0
   
Note que la respuesta se devuelve en "trozos".

### Método de petición "HEAD"

La petición HEAD es similar a la petición GET. Sin embargo, el servidor devuelve sólo el encabezado de respuesta sin el cuerpo de la respuesta  que contiene el documento actual. La petición HEAD es útil para comprobar las cabeceras, tales como Last-Modified, Content-Type, Content-Length, antes de enviar una solicitud GET adecuada para recuperar el documento.

La sintaxis de la petición HEAD es la siguiente:

	CABEZA URI de solicitud  HTTP-versión
	 (otras cabeceras de solicitud opcionales)
	(linea en blanco)
	(Cuerpo de la petición opcional) 

Ejemplo

	 CABEZA /index.html HTTP / 1.0
	(linea en blanco) 
	  HTTP / 1.1 200 OK
	Fecha: Sun 18 Oct 2009 14:09:16 GMT
	Servidor: Apache / 2.2.14 (Win32)
	Última modificación: Sáb 20 Nov 2004 07:16:26 GMT
	ETag: "10000000565a5-2c-3e94b66c2e680"
	 Accept-Ranges: bytes
	Content-Length: 44
	 Conexión: cerrar
	 Content-Type: text / html
	X-Pad: evitar el fallo del navegador 

Observe que la respuesta consiste en la cabecera sólo que sin el cuerpo, que contiene el documento real.

### Método de petición"OPTIONS" 

Un cliente puede utilizar un método de petición OPTIONS para consultar con el  servidor qué  métodos de petición soporta. La sintaxis de mensaje de solicitud de OPCIONES es:

	OPTIONS URI de solicitud | * HTTP-versión
	 (otros títulos opcionales)
	(linea en blanco) 
" *" Se puede utilizar en lugar de un URI de solicitud para indicar que la solicitud no se aplica a cualquier recurso en particular.

**Ejemplo**

Por ejemplo, la siguiente petición OPTIONS se envía a través de un servidor proxy:

	 OPCIONES http://www.amazon.com/~~V~~plural~~3rd HTTP / 1.1
	Anfitrión: www.amazon.com
	 Conexión: Cerrar
	(linea en blanco) 
	  HTTP / 1.1 200 OK
	Fecha: Fri 27 Feb 2004 09:42:46 GMT
	Content-Length: 0
	 Conexión: cerrar
	Servidor: Fortaleza / 2.4.2 Apache / 1.3.6 C2NetEU / 2412 (Unix)
	Permitir: GET, HEAD, POST, OPCIONES, TRACE
	 Conexión: close
	Vía: 1.1 xproxy (NetCache NetApp / 5.3.1R4D5)
	(linea en blanco) 
	
Todos los servidores que permiten a petición GET permitirá petición HEAD. A veces, la cabeza no está en la lista.

###"TRACE" método de la petición

Un cliente puede enviar una solicitud TRACE para pedir al servidor  devolver un rastreo de diagnóstico.

La solicitud de rastreo toma la siguiente sintaxis:

	TRACE / HTTP-versión
	 (línea en blanco)

**Ejemplo**

El siguiente ejemplo muestra una petición TRACE emitida a través de un servidor proxy.

	 TRACE http://www.amazon.com/ HTTP / 1.1
	Anfitrión: www.amazon.com
	 Conexión: Cerrar
	(linea en blanco) 
	  HTTP / 1.1 200 OK
	 Transfer-Encoding: fragmentada
	Fecha: Fri 27 Feb 2004 09:44:21 GMT
	Content-Type: mensaje / http
	 Conexión: cerrar
	Servidor: Fortaleza / 2.4.2 Apache / 1.3.6 C2NetEU / 2412 (Unix)
	 Conexión: cerrar
	Vía: 1.1 xproxy (NetCache NetApp / 5.3.1R4D5)
   
	 9d
	TRACE / HTTP / 1.1
	 Conexión: keep-alive
	Anfitrión: www.amazon.com
	Vía: 1.1 xproxy (NetCache NetApp / 5.3.1R4D5)
	X-reenvía a: 155.69.185.59, 155.69.5.234
   
	 0
   
(Para comparar la solicitud de rastreo con el trazado de ruta)


> Written with [StackEdit](https://stackedit.io/).

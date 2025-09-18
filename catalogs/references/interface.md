## Arquitectura de microservicios y monolítica

En una arquitectura monolítica, toda la aplicación está construida como un solo bloque de software. Esto significa que todos los procesos —como el manejo de usuarios, pagos, base de datos, etc.— están agrupados y funcionan juntos dentro de un único programa. Si uno de esos procesos necesita más capacidad (por ejemplo, porque muchos usuarios lo están usando al mismo tiempo), se tiene que escalar toda la aplicación completa, no solo ese proceso.

Conforme la aplicación crece y se le agregan nuevas funciones, el código se vuelve más difícil de mantener y de modificar. Esta complejidad puede hacer más lento el desarrollo, limitar la posibilidad de probar nuevas ideas y aumentar el riesgo de errores. Además, como todos los componentes están conectados entre sí, si un proceso falla, puede afectar a toda la aplicación.

Por otro lado, en una arquitectura de microservicios, la aplicación se divide en partes más pequeñas e independientes llamadas "servicios". Cada uno de estos servicios cumple una función específica (por ejemplo, uno maneja usuarios, otro publica mensajes, otro gestiona pagos). Estos servicios se comunican entre sí a través de interfaces bien definidas usando APIs ligeras.

Gracias a que cada microservicio funciona de forma independiente, es posible actualizarlos, escalarlos o reemplazarlos sin afectar al resto del sistema. Esto facilita el desarrollo, mejora la estabilidad y permite una mayor flexibilidad para adaptarse a las necesidades del negocio.

### Beneficios de los Microservicios

Agilidad: Equipos pequeños e independientes pueden trabajar rápido y con mayor autonomía, acelerando el desarrollo.

Escalado flexible: Cada servicio se puede escalar por separado según la demanda, optimizando recursos y costos.

Implementación sencilla: Facilitan pruebas, actualizaciones rápidas y reversión de errores, promoviendo la experimentación.

Libertad tecnológica: Los equipos pueden usar diferentes herramientas y tecnologías según sus necesidades.

Código reutilizable: Servicios pequeños y bien definidos pueden reutilizarse para distintas funciones, ahorrando tiempo de desarrollo.

Resiliencia: Los errores en un servicio no afectan toda la aplicación, permitiendo que funcione con menor impacto ante fallos.

Referencia: https://aws.amazon.com/es/microservices/

## ¿Qué es una API?

API significa “interfaz de programación de aplicaciones”. En el contexto de las API, la palabra aplicación se refiere a cualquier software con una función distinta. La interfaz puede considerarse como un contrato de servicio entre dos aplicaciones. Este contrato define cómo se comunican entre sí mediante solicitudes y respuestas. La documentación de su API contiene información sobre cómo los desarrolladores deben estructurar esas solicitudes y respuestas. Las API son mecanismos que permiten a dos componentes de software comunicarse entre sí mediante un conjunto de definiciones y protocolos. Por ejemplo, el sistema de software del instituto de meteorología contiene datos meteorológicos diarios. La aplicación meteorológica de su teléfono “habla” con este sistema a través de las API y le muestra las actualizaciones meteorológicas diarias en su teléfono.

Referencia: https://aws.amazon.com/es/what-is/api/

## ¿Qué son protocolos?

Los protocolos son un conjunto de reglas y normas que permiten que diferentes dispositivos o programas se comuniquen entre sí de manera ordenada y entendible. En otras palabras son como un lenguaje común o un acuerdo que define cómo se debe enviar, recibir y procesar la información para que no haya confusión ni errores durante la comunicación. Sin protocolos, los dispositivos no podrían intercambiar datos correctamente, porque no sabrían cómo interpretar lo que reciben.

### Tipos de Protocolos

*Protocolos de Comunicación de Red*: 

*TCP (Transmission Control Protocol): Protocolo orientado a la conexión que garantiza la entrega correcta y en orden de los datos.

*UDP (User Datagram Protocol): Protocolo sin conexión que envía datos rápidamente pero sin garantía de entrega ni orden.

*Protocolos de Aplicación*

*HTTP (HyperText Transfer Protocol): Usado para la transferencia de páginas web.

*HTTPS: Versión segura de HTTP, con cifrado.

*FTP (File Transfer Protocol): Para transferencia de archivos.

*SMTP (Simple Mail Transfer Protocol): Para envío de correos electrónicos.

*IMAP/POP3: Para recibir correos electrónicos.

*Protocolos de Enlace de Datos*: 

*Ethernet: Usado en redes locales (LAN).

*PPP (Point-to-Point Protocol): Para conexiones directas entre dos nodos.

*Protocolos de Internet*: 

*IP (Internet Protocol): Dirige paquetes de datos a través de redes.

*ICMP (Internet Control Message Protocol): Utilizado para enviar mensajes de control y error.

*Protocolos de Seguridad*:

*SSL/TLS: Para cifrado y seguridad en la comunicación en internet.

*IPSec: Protocolo para asegurar comunicaciones IP.

----------------------------------------------------------------------------------------------------------

## Interfaz 001

**name**: API REST

**description**: Es una interfaz de programación de aplicaciones que se ajusta a los principios de diseño del estilo arquitectónico de transferencia de estado representacional, es un estilo que se utiliza para conectar sistemas hipermedia distribuidos. Ofrece una forma sencilla de crear API web y se utilizan para facilitar el intercambio de datos entre aplicaicones, servicios web y bases de datos, además para conectar componentes de arquitectura de microservicios.

**type**: Una API es un mecanismo que permite a una aplicación o servicio acceder a un recurso dentro de otra aplicación, servicio o base de datos, osea, la aplicación o servicio que accede a los recursos es el cliente y la aplicación o servicio que contiene el recurso es el servidor. Alguna API, como SOAP o XML-RPC, imponen un marco estricot a los desarrolladores no obstante ellos pueden desarrollar API REST untilizando cualquier lenguaje de programación y admiten diversos formatos de datos. El único requisito es que se ajusten a los siguientes seis principios de diseño REST, tambien conocidos como restircciones arquitectónicas.

**protocols**: Las API REST se comunican a través de solicitudes HTTP para realizar funciones de base de datos estándar, como crear, leer, actualizar y eliminar registros (también conocidos como CRUD) dentro de un recurso. Por ejemplo, una API REST usaría una solicitud GET para recuperar un registro. Una solicitud POST crea un nuevo registro. Una solicitud PUT actualiza un registro y una solicitud DELETE lo elimina. Todos los métodos HTTP se pueden usar en las llamadas a la API. Una API REST bien diseñada es similar a un sitio web que se ejecuta en un navegador web con funcionalidad HTTP integrada.

**dataFormats**: El estado de un recurso en un instante determinado, o marca de tiempo, se conoce como representación del recurso. Esta información puede entregarse a un cliente en prácticamente cualquier formato, incluyendo Notación de Objetos JavaScript (JSON), HTML, XLT, Python, PHP o texto plano. JSON es popular porque es legible tanto para humanos como para máquinas, y es independiente del lenguaje de programación.

**security**: Utilice algoritmos de hash para la seguridad de las contraseñas y HTTPS para la transmisión segura de datos. Un marco de autorización como OAuth 2.0 puede ayudar a limitar los privilegios de las aplicaciones de terceros.

**version**: La Especificación OpenAPI (OAS) establece una interfaz para describir una API de forma que cualquier desarrollador o aplicación pueda descubrirla y comprender plenamente sus parámetros y capacidades. Esta información incluye los puntos de conexión disponibles, las operaciones permitidas en cada punto de conexión, los parámetros de operación, los métodos de autenticación y más. La última versión, OAS3 , incluye herramientas prácticas, como el Generador OpenAPI, para generar clientes API y stubs de servidor en diferentes lenguajes de programación.

**status**: Activo

**documentation**: https://www.ibm.com/think/topics/rest-apis

## Interfaz 002

**name**: API GraphQL

**description**: Es un lenguaje de consulta para API y un entorno de ejecución para ejecutar dichas consultas con datos existentes. GraphQL proporciona una descripción completa y comprensible de los datos de tu API, permite a los clientes solicitar exactamente lo que necesitan y nada más, facilita la evolución de las API con el tiempo y habilita potentes herramientas para desarrolladores .

GraphQL permite leer, escribir ( mutar ) y suscribirse a cambios en los datos (actualizaciones en tiempo real, generalmente implementadas mediante WebhHooks). Los servidores GraphQL están disponibles para múltiples lenguajes, como Haskell, JavaScript, Perl, Python, Ruby, Java, C++, C#, Scala, Go, Erlang, PHP y R.

**type**: La obtención de datos de GraphQL es eficiente y ofrece beneficios que incluyen una fácil lectura, evitar la obtención excesiva o insuficiente de datos, tipificación estricta y una evolución flexible del esquema.

**protocols**: Se basa en HTTP, ya que HTTP es el protocolo de comunicación subyacente. GraphQL diseñan su intercambio de datos en torno a los recursos. Un recurso hace referencia a cualquier dato u objeto al que el cliente puede acceder y manipular a través de la API. Cada recurso tiene su propio identificador único (URI) y un conjunto de operaciones (métodos HTTP) que el cliente puede realizar en él.

**dataFormats**: JSON es el formato de intercambio de datos más popular que todos los lenguajes, plataformas y sistemas entienden. El servidor devuelve los datos en formato JSON al cliente. Hay otros formatos de datos disponibles, pero se utilizan con menos frecuencia, como XML y HTML. Tanto las API de GraphQL como las de REST funcionan con cualquier estructura de base de datos y cualquier lenguaje de programación, tanto del cliente como del servidor. Esto hace que tengan un alto nivel de interoperabilidad con cualquier aplicación.

**security**: Utilizar mecanismos como Tokens Web JSON (JWT) para autenticar a los usuarios y establecer permisos basados en roles para restringir el acceso a datos y operaciones específicas, según la autorización basada en roles..

**version**: No hay una única "versión actual de la API GraphQL", ya que GraphQL es un lenguaje de consulta, no una API en sí misma. La "versión actual" depende del servicio o plataforma que utilice GraphQL

**status**: Activo

**documentation**: https://aws.amazon.com/es/compare/the-difference-between-graphql-and-rest/
https://hygraph.com/learn/graphql

## Interfaz 003

**name**: Protobuf

**description**: Es como JSON, pero más pequeño y rápido, y genera enlaces en lenguajes nativos. Defines cómo quieres que se estructuren tus datos una vez, y luego puedes usar código fuente generado específicamente para escribir y leer fácilmente tus datos estructurados en y desde diversos flujos de datos y en diversos lenguajes. Los buffers de protocolo son una combinación del lenguaje de definición (creado en .protoarchivos), el código que el compilador proto genera para interactuar con los datos, las bibliotecas de tiempo de ejecución específicas del lenguaje, el formato de serialización para los datos que se escriben en un archivo (o se envían a través de una conexión de red) y los datos serializados

**type**: gRPC es un marco de trabajo para comunicación remota (Remote Procedure Calls - RPC) desarrollado por Google que utiliza Protocol Buffers como formato de serialización de datos por defecto. En gRPC, los servicios se definen usando archivos .proto, que luego son compilados para generar código que maneja la serialización y deserialización de mensajes, así como la implementación de servicios.

**protocols**: Los búferes de protocolo son ideales para cualquier situación en la que se necesite serializar datos estructurados, similares a registros y tipificados, de forma independiente del lenguaje y la plataforma, y ​​extensible. Se utilizan con mayor frecuencia para definir protocolos de comunicación (junto con gRPC) y para el almacenamiento de datos. gRPC (que se basa en HTTP/2 y TCP) sí usan Protobuf por defecto para la serialización de datos.

**dataFormats**: Los Protobuf utilizan un formato de datos binarios por defecto, lo que lo hace más eficiente en términos de tamaño y velocidad que formatos como JSON o XML.

**security**: Protocol Buffers (Protobuf) no incluye seguridad por sí mismo, pero cuando se usa con gRPC, se suele combinar con mecanismos como TLS y mTLS para garantizar la autenticación, autorización y cifrado de datos.

**version**: La versión estable más reciente es 4.31.0, liberada el 14 de mayo de 2025.

**status**: Activo

**documentation**: https://protobuf.dev/overview/

## Interfaz 004

**name**: Documentos ZIP

**description**: Un ZIP es un formato de archivo comprimido que permite empaquetar uno o más archivos en un solo archivo más pequeño para almacenamiento o transferencia. Muy común en distribución de software, copias de seguridad y transmisión de archivos por internet.

**type**: Los archivos ZIP son formatos para almacenar y transferir datos/comprimidos porlo que son de tipo unicamente de file tranfer. No son APIs ni protocolos de comunicación, sino archivos que se mueven o almacenan usando métodos de transferencia de archivos.

**protocols**: ZIP es solo un formato de archivo, no un protocolo de red. Se puede transferir usando otros protocolos como HTTP, FTP, SFTP, etc.

**dataFormats**: LoLos archivos ZIP están en formato binario, y contienen tanto los archivos como los metadatos de compresión. 

**security**: ZIP puede tener seguridad propia a nivel de archivo, que generalmente es una protección con contraseña.

**version**:La versión más reciente del estándar ZIP es la 6.3.10 de 2022.

**status**: Activo

**documentation**: https://www.loc.gov/preservation/digital/formats/fdd/fdd000362.shtml?utm

## Interfaz 005

**name**: HTTP

**description**: HTTP significa HyperText Transfer Protocol (Protocolo de Transferencia de Hipertexto). Es el protocolo fundamental que se usa para la comunicación en la web. Permite que los navegadores (como Chrome, Firefox) y los servidores web intercambien información.

**type**: HTTP es el protocolo base que puede soportar muchos tipos de servicios como REST API (muy comúnmente usado con HTTP), REST y SOAP.

**protocols**: HTTP es un protocolo de texto sin estado (stateless), basado en solicitudes y respuestas entre cliente y servidor. Opera generalmente sobre TCP en el puerto 80 (HTTP) o 443 (HTTPS).

**dataFormats**: HTTP no impone un formato específico, sino que el formato depende del contenido (Content-Type). Sin embargo HTTP puede transportar múltiples formatos de datos, algunos comunes son:
HTML (páginas web)
JSON (intercambio de datos en APIs REST)
XML (en SOAP y otros)
Texto plano
Imágenes, videos, archivos binarios, etc.

**security**: HTTP no es seguro por sí mismo (los datos viajan en texto plano). La seguridad se logra con HTTPS, que es HTTP sobre TLS (Transport Layer Security), cifrando la comunicación entre cliente y servidor.

**version**: La versión más reciente es HTTP/2 del 2015, en esta se mejora de manera muy importante el rendimiento y enviando flujos de datos simultáneamente a través de un solo canal o medio de comunicación (multiplexación).

**status**: Activo

**documentation**: https://developer.mozilla.org/en-US/docs/Web/HTTP

## Interfaz 006

**name**: Web Socket

**description**: WebSocket es un protocolo de comunicación que permite abrir una conexión constante y bidireccional entre un cliente (por ejemplo, un navegador) y un servidor. Esto significa que ambos pueden enviarse mensajes entre sí en cualquier momento, sin necesidad de que el cliente haga una nueva solicitud cada vez como ocurre con HTTP. 

**type**: Protocolo de comunicación en tiempo real. WebSocket es un protocolo propio, que es un tipo distinto de comunicación en tiempo real muy diferente a REST API o File Transfer.

**protocols**: WebSocket es un protocolo propio.

**dataFormats**: Permite transmitir datos en:
Texto (normalmente UTF-8)
Binario (por ejemplo, imágenes, archivos, formatos serializados como Protobuf)

**security**: HTTP no es seguro por sí mismo (los datos viajan en texto plano). La seguridad se logra con HTTPS, que es HTTP sobre TLS (Transport Layer Security), cifrando la comunicación entre cliente y servidor.WebSocket puede funcionar sobre:
ws:// (WebSocket sin cifrar)
wss:// (WebSocket seguro, que usa TLS para cifrar la conexión). Este es el equivalente a HTTPS para WebSocket, protegiendo la comunicación de escuchas y ataques.

**version**: El protocolo WebSocket fue estandarizado por el IETF en la RFC 6455 en diciembre de 2011.

**status**: Activo

**documentation**: https://developer.mozilla.org/en-US/docs/Web/HTTP
https://devcenter.heroku.com/articles/websocket-security?utm_source=chatgpt.com

## Interfaz 007

**name**: SSE SERVER-SENT EVENT

**description**: SSE significa Eventos Enviados por el Servidor. Es una tecnología web que permite que el servidor envíe datos automáticamente al navegador (cliente) de forma continua, a través de una conexión HTTP mantenida abierta.Es un canal unidireccional: el servidor puede enviar mensajes al cliente, pero el cliente no puede responder por el mismo canal.

**type**: Es de tipo event stream. SSE se usa cuando necesitas actualizaciones automáticas y en tiempo real desde el servidor, como por ejemplo:
Notificaciones en tiempo real
Resultados de eventos deportivos
Actualización de feeds o dashboards
Streaming de datos de sensores o IoT (si no se necesita comunicación en ambos sentidos)

**protocols**: Esta basado en HTTP.

**dataFormats**: Texto plano, usando formato MIME: text/event-stream

**security**: SSE no tiene seguridad propia. La seguridad depende del protocolo de transporte y usualmente utilizas HTTPS (TLS) para cifrar la conexión.

**status**: Activo

**documentation**: https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events

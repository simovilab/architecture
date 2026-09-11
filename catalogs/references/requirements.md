preguntas clave

¿Qué debe hacer el sistema?

 Proveer rastreo en tiempo real, notificaciones de alerta e información estática de mapas, horarios y rutas [1].

¿Qué cambios son necesarios para cumplir los objetivos?

 Adopción de estándares (GTFS/GTFS-Realtime), despliegue de telemetría a bordo (OBU, conectividad), procesos de seguridad/privacidad y gobernanza de datos (SIMI y ARC-IT sugieren  gobernanza operativa) [2].

¿Cómo se plantean los requisitos de un sistema informático?

 Siguiendo IEEE Std 830: se documentan introducción, descripción general, requisitos específicos (funcionales, rendimiento, interfaces, bases de datos, atributos y constraints), con trazabilidad, verificación y apportioning. Usa plantillas (por modo, por user class, por feature) según convenga [3].

En base a los requisitos funcionales para el sistema de transporte inteligente:

  1. Registro, monitoreo y localización en tiempo real de unidades mediante GPS y redes móviles [2].
  2. Consulta pública de rutas, horarios y tiempos de llegada por aplicación web o móvil [2].
  3. Gestión y validación de datos por parte del Consejo de Transporte Público (CTP) y la ARESEP [2].
  4. Canal de alertas automáticas por emergencias enviado desde la CNE [2].
  5. Módulo de retroalimentación ciudadana gestionado por las municipalidades [2].

Se proponen los siguientes requisitos basándose en las referencias [3], [4] y [5]: 

id: requirement:001
name: Real-Time Data Message Exchange
description: El sistema deberá transmitir posiciones de vehículos, actualizaciones de viajes y alertas dentro de un único FeedMessage para garantizar una comunicación en tiempo real consistente.
type: Functional
priority: High
status: In Review
rationale: Contenedor central de todos los datos GTFS-Realtime. Garantiza sincronización y entrega confiable de actualizaciones.
stakeholders: [Operadores de Transporte Público, Desarrolladores de Aplicaciones, CTP, ARESEP]
acceptanceCriteria:
  - FeedMessage incluye cabecera y bloques de entidades para vehículos, viajes y alertas
  - El mensaje se actualiza al menos cada 30 segundos
  - El formato del mensaje valida contra el esquema GTFS-Realtime
relatedComponents: [API de Datos en Tiempo Real, Agregador de Datos, Servicio de Mensajería en la Nube]
relatedInterfaces: [Endpoint API GTFS-Realtime, Aplicaciones Web/Móviles]
relatedDataEntities: [TripUpdate, VehiclePosition, Alert]
relatedActors: [Sistema del Operador de Transporte, Usuarios Finales, Reguladores]
relación con requisito Funcional: [1, 2, 3]


id: requirement:002
name: Real-Time Feed Metadata
description: El sistema deberá proveer un FeedHeader que incluya marca de tiempo y versión para validar la vigencia y compatibilidad de los datos.
type: Functional
priority: High
status: In Review
rationale: Permite a reguladores y aplicaciones verificar si los datos recibidos son actuales y cumplen con la versión GTFS-Realtime.
stakeholders: [CTP, ARESEP, Desarrolladores de Aplicaciones]
acceptanceCriteria:
  - FeedHeader incluye feed_version y timestamp
  - La marca de tiempo no difiere más de 10 segundos del tiempo del servidor
relatedComponents: [Publicador de Datos, Servicio de Validación]
relatedInterfaces: [Endpoint API GTFS-Realtime]
relatedDataEntities: [FeedHeader]
relatedActors: [Agencias Reguladoras, Aplicaciones]
relación con requisito Funcional: [1, 2, 3]

id: requirement:003
name: Real-Time Vehicle Location
description: El sistema deberá proporcionar en tiempo real la latitud, longitud, dirección y velocidad de cada vehículo en operación.
type: Functional
priority: Critical
status: In Review
rationale: Requisito central para el rastreo GPS, monitoreo y aplicaciones públicas.
stakeholders: [Pasajeros, Operadores de Transporte, CTP, ARESEP]
acceptanceCriteria:
  - Precisión de localización dentro de 10 metros
  - Actualizaciones al menos cada 15 segundos
  - El ID del vehículo coincide con un vehículo registrado en la base de datos
relatedComponents: [Dispositivo GPS, Red Móvil, Servidor en Tiempo Real]
relatedInterfaces: [Endpoint GTFS-Realtime VehiclePositions, Mapas Web/Móviles]
relatedDataEntities: [VehiclePosition, Position, VehicleDescriptor]
relatedActors: [Conductores, Sistema IT del Operador, Pasajeros]
relación con requisito Funcional: [1]

id: requirement:004
name: Trip Schedule Updates
description: El sistema deberá proporcionar tiempos previstos de llegada y salida en cada parada, incluyendo retrasos o adelantos.
type: Functional
priority: Critical
status: In Review
rationale: Esencial para sistemas de información al pasajero y validación regulatoria del cumplimiento del servicio.
stakeholders: [Pasajeros, Desarrolladores de Aplicaciones, CTP, ARESEP]
acceptanceCriteria:
  - Tiempos previstos disponibles para todos los viajes activos
  - El campo de retraso se llena cuando el servicio se desvía más de 60 segundos
  - Vinculado al GTFS estático mediante TripDescriptor
relatedComponents: [Motor de Predicción de Horarios, Servicio de Integración de Datos]
relatedInterfaces: [Endpoint GTFS-Realtime TripUpdates, Aplicaciones Web/Móviles]
relatedDataEntities: [TripUpdate, StopTimeUpdate, TripDescriptor]
relatedActors: [Pasajeros, Operadores de Transporte, Reguladores]
relación con requisito Funcional: [1, 2]

id: requirement:005
name: Trip Identification
description: El sistema deberá identificar cada viaje activo con referencia al feed GTFS estático para validación y consistencia de horarios.
type: Functional
priority: High
status: In Review
rationale: Garantiza que las actualizaciones en tiempo real estén correctamente asociadas con los viajes planificados.
stakeholders: [CTP, ARESEP, Operadores de Transporte]
acceptanceCriteria:
  - Cada TripUpdate contiene un TripDescriptor válido
  - TripDescriptor coincide con trip_id del GTFS estático
relatedComponents: [Validador de Datos, Capa de Integración en Tiempo Real]
relatedInterfaces: [API GTFS-Realtime, Feed GTFS Estático]
relatedDataEntities: [TripDescriptor]
relatedActors: [Agencias Reguladoras, Operadores de Transporte]
relación con requisito Funcional: [2, 3]

id: requirement:006
name: Vehicle Identification
description: El sistema deberá identificar de manera única los vehículos en tiempo real para auditoría, monitoreo y reportes.
type: Functional
priority: High
status: In Review
rationale: Permite a reguladores y operadores rastrear desempeño y cumplimiento de los vehículos.
stakeholders: [CTP, ARESEP, Operadores de Transporte]
acceptanceCriteria:
  - Cada VehiclePosition incluye un VehicleDescriptor único
  - VehicleDescriptor corresponde a un vehículo registrado por el operador
relatedComponents: [Sistema de Gestión de Flota, Base de Datos Regulatoria]
relatedInterfaces: [Endpoint GTFS-Realtime VehiclePositions]
relatedDataEntities: [VehicleDescriptor, VehiclePosition]
relatedActors: [Operadores de Transporte, Reguladores]
relación con requisito Funcional: [1, 3]

id: requirement:007
name: Real-Time Service Alerts
description: El sistema deberá proveer alertas sobre emergencias, interrupciones del servicio y desvíos de rutas con rango de tiempo, severidad, causa y entidades afectadas.
type: Functional
priority: Critical
status: In Review
rationale: Permite comunicación de emergencias (CNE), mejora la seguridad de los pasajeros y asegura transparencia en cambios del servicio.
stakeholders: [Pasajeros, CNE, Operadores de Transporte, CTP, Municipalidades]
acceptanceCriteria:
  - Las alertas incluyen título, descripción y rutas/paradas afectadas
  - Las alertas tienen rango de tiempo activo
  - Campos de Severidad, Causa y Efecto están completados
relatedComponents: [Interfaz de Gestión de Emergencias, Sistema de Distribución de Alertas]
relatedInterfaces: [Endpoint GTFS-Realtime Alerts, Notificaciones Web/Móviles]
relatedDataEntities: [Alert, TimeRange, EntitySelector, Cause, Effect, SeverityLevel]
relatedActors: [CNE, Pasajeros, Municipalidades, Operadores]
relación con requisito Funcional: [2, 3, 4]

id: requirement:008
name: Citizen Feedback Integration
description: El sistema deberá proveer un módulo de retroalimentación donde los pasajeros puedan enviar comentarios, quejas o sugerencias sobre rutas, vehículos y paradas, los cuales serán gestionados por las municipalidades.
type: Functional
priority: High
status: In Review
rationale: Promueve la transparencia, la participación ciudadana y la mejora continua del servicio de transporte. Se alinea con las prácticas de gobernanza en Costa Rica donde las municipalidades atienden la retroalimentación comunitaria.
stakeholders: [Pasajeros, Municipalidades, CTP, ARESEP, Operadores de Transporte]
acceptanceCriteria:
  - Los pasajeros pueden enviar retroalimentación vía aplicaciones web o móviles
  - La retroalimentación se categoriza (queja, sugerencia, incidente, etc.)
  - Las municipalidades cuentan con una interfaz para revisar, clasificar y responder
  - Se pueden generar reportes y compartir con reguladores (CTP, ARESEP)
relatedComponents: [Portal de Retroalimentación Ciudadana, Panel de Gestión Municipal, Sistema de Notificaciones]
relatedInterfaces: [Aplicaciones Web/Móviles, Sistema de Información Municipal, Interfaz de Reportes Regulatorios]
relatedDataEntities: [FeedbackEntry, FeedbackCategory, UserProfile, FeedbackResponse]
relatedActors: [Pasajeros, Funcionarios Municipales, CTP, ARESEP, Operadores de Transporte]
relación con requisito Funcional: [5]




En base a los requisitos no funcionales para el sistema de transporte inteligente:

  1. Escalabilidad para integrar nuevos operadores o municipalidades sin rediseño estructural [2].
  2. Cumplimiento con WCAG 2.1 en accesibilidad digital [2].
  3. Soporte multilingüe: español e inglés como mínimo [2].
  4. Alta disponibilidad (>99%) y mecanismos de recuperación ante fallos [2].
  5. Cumplimiento con la Ley 8968 de protección de datos [2].

Se proponen los siguientes requisitos basándose en las referencias [3], [4], [5], [6] y [7]:

id: requirement:009
name: Soporte Multilingüe
description: El sistema deberá permitir que todos los mensajes de texto en la aplicación y alertas tengan versiones en al menos español e inglés.
type: Non-Functional
priority: High
status: In Review
rationale: Permite atender a usuarios de diferentes idiomas y cumplir con estándares internacionales de accesibilidad y usabilidad.
stakeholders: [Pasajeros, Operadores de Transporte, Desarrolladores de Aplicaciones, CTP, ARESEP]
acceptanceCriteria:
  - Todos los textos visibles al usuario tienen traducción al español e inglés
  - Traducciones verificadas y consistentes con los mensajes originales
  - La selección de idioma se aplica automáticamente según la configuración del usuario
relatedComponents: [Motor de Mensajes, Servidor de Aplicaciones, Base de Datos de Textos Multilingües]
relatedInterfaces: [API de Aplicaciones Web/Móviles, Endpoint GTFS-Realtime]
relatedDataEntities: [TranslatedString, TripUpdate, Alert]
relatedActors: [Usuarios Finales, Operadores de Transporte, Reguladores]
relación con requisito No Funcional: [3]

id: requirement:010
name: Recursos Multimedia Multilingües
description: El sistema deberá proporcionar imágenes y recursos multimedia localizados que se adapten al idioma del usuario.
type: Non-Functional
priority: Medium
status: In Review
rationale: Mejora la comprensión de la información y cumple con estándares de accesibilidad y experiencia de usuario multilingüe.
stakeholders: [Pasajeros, Desarrolladores de Aplicaciones, Operadores de Transporte]
acceptanceCriteria:
  - Todas las imágenes y iconos de mensajes importantes tienen versión para español e inglés
  - La imagen mostrada se corresponde con el idioma seleccionado por el usuario
relatedComponents: [Repositorio de Imágenes Localizadas, Motor de Presentación de UI]
relatedInterfaces: [Aplicaciones Web/Móviles]
relatedDataEntities: [LocalizedImage, TranslatedImage]
relatedActors: [Usuarios Finales, Desarrolladores]
relación con requisito No Funcional: [3]

id: requirement:011
name: Información de Accesibilidad
description: El sistema deberá indicar la accesibilidad de paradas y vehículos para personas con movilidad reducida, cumpliendo con WCAG 2.1.
type: Non-Functional
priority: High
status: In Review
rationale: Garantiza que la información de transporte sea accesible para todos los usuarios, cumpliendo normas de accesibilidad digital y física.
stakeholders: [Pasajeros con Discapacidad, Operadores de Transporte, CTP, ARESEP]
acceptanceCriteria:
  - Todos los vehículos y paradas indican el estado de accesibilidad
  - La información es visualmente accesible en aplicaciones web y móviles
  - Compatible con lectores de pantalla y estándares WCAG 2.1
relatedComponents: [Base de Datos de Paradas y Vehículos, Motor de Presentación UI]
relatedInterfaces: [Aplicaciones Web/Móviles]
relatedDataEntities: [WheelchairBoarding, Stop, VehiclePosition]
relatedActors: [Usuarios con Discapacidad, Operadores, Reguladores]
relación con requisito No Funcional: [2]

id: requirement:012
name: Adaptabilidad de Viajes
description: El sistema deberá permitir modificar dinámicamente los viajes y rutas sin necesidad de rediseño estructural del sistema.
type: Non-Functional
priority: Critical
status: In Review
rationale: Facilita la escalabilidad para integrar nuevos operadores o municipalidades y soporta cambios operativos sin interrupciones.
stakeholders: [Operadores de Transporte, Municipalidades, CTP, ARESEP]
acceptanceCriteria:
  - Nuevos viajes o cambios de rutas pueden agregarse o modificarse sin reiniciar el sistema
  - El feed en tiempo real refleja inmediatamente los cambios
  - No se requieren cambios en la base de datos estática existente
relatedComponents: [Motor de Modificación de Viajes, Integración GTFS-Realtime]
relatedInterfaces: [API GTFS-Realtime, Dashboard de Operadores]
relatedDataEntities: [TripModifications, TripUpdate, StopTimeUpdate]
relatedActors: [Operadores, Administradores de Sistema, Reguladores]
relación con requisito No Funcional: [1, 4]

id: requirement:013
name: Gestión de Paradas Dinámicas
description: El sistema deberá permitir reemplazar o seleccionar paradas afectadas por cambios o desvíos sin modificar la estructura general de rutas.
type: Non-Functional
priority: High
status: In Review
rationale: Permite escalar y adaptarse a nuevos operadores o situaciones imprevistas sin reestructurar la base de datos o el feed de rutas.
stakeholders: [Operadores de Transporte, Municipalidades, CTP]
acceptanceCriteria:
  - Se pueden definir paradas alternativas para viajes en tiempo real
  - La información se actualiza automáticamente en el feed GTFS-Realtime
relatedComponents: [Gestor de Paradas, Motor de Integración de Datos]
relatedInterfaces: [API GTFS-Realtime, Aplicaciones Web/Móviles]
relatedDataEntities: [StopSelector, ReplacementStop, StopTimeUpdate]
relatedActors: [Operadores, Pasajeros, Reguladores]
relación con requisito No Funcional: [1, 4]

id: requirement:014
name: Representación de Trayectorias
description: El sistema deberá representar de manera flexible las trayectorias de los vehículos, permitiendo cambios de ruta y soporte multilingüe en información de rutas.
type: Non-Functional
priority: Medium
status: In Review
rationale: Facilita escalabilidad y visualización clara de rutas, incluyendo soporte para diferentes idiomas en la presentación de trayectorias.
stakeholders: [Operadores de Transporte, Pasajeros, Desarrolladores de Aplicaciones]
acceptanceCriteria:
  - Todas las rutas están representadas por shapes válidos
  - Cambios en trayectorias se reflejan en tiempo real sin alterar la estructura base
  - Información de rutas visualizada incluye etiquetas en múltiples idiomas
relatedComponents: [Motor de Mapas, Base de Datos de Shapes]
relatedInterfaces: [Aplicaciones Web/Móviles, API GTFS-Realtime]
relatedDataEntities: [Shape, TripUpdate]
relatedActors: [Pasajeros, Operadores, Desarrolladores]
relación con requisito No Funcional: [1, 3, 4]

id: requirement:015
name: Información de Paradas
description: El sistema deberá proveer información detallada de paradas incluyendo accesibilidad y nombres multilingües.
type: Non-Functional
priority: High
status: In Review
rationale: Mejora la experiencia del usuario, cumple WCAG 2.1 y facilita integración de nuevos operadores o municipalidades.
stakeholders: [Pasajeros, Operadores, CTP, ARESEP]
acceptanceCriteria:
  - Todas las paradas incluyen nombre en español e inglés
  - Información de accesibilidad disponible y visible según WCAG 2.1
  - Se pueden agregar nuevas paradas sin reestructurar el sistema
relatedComponents: [Base de Datos de Paradas, API de Información de Paradas]
relatedInterfaces: [Aplicaciones Web/Móviles, Endpoint GTFS-Realtime]
relatedDataEntities: [Stop, WheelchairBoarding, TranslatedString]
relatedActors: [Pasajeros, Operadores, Reguladores]
relación con requisito No Funcional: [1, 2, 3]

id: requirement:016
name: Protección de Datos de Ubicación de Vehículos
description: El sistema deberá garantizar que cualquier información de ubicación de vehículos que pueda identificar a conductores y/o pasajeros sea tratada conforme a la Ley 8968, asegurando confidencialidad y seguridad.
type: Non-Functional
priority: Critical
status: In Review
rationale: Previene la exposición de datos personales de conductores y/o pasajeros y cumple con las regulaciones legales de Costa Rica.
stakeholders: [Conductores, Operadores de Transporte, CTP, ARESEP, Pasajeros]
acceptanceCriteria:
  - La ubicación de los vehículos se almacena y transmite de forma segura
  - No se divulga información que identifique directamente a los conductores y/o pasajeros sin consentimiento
  - Los datos cumplen con los estándares de confidencialidad y seguridad requeridos
relatedComponents: [Servidores de Datos, Base de Datos de Vehículos, Sistema de Seguridad de Información]
relatedInterfaces: [API GTFS-Realtime VehiclePositions, Aplicaciones Web/Móviles]
relatedDataEntities: [VehiclePosition, VehicleDescriptor, Position]
relatedActors: [Conductores, Administradores de Flota, Reguladores]
relación con requisito No Funcional: [5]






En base a los requisitos de rendimiento para el sistema de transporte inteligente:

1. Visualización de datos para al menos 5,000 unidades móviles concurrentes [2].
2. Actualización de ubicación en menos de 3 segundos [2].
3. Compatibilidad con dispositivos móviles con conectividad 3G o superior [2].
4. Notificación de eventos críticos en un plazo máximo de 60 segundos [2].

Se proponen los siguientes requisitos basándose en las referencias [3], [4] y [5]:

id: requirement:017
name: Actualización de Ubicación de Vehículos
description: El sistema deberá proporcionar la ubicación en tiempo real de todos los vehículos en operación, actualizando su posición al menos cada 3 segundos para garantizar monitoreo continuo.
type: Non-Functional
priority: Critical
status: In Review
rationale: Permite seguimiento preciso de flotas, soporte a aplicaciones de pasajeros y cumplimiento de objetivos de rendimiento en tiempo real.
stakeholders: [Pasajeros, Operadores de Transporte, CTP, ARESEP, Desarrolladores de Aplicaciones]
acceptanceCriteria:
  - Las posiciones se actualizan en menos de 3 segundos desde el cambio real
  - Soporta al menos 5,000 unidades móviles concurrentes
  - Compatible con dispositivos móviles 3G o superior
relatedComponents: [GPS, Servidor en Tiempo Real, Motor de Procesamiento de Posiciones]
relatedInterfaces: [API GTFS-Realtime VehiclePositions, Aplicaciones Web/Móviles]
relatedDataEntities: [VehiclePosition, Position, VehicleDescriptor]
relatedActors: [Conductores, Administradores de Flota, Pasajeros]
relación con requisito de Rendimiento: [1, 2, 3]

id: requirement:018
name: Actualización de Estado de Viajes
description: El sistema deberá actualizar en tiempo real el estado de cada viaje, incluyendo retrasos, cambios de ruta y tiempos estimados de llegada, garantizando notificaciones a los usuarios en menos de 60 segundos.
type: Non-Functional
priority: Critical
status: In Review
rationale: Permite informar a los pasajeros de manera inmediata sobre eventos críticos y mantener la confiabilidad del sistema de transporte.
stakeholders: [Pasajeros, Operadores de Transporte, CTP, ARESEP, Desarrolladores]
acceptanceCriteria:
  - Actualizaciones reflejadas en menos de 60 segundos
  - Soporta visualización de al menos 5,000 vehículos concurrentes
  - Compatible con dispositivos móviles 3G o superior
relatedComponents: [Motor de Predicción de Horarios, Servidor de Datos en Tiempo Real]
relatedInterfaces: [API GTFS-Realtime TripUpdates, Aplicaciones Web/Móviles]
relatedDataEntities: [TripUpdate, StopTimeUpdate, TripDescriptor]
relatedActors: [Pasajeros, Conductores, Reguladores]
relación con requisito de Rendimiento: [1, 2, 3, 4]

id: requirement:019
name: Notificación de Eventos Críticos
description: El sistema deberá enviar alertas en tiempo real sobre interrupciones de servicio, emergencias o eventos críticos, asegurando que los usuarios reciban la información en menos de 60 segundos.
type: Non-Functional
priority: Critical
status: In Review
rationale: Garantiza seguridad y confianza en el servicio, permitiendo a los pasajeros y operadores reaccionar ante situaciones críticas de manera oportuna.
stakeholders: [Pasajeros, Operadores de Transporte, CNE, CTP, ARESEP, Municipalidades]
acceptanceCriteria:
  - Las alertas se reciben por el usuario final en menos de 60 segundos
  - Soporta envío simultáneo a 5,000 unidades móviles o más
  - Compatible con dispositivos móviles 3G o superior
relatedComponents: [Sistema de Alertas, Servidor en Tiempo Real, Motor de Distribución de Notificaciones]
relatedInterfaces: [API GTFS-Realtime Alerts, Aplicaciones Web/Móviles, Notificaciones Push]
relatedDataEntities: [Alert, TimeRange, EntitySelector, SeverityLevel, Cause, Effect]
relatedActors: [Usuarios, Operadores, Reguladores, CNE]
relación con requisito de Rendimiento: [1, 3, 4]




Referencias

[1] SIMOVILAB. [Online]. Available: https://github.com/simovilab/context/blob/main/tech
stack.md
[2] SIMI. [Online]. Available: https://simovilab.github.io/sistema-informacion/
[3] 830-1998 - IEEE Recommended Practice for Software Requirements Specifications.
[Online]. Available: https://ieeexplore.ieee.org/document/720574
[4] Arc-It. [Online]. Available: https://www.arc-it.net/index.html
[5] GTFS. [Online]. Available: https://gtfs.org/#
[6] Web Content Accessibility Guidelines 2.1 [Online]. Available: https://www.w3.org/TR/2025/REC-WCAG21-20250506/
[7] Ley de Protección de la Persona frente al tratamiento de sus datos personales [Online]. Available: https://pgrweb.go.cr/scij/Busqueda/Normativa/Normas/nrm_texto_completo.aspx?param1=NRTC&nValor1=1&nValor2=70975&nValor3=85989&strTipM=TC
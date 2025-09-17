preguntas clave

¿Qué debe hacer el sistema?

 Proveer rastreo en tiempo real, APIs públicas/privadas (GTFS + Realtime), gestión de flota y pagos, notificaciones, dashboards operativos y reporting [1].

¿Qué cambios son necesarios para cumplir los objetivos?

 Adopción de estándares (GTFS/GTFS-Realtime), despliegue de telemetría a bordo (OBU + conectividad), arquitectura en microservicios con ingest/streaming, procesos de seguridad/privacidad, acuerdos con PSPs y gobernanza de datos (SIMI y ARC-IT sugieren gobernanza y gobernanza operativa) [2].

¿Cómo se plantean los requisitos de un sistema informático?

 Siguiendo IEEE Std 830: se documentan introducción, descripción general, requisitos específicos (funcionales, rendimiento, interfaces, bases de datos, atributos y constraints), con trazabilidad, verificación y apportioning. Usa plantillas (por modo, por user class, por feature) según convenga [3].

Elementos preliminares

Elementos preliminares (stakeholders, tecnologías, interfaces, organizaciones, actores, etc.)

Stakeholders [4] (grupos)

 Operadores de transporte público (empresas de buses). 
 Autoridad/secretaría de transporte (regulación, control).
 Pasajeros / ciudadanos / usuarios finales. 
 Conductores y personal de flota (consolas en bus). 
 Equipo de operaciones (SOC, soporte). 
 Equipo de planificación / scheduling (planificadores de rutas). 
 Equipo de producto / desarrollo (SW/DevOps). 
 Proveedores de pago / PSP (tarjetas, billeteras móviles). 
 Proveedores de mapas / geocodificación (Google Maps, OpenStreetMap). 
 Proveedores de conectividad / MVNO / operadores móviles. 
 Integradores TI y SIEM (seguridad, auditoría). 
 Agregadores / apps de movilidad (apps de terceros que consumen GTFS). 
 Comunidad / grupos de interés (ONG movilidad, academia). 
  

Tecnologías y componentes tecnológicos [4]

 Dispositivos a bordo: GPS GNSS, modem celular 4G/5G, OBU (on-board unit). 
 Sensores: odómetro, NFC/contactless reader (para pago), puertas, sensores de ocupación (opcional). 
 Edge compute en bus (gateway local para buffering). 
 Backend en la nube: API Gateway, microservicios, base de datos relacional + data lake/warehouse. 
 Protocolos y estándares: GTFS (static), GTFS-Realtime, MQTT/HTTP(S)/WebSocket, HTTPS/REST, Oauth2/OpenID Connect. 
 Mensajería / streaming: Kafka / RabbitMQ (telemetría en tiempo real). 
 Observabilidad: logging centralizado, métricas (Prometheus), tracing.
 CI/CD, contenedores (Docker/Kubernetes).
 Sistemas de pago: integración con PSP, tokenización, PCI-DSS considerations.
 Herramientas GIS / routing engine: OSRM, GraphHopper, Valhalla.
  (Se alinea con tech stack recomendado en repositorios y prácticas ITS). 

Interfaces (externas e internas) [4]

 GTFS Schedule (archivo estático) y GTFS-Realtime feed (vehicle positions, trip updates, service alerts).  
 API pública REST para terceros (rutas, paradas, ETA). 
 Webhooks / push para notificaciones (SMS, push notifications). 
 Interfaces con sistemas de pago (PSP API). 
 Interface con sistemas de control de flota (AVL/MDM). 
 Integración con sistemas de información del operador (ERP, cadence scheduling). 
 Telemetría (MQTT/Kafka) entre buses y backend. 
  (IEEE 830 sugiere documentar cada interfaz — contenido, formato, timing, tolerancia). 

Actores (sistemas y usuarios) [4]

 Actor humano: Pasajero (app móvil, web). 
 Actor humano: Operador/Despacho (dashboard). 
 Actor sistema: GTFS-consumer apps (Google Maps, apps locales). 
 Actor sistema: PSP (pagos). 
 Actor sistema: Sistemas de control de tránsito / autoridad. 
 Actor sistema: Módulo de predicción ETA / ML.
  (Organizar por “user class” u “objetos” es recomendado por IEEE 830 para claridad). 

Catálogo preliminar de requisitos

requirement:001

name: Real-Time Bus Tracking [1] 
description: El sistema deberá proveer la posición en tiempo real de cada unidad de bus (lat, lon, heading, velocidad, timestamp) con actualización mínima cada 5 s/10 s (configurable). 
type: Functional 
priority: Critical 
status: Approved 
rationale: Base para información al pasajero, despacho y análisis operativo; facilita GTFS-Realtime.  
stakeholders: Pasajeros, Operador, Despacho, Autoridad. 
acceptanceCriteria: 95% de los mensajes de posición recibidos en backend con latencia ≤ 10s bajo condiciones normales; precisión GPS ≤ 10 m. 
relatedComponents: OBU (GPS + modem), Edge buffer, Telemetry Ingest service, Position service, DB (timeseries). 
relatedInterfaces: GTFS-Realtime vehicle_positions, MQTT/Kafka ingest.  
relatedDataEntities: vehicle_position(record), vehicle_id, trip_id, timestamp, speed, heading. 
relatedActors: Bus OBU, Backend Ingest, Third-party apps. 



 requirement:002

name: User Authentication 
description: El sistema deberá autenticar usuarios usando OIDC/OAuth2 con roles (rider, operator, admin). 
type: Functional / Security 
priority: High 
status: Approved 
rationale: Protección de APIs y gestión de permisos; separación de privilegios. 
acceptanceCriteria: Login exitoso < 3 s; tokens expirables; roles aplican correctamente en 100% de endpoints. 
relatedComponents: Identity Provider, API Gateway, User profile service. 
relatedInterfaces: OIDC endpoints, Admin UI. 
relatedDataEntities: user_profile, role, token. 
relatedActors: Pasajero, Admin, Operador. 



 requirement:003

name: GTFS Static & Realtime Compatibility  
description: El sistema debe publicar y consumir GTFS Schedule (static) y GTFS-Realtime feeds (vehicle positions, trip updates, service alerts) en formatos estándar [5]. 
type: Functional / Interoperability 
priority: Critical 
status: In Review 
rationale: Interoperabilidad con ecosistema de apps y cumplimiento de prácticas globales.  
acceptanceCriteria: Generación de GTFS static válida (validador) y feed GTFS-Realtime conforme a spec; apps externas pueden suscribirse. 
relatedComponents: GTFS generator, Realtime publisher, Feed validator. 
relatedInterfaces: GTFS files (stops.txt, trips.txt, routes.txt), GTFS-Realtime protobuf endpoint. 
relatedDataEntities: routes, trips, stops, stop_times, vehicle_positions. 
relatedActors: External apps, MobilityData consumers. 



 requirement:004

name: ETA / Arrival Predictions 
description: El sistema deberá calcular ETAs a paradas usando datos de posición en tiempo real y modelos de predicción (ML o reglas heurísticas) [4]. 
type: Functional / Technical 
priority: High 
status: Pending 
rationale: Mejora la experiencia de usuario y la eficiencia operativa. 
acceptanceCriteria: Error medio absoluto (MAE) de ETA ≤ 60 s en condiciones normales; 90% de predicciones disponibles para los próximos 15 min. 
relatedComponents: Prediction service (ML), Historical DB, Stream processor. 
relatedInterfaces: ETA API (public), dashboard. 
relatedDataEntities: historical_trip_data, traffic_conditions, route_segment_times. 
relatedActors: Passenger app, Dispatch. 



 requirement:005

name: Notifications & Alerts (Push/SMS/In-App) 
description: Envío de alertas de servicio (retrasos, cancelaciones) y notificaciones personalizadas (paradas favoritas) [5]. 
type: Functional 
priority: Medium 
status: Pending 
rationale: Comunicación proactiva mejora satisfacción y reduce consultas. 
acceptanceCriteria: 99% de mensajes entregados dentro de SLA (configurable); registro de entrega. 
relatedComponents: Notification service, Push provider, SMS gateway. 
relatedInterfaces: Webhooks, mobile push, SMS API. 
relatedDataEntities: notification, user_subscription. 
relatedActors: Passenger app, Admin. 


requirement:006

name: Admin & Operations Dashboard 
description: Dashboard web para monitoreo de flota, incidentes, KPIs y control manual de rutas/servicios [5]. 
type: Functional / Usability 
priority: High 
status: Pending 
rationale: Operadores necesitan visibilidad y control en tiempo real. 
acceptanceCriteria: Panel con heatmap, unidades en tiempo real, filtros por ruta, alertas configurables. 
relatedComponents: Frontend UI, Backend APIs, Auth. 
relatedInterfaces: Internal API, role-based access. 
relatedDataEntities: live_positions, incidents, kpi_metrics. 
relatedActors: Operations staff, Admin. 



 requirement:007

name: Reporting & Analytics (Batch / Near-real-time) 
description: Generación de informes operativos (punctuality, ridership) y dataset para análisis histórico [5]. 
type: Functional / Business 
priority: Medium 
status: Pending 
rationale: Planeamiento y KPIs para optimización del servicio. 
acceptanceCriteria: Dashboards con KPIs diarios/semana/mes y export CSV/JSON; latencia de 1h para datos agregados. 
relatedComponents: Data warehouse, ETL jobs, BI tools. 
relatedInterfaces: BI connectors (SQL). 
relatedDataEntities: trips, passenger_counts, fares. 
relatedActors: Planners, Analysts. 



 requirement:008

name: Security & Audit Trail 
description: Registro inmutable de acciones críticas (cambios de tarifa, login admin, reconfiguraciones) y logs de acceso [5]. 
type: Non-Functional / Security 
priority: Critical 
status: Approved 
rationale: Cumplimiento, detección de fraude y responsabilidad. 
acceptanceCriteria: Todos los eventos críticos registrados con user_id, timestamp y resultado; retención mínima configurable. 
relatedComponents: SIEM, Audit DB, Auth service. 
relatedInterfaces: Logging API, Admin UI. 
relatedDataEntities: audit_log, access_event. 
relatedActors: Admin, Security team. 



 requirement:009

name: High Availability & Fault Tolerance (SLA) 
description: Backend crítico con disponibilidad ≥ 99.9 % (configurable), tolerante a fallos regionales; failover automático [5]. 
type: Non-Functional / Reliability 
priority: Critical 
status: In Review 
rationale: Servicio en tiempo real exige disponibilidad. 
acceptanceCriteria: RTO/RPO definidos; pruebas de DR realizadas trimestralmente. 
relatedComponents: Load balancers, multi-AZ deployment, DB replicas. 
relatedInterfaces: Healthcheck endpoints. 
relatedDataEntities: service_status, replication_state. 
relatedActors: DevOps, Operations. 



 requirement:010

name: Scalability (throughput) 
description: Soportar crecimiento: tamaño inicial X buses y escalar a 10x sin degradación perceptible [5]. 
type: Non-Functional / Performance 
priority: High 
status: Pending 
rationale: Escalado por aumento de flota o adopción. 
acceptanceCriteria: 95% de eventos procesados < 2 s en picos previstos; auto-scaling validado. 
relatedComponents: Streaming infra, Autoscaling groups. 
relatedInterfaces: Telemetry ingest. 
relatedDataEntities: telemetry_events. 



 requirement:011

name: Privacy & Data Protection (GDPR-like) 
description: Cumplir con la normativa de protección de datos aplicable (anonimización, retención, derecho al olvido) [5]. 
type: Non-Functional / Legal 
priority: Critical 
status: In Review 
rationale: Protección legal y confianza del usuario. 
acceptanceCriteria: PII cifrada at-rest, consentimiento registrado; política de retención implementada. 
relatedComponents: User DB, Consent manager, KMS. 
relatedInterfaces: Data export, Admin data request API. 
relatedDataEntities: user_profile, consent_record.  
relatedActors: Legal, Privacy officer. 



 requirement:012

name: Over-the-Air Updates & Fleet Config Management 
description: Habilitar actualizaciones remotas de configuraciones y firmware limitado (seguro) para OBU [5]. 
type: Technical / Security 
priority: Medium 
status: Pending 
rationale: Mantener seguridad y funciones actualizadas sin intervención física. 
acceptanceCriteria: Firma digital de imágenes; rollback seguro. 
relatedComponents: Device management service, OTA server. 
relatedInterfaces: Device management API. 
relatedDataEntities: device_firmware, device_config. 
relatedActors: Field technicians, DevOps. 



 requirement:013

name: Multi-Modal & Intermodal Support 
description: Soportar transporte multimodal (buses, paratransit) y mostrar conexiones/transfers [5]. 
type: Business / Functional 
priority: Low/Medium 
status: Pending 
rationale: Extensibilidad futura y alineamiento con ARC-IT. 
acceptanceCriteria: Rutas y transfers visibles en UI; integración de datos de otros modos. 
relatedComponents: Routing engine, GTFS aggregator. 
relatedInterfaces: External feeds (other operators). 
relatedDataEntities: mode_type, transfer_node. 
relatedActors: Planners, Users. 



 requirement:014

name: Third-party API & Developer Portal 
description: Publicar APIs documentadas para compartir datos (limítrofes) con desarrolladores y apps [5]. 
type: Functional / Business 
priority: Medium 
status: Pending 
rationale: Ecosistema y visibilidad para pasajeros. 
acceptanceCriteria: Documentación OpenAPI, cuota por API, sandbox. 
relatedComponents: API Gateway, Developer Portal. 
relatedInterfaces: REST/GraphQL endpoints. 
relatedDataEntities: api_key, app_registration. 
relatedActors: Third-party developers, Mobility apps. 

Referencias

[1] SIMOVILAB. [Online]. Available: https://github.com/simovilab/context/blob/main/tech
stack.md
[2] SIMI. [Online]. Available: https://simovilab.github.io/sistema-informacion/
[3] 830-1998 - IEEE Recommended Practice for Software Requirements Specifications.
[Online]. Available: https://ieeexplore.ieee.org/document/720574
[4] Arc-It. [Online]. Available: https://www.arc-it.net/index.html
[5] GTFS. [Online]. Available: https://gtfs.org/#
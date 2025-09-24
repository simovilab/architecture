César Alvarado Castro B60306

Key Questions

What should the system do?

Provide real-time tracking, alert notifications, and static information on maps, schedules, and routes [1].

What changes are necessary to meet the objectives?

Adoption of standards (GTFS/GTFS-Realtime), deployment of on-board telemetry (OBU, connectivity), security/privacy processes, and data governance (SIMI and ARC-IT suggest operational governance) [2].

How are the requirements of an information system defined?

Following IEEE Std 830: documenting introduction, general description, specific requirements (functional, performance, interfaces, databases, attributes, and constraints), with traceability, verification, and apportioning. Templates (by mode, by user class, by feature) are used as needed [3].



Based on the functional requirements for the intelligent transport system:

1. Registration, monitoring, and real-time location of units through GPS and mobile networks [2].
2. Public consultation of routes, schedules, and arrival times via web or mobile application [2].
3. Data management and validation by the Public Transport Council (CTP) and ARESEP [2].
4. Automatic emergency alert channel issued by the CNE [2].
5. Citizen feedback module managed by municipalities [2].

The following requirements are proposed based on references [3], [4], and [5]:



Functional Requirements

id: requirement:001
name: Real-Time Data Message Exchange
description: The system shall transmit vehicle positions, trip updates, and alerts within a single FeedMessage to ensure consistent real-time communication.
type: Functional
priority: High
status: In Review
rationale: Central container for all GTFS-Realtime data. Ensures synchronization and reliable delivery of updates.
stakeholders: [Public Transport Operators, Application Developers, CTP, ARESEP]
acceptanceCriteria:

 FeedMessage includes header and entity blocks for vehicles, trips, and alerts
 Message is updated at least every 30 seconds
 Message format validates against GTFS-Realtime schema
 relatedComponents: [Real-Time Data API, Data Aggregator, Cloud Messaging Service]
 relatedInterfaces: [GTFS-Realtime API Endpoint, Web/Mobile Applications]
 relatedDataEntities: [TripUpdate, VehiclePosition, Alert]
 relatedActors: [Operator’s Transport System, End Users, Regulators]
 implementationOwner: [SIMOVI]
  with Functional Requirement: [1, 2, 3]



id: requirement:002
name: Real-Time Feed Metadata
description: The system shall provide a FeedHeader including timestamp and version to validate the timeliness and compatibility of data.
type: Functional
priority: High
status: In Review
rationale: Allows regulators and applications to verify that received data is current and compliant with GTFS-Realtime versioning.
stakeholders: [Application Developers]
acceptanceCriteria:

 FeedHeader includes feed\_version and timestamp
 Timestamp does not differ by more than 10 seconds from server time
 relatedComponents: [Data Publisher, Validation Service]
 relatedInterfaces: [GTFS-Realtime API Endpoint]
 relatedDataEntities: [FeedHeader]
 relatedActors: [Regulatory Agencies, Applications, CTP, ARESEP]
 implementationOwner: [SIMOVI]
  with Functional Requirement: [1, 2, 3]



id: requirement:003
name: Real-Time Vehicle Location
description: The system shall provide in real time the latitude, longitude, direction (optional), and speed (optional) of each operating vehicle.
type: Functional
priority: Critical
status: In Review
rationale: Core requirement for GPS tracking, monitoring, and public applications.
stakeholders: [Passengers, Transport Operators]
acceptanceCriteria:

 Location accuracy within 10 meters
 Updates at least every 15 seconds
 Vehicle ID matches a registered vehicle in the database
 relatedComponents: [GPS Device, Mobile Network, Real-Time Server]
 relatedInterfaces: [GTFS-Realtime VehiclePositions Endpoint, Web/Mobile Maps]
 relatedDataEntities: [VehiclePosition, Position, VehicleDescriptor]
 relatedActors: [Drivers, Operator IT System, Passengers, CTP, ARESEP]
 implementationOwner: [SIMOVI]
  with Functional Requirement: [1]



id: requirement:004
name: Trip Schedule Updates
description: The system shall provide expected arrival and departure times at each stop, including delays or early arrivals.
type: Functional
priority: Critical
status: In Review
rationale: Essential for passenger information systems and regulatory validation of service compliance.
stakeholders: [Passengers, Application Developers]
acceptanceCriteria:

 Predicted times available for all active trips
 Delay field is filled when service deviates by more than 60 seconds
 Linked to static GTFS via TripDescriptor
 relatedComponents: [Schedule Prediction Engine, Data Integration Service]
 relatedInterfaces: [GTFS-Realtime TripUpdates Endpoint, Web/Mobile Applications]
 relatedDataEntities: [TripUpdate, StopTimeUpdate, TripDescriptor]
 relatedActors: [Passengers, Transport Operators, Regulators, CTP, ARESEP]
 implementationOwner: [SIMOVI]
  with Functional Requirement: [1, 2]



id: requirement:005
name: Trip Identification
description: The system shall identify each active trip with reference to the GTFS Schedule feed for validation and schedule consistency.
type: Functional
priority: High
status: In Review
rationale: Ensures real-time updates are correctly associated with scheduled trips.
stakeholders: [CTP, ARESEP, Transport Operators]
acceptanceCriteria:

 Each TripUpdate contains a valid TripDescriptor
 TripDescriptor matches trip\_id from static GTFS
 relatedComponents: [Data Validator, Real-Time Integration Layer]
 relatedInterfaces: [GTFS-Realtime API, Static GTFS Feed]
 relatedDataEntities: [TripDescriptor]
 relatedActors: [Regulatory Agencies, Transport Operators]
 implementationOwner: [SIMOVI]
  with Functional Requirement: [2, 3]



id: requirement:006
name: Vehicle Identification
description: The system shall uniquely identify vehicles in real time for auditing, monitoring, and reporting.
type: Functional
priority: High
status: In Review
rationale: Allows regulators and operators to track vehicle performance and compliance.
stakeholders: [CTP, ARESEP, Transport Operators]
acceptanceCriteria:

 Each VehiclePosition includes a unique VehicleDescriptor
 VehicleDescriptor corresponds to a registered operator’s vehicle
 relatedComponents: [Fleet Management System, Regulatory Database]
 relatedInterfaces: [GTFS-Realtime VehiclePositions Endpoint]
 relatedDataEntities: [VehicleDescriptor, VehiclePosition]
 relatedActors: [Transport Operators, Regulators]
 implementationOwner: [SIMOVI]
  with Functional Requirement: [1, 3]



id: requirement:007
name: Real-Time Service Alerts
description: The system shall provide alerts on emergencies, service disruptions, and route diversions with time range, severity, cause, and affected entities.
type: Functional
priority: Critical
status: In Review
rationale: Enables emergency communication (CNE), enhances passenger safety, and ensures transparency in service changes.
stakeholders: [Passengers, CNE, Transport Operators, CTP, Municipalities]
acceptanceCriteria:

 Alerts include title, description, and affected routes/stops
 Alerts have an active time range
 Severity, Cause, and Effect fields are completed
 relatedComponents: [Emergency Management Interface, Alert Distribution System]
 relatedInterfaces: [GTFS-Realtime Alerts Endpoint, Web/Mobile Notifications]
 relatedDataEntities: [Alert, TimeRange, EntitySelector, Cause, Effect, SeverityLevel]
 relatedActors: [CNE, Passengers, Municipalities, Operators]
 implementationOwner: [SIMOVI]
  with Functional Requirement: [2, 3, 4]



id: requirement:008
name: Citizen Feedback Integration
description: The system shall provide a feedback module where passengers can submit comments, complaints, or suggestions on routes, vehicles, and stops, managed by municipalities.
type: Functional
priority: High
status: In Review
rationale: Promotes transparency, citizen participation, and continuous improvement of transport services. Aligns with Costa Rican governance practices where municipalities address community feedback.
stakeholders: [Passengers, Municipalities, CTP, ARESEP, Transport Operators]
acceptanceCriteria:

 Passengers can submit feedback via web or mobile apps
 Feedback is categorized (complaint, suggestion, incident, etc.)
 Municipalities have an interface to review, classify, and respond
 Reports can be generated and shared with regulators (CTP, ARESEP)
 relatedComponents: [Citizen Feedback Portal, Municipal Management Dashboard, Notification System]
 relatedInterfaces: [Web/Mobile Applications, Municipal Information System, Regulatory Reporting Interface]
 relatedDataEntities: [FeedbackEntry, FeedbackCategory, UserProfile, FeedbackResponse]
 relatedActors: [Passengers, Municipal Officials, CTP, ARESEP, Transport Operators]
 implementationOwner: [SIMOVI]
  with Functional Requirement: [5]

Based on thenon-functional requirements for the intelligent transport system:

1. Scalability to integrate new operators or municipalities without structural redesign [2].
2. Compliance with WCAG 2.1 digital accessibility standards [2].
3. Multilingual support: Spanish and English at minimum [2].
4. High availability (>99%) and fault recovery mechanisms [2].
5. Compliance with Law 8968 on data protection [2].

The following requirements are proposed based on references [3], [4], [5], [6], and [7]:

id: requirement:009
name: Accessibility Information for Visual Interfaces
description: The system shall indicate accessibility of visual interfaces for people with disabilities, complying with WCAG 2.1.
type: Non-Functional
priority: High
status: In Review
rationale: Ensures transport information is accessible to all users, complying with digital and physical accessibility standards.
stakeholders: [Passengers with Disabilities, Transport Operators, CTP, ARESEP]
acceptanceCriteria:

 All vehicles and stops indicate accessibility status
 Information is visually accessible in web and mobile applications
 Compatible with screen readers and WCAG 2.1 standards
 relatedComponents: [Stops and Vehicles Database, UI Presentation Engine]
 relatedInterfaces: [Web/Mobile Applications]
 relatedDataEntities: [WheelchairBoarding, Stop, VehiclePosition]
 relatedActors: [Users with Disabilities, Operators, Regulators]
 implementationOwner: [SIMOVI]
  with Non-Functional Requirement: [2]



id: requirement:010
name: Trip Adaptability
description: The system shall allow dynamic modification of trips and routes without structural redesign of the system.
type: Non-Functional
priority: Critical
status: In Review
rationale: Facilitates scalability to integrate new operators or municipalities and supports operational changes without service disruption.
stakeholders: [Transport Operators, Municipalities, CTP, ARESEP]
acceptanceCriteria:

 New trips or route changes can be added or modified without restarting the system
 Real-time feed immediately reflects changes
 No changes required in existing static database
 relatedComponents: [Trip Modification Engine, GTFS-Realtime Integration]
 relatedInterfaces: [GTFS-Realtime API, Operator Dashboard]
 relatedDataEntities: [TripModifications, TripUpdate, StopTimeUpdate]
 relatedActors: [Operators, System Administrators, Regulators]
 implementationOwner: [SIMOVI]
  with Non-Functional Requirement: [1, 4]



id: requirement:011
name: Dynamic Stop Management
description: The system shall allow replacement or selection of stops affected by changes or diversions without modifying the overall route structure.
type: Non-Functional
priority: High
status: In Review
rationale: Enables scaling and adaptation to new operators or unforeseen situations without restructuring the database or route feed.
stakeholders: [Transport Operators, Municipalities, CTP]
acceptanceCriteria:

 Alternative stops can be defined for real-time trips
 Information is automatically updated in the GTFS-Realtime feed
 relatedComponents: [Stop Manager, Data Integration Engine]
 relatedInterfaces: [GTFS-Realtime API, Web/Mobile Applications]
 relatedDataEntities: [StopSelector, ReplacementStop, StopTimeUpdate]
 relatedActors: [Operators, Passengers, Regulators]
 implementationOwner: [SIMOVI]
  with Non-Functional Requirement: [1, 4]



id: requirement:012
name: Route Representation
description: The system shall flexibly represent geospatial data of vehicle routes, allowing route changes.
type: Non-Functional
priority: Medium
status: In Review
rationale: Facilitates scalability and clear visualization of routes.
stakeholders: [Transport Operators, Passengers, Application Developers]
acceptanceCriteria:

 All routes are represented by valid shapes
 Route changes are reflected in real time without altering the base structure
 Route information displayed includes labels in multiple languages
 Data exportable in multiple formats for geographic information systems
 relatedComponents: [Map Engine, Shapes Database]
 relatedInterfaces: [Web/Mobile Applications, GTFS-Realtime API]
 relatedDataEntities: [Shape, TripUpdate]
 relatedActors: [Passengers, Operators, Developers]
 implementationOwner: [SIMOVI]
  with Non-Functional Requirement: [1, 3, 4]



id: requirement:013
name: Personal Data Protection
description: The system shall ensure that any real-time information that could identify drivers and/or passengers is handled in compliance with Law 8968, ensuring confidentiality and security.
type: Non-Functional
priority: Critical
status: In Review
rationale: Prevents exposure of personal data of drivers and/or passengers and complies with Costa Rican legal regulations.
stakeholders: [Drivers, Transport Operators, CTP, ARESEP, Passengers]
acceptanceCriteria:

 Vehicle location is securely stored and transmitted
 No information that directly identifies drivers and/or passengers is disclosed without consent
 Data complies with required confidentiality and security standards
 relatedComponents: [Data Servers, Vehicle Database, Information Security System]
 relatedInterfaces: [GTFS-Realtime VehiclePositions API, Web/Mobile Applications]
 relatedDataEntities: [VehiclePosition, VehicleDescriptor, Position]
 relatedActors: [Drivers, Fleet Managers, Regulators]
 implementationOwner: [SIMOVI]
  with Non-Functional Requirement: [5]



Based on theperformance requirements for the intelligent transport system:

1. Data visualization for at least 5,000 concurrent mobile units [2].
2. Location updates in under 3 seconds [2].
3. Compatibility with mobile devices with 3G connectivity or higher [2].
4. Notification of critical events within a maximum of 60 seconds [2].

The following requirements are proposed based on references [3], [4], and [5]:



id: requirement:014
name: Vehicle Location Update
description: The system shall provide the real-time location of all operating vehicles, updating their position at least every 3 seconds to ensure continuous monitoring.
type: Non-Functional
priority: Critical
status: In Review
rationale: Enables accurate fleet tracking, supports passenger applications, and ensures compliance with real-time performance objectives.
stakeholders: [Passengers, Transport Operators, CTP, ARESEP, Application Developers]
acceptanceCriteria:

 Positions update in less than 3 seconds from actual change
 Supports at least 5,000 concurrent mobile units
 Compatible with mobile devices with 3G or higher
 relatedComponents: [GPS, Real-Time Server, Position Processing Engine]
 relatedInterfaces: [GTFS-Realtime VehiclePositions API, Web/Mobile Applications]
 relatedDataEntities: [VehiclePosition, Position, VehicleDescriptor]
 relatedActors: [Drivers, Fleet Managers, Passengers]
 implementationOwner: [SIMOVI]
  with Performance Requirement: [1, 2, 3]



id: requirement:015
name: Trip Status Update
description: The system shall update in real time the status of each trip, including delays, route changes, and estimated arrival times, ensuring notifications to users within 60 seconds.
type: Non-Functional
priority: Critical
status: In Review
rationale: Provides immediate information to passengers about critical events and maintains transport system reliability.
stakeholders: [Passengers, Transport Operators, CTP, ARESEP, Developers]
acceptanceCriteria:

 Updates reflected within 60 seconds
 Supports visualization of at least 5,000 concurrent vehicles
 Compatible with mobile devices with 3G or higher
 relatedComponents: [Schedule Prediction Engine, Real-Time Data Server]
 relatedInterfaces: [GTFS-Realtime TripUpdates API, Web/Mobile Applications]
 relatedDataEntities: [TripUpdate, StopTimeUpdate, TripDescriptor]
 relatedActors: [Passengers, Drivers, Regulators]
 implementationOwner: [SIMOVI]
  with Performance Requirement: [1, 2, 3, 4]



id: requirement:016
name: Critical Event Notification
description: The system shall send real-time alerts on service interruptions, emergencies, or critical events, ensuring users receive the information in less than 60 seconds.
type: Non-Functional
priority: Critical
status: In Review
rationale: Ensures safety and trust in the service, enabling passengers and operators to respond to critical situations in a timely manner.
stakeholders: [Passengers, Transport Operators, CNE, CTP, ARESEP, Municipalities]
acceptanceCriteria:

 Alerts are received by end users within 60 seconds
 Supports simultaneous sending to 5,000 or more mobile units
 Compatible with mobile devices with 3G or higher
 relatedComponents: [Alert System, Real-Time Server, Notification Distribution Engine]
 relatedInterfaces: [GTFS-Realtime Alerts API, Web/Mobile Applications, Push Notifications]
 relatedDataEntities: [Alert, TimeRange, EntitySelector, SeverityLevel, Cause, Effect]
 relatedActors: [Users, Operators, Regulators, CNE]
 implementationOwner: [SIMOVI]
  with Performance Requirement: [1, 3, 4]



References

[1] SIMOVILAB. [Online]. Available: [https://github.com/simovilab/context/blob/main/techstack.md](https://github.com/simovilab/context/blob/main/techstack.md)
[2] SIMI. [Online]. Available: [https://simovilab.github.io/sistema-informacion/](https://simovilab.github.io/sistema-informacion/)
[3] 830-1998 - IEEE Recommended Practice for Software Requirements Specifications. [Online]. Available: [https://ieeexplore.ieee.org/document/720574](https://ieeexplore.ieee.org/document/720574)
[4] Arc-It. [Online]. Available: [https://www.arc-it.net/index.html](https://www.arc-it.net/index.html)
[5] GTFS. [Online]. Available: [https://gtfs.org/#](https://gtfs.org/#)
[6] Web Content Accessibility Guidelines 2.1 [Online]. Available: [https://www.w3.org/TR/2025/REC-WCAG21-20250506/](https://www.w3.org/TR/2025/REC-WCAG21-20250506/)
[7] Law for the Protection of Individuals regarding the Processing of their Personal Data [Online]. Available: [https://pgrweb.go.cr/scij/Busqueda/Normativa/Normas/nrm\_texto\_completo.aspx?param1=NRTC\&nValor1=1\&nValor2=70975\&nValor3=85989\&strTipM=TC](https://pgrweb.go.cr/scij/Busqueda/Normativa/Normas/nrm_texto_completo.aspx?param1=NRTC&nValor1=1&nValor2=70975&nValor3=85989&strTipM=TC)
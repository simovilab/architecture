# Architecture Catalogs Development Project

## Overview

This project aims to develop comprehensive architecture catalogs for the Public Transportation Information System following the TOGAF Architecture Development Method (ADM). A catalog is a fundamental type of artifact in architecture design that provides structured lists of architectural objects, serving as the foundation for informed decision-making throughout the enterprise architecture development process.

## Project Objectives

- **Establish Architecture Foundation**: Create standardized catalogs that serve as authoritative sources of architectural information
- **Enable Informed Decision-Making**: Provide structured data to support architecture governance and strategic planning
- **Support TOGAF ADM Implementation**: Develop artifacts aligned with each phase of the Architecture Development Method
- **Facilitate Stakeholder Communication**: Create clear, accessible documentation of system components and relationships
- **Enable Future Expansion**: Establish extensible frameworks for ongoing catalog development and maintenance

## TOGAF ADM Catalog Mapping

The catalogs are organized according to TOGAF ADM phases, ensuring comprehensive coverage of the architecture development lifecycle:

### Preliminary Phase

- **Principles catalog**: Foundational principles that guide architectural decisions and system design

### Architecture Vision

- **Stakeholder catalog**: Key stakeholders, their roles, interests, and influence levels

### Business Architecture

- **Organization and actor catalog**: Organizations and individuals involved in system operation and governance
- **Business capability catalog**: Core business functions and capabilities (future scope)

### Information Systems Architecture (Data)

- **Data entity and component catalog**: Data structures, entities, and management components

### Application Architecture

- **Application portfolio catalog**: Applications, their relationships, and technical characteristics
- **Interface catalog**: System interfaces and integration points

### Technology Architecture

- **Technology standards catalog**: Adopted technology standards and specifications
- **Technology portfolio catalog**: Technology stack and infrastructure components

### Opportunities and Solutions

- **Implementation factor catalog**: Implementation considerations and constraints (future scope)

### Requirements Management

- **Requirements catalog**: Functional and non-functional system requirements

## Team Assignments and Responsibilities

| Catalog                  | Assignee | Status         | Key Deliverables                            |
| ------------------------ | -------- | -------------- | ------------------------------------------- |
| Principles               | Fabián   | 🔄 In Progress | Architecture principles, design guidelines  |
| Stakeholders             | Jose     | 🔄 In Progress | Stakeholder mapping, influence analysis     |
| Organizations and actors | Jose     | 🔄 In Progress | Organizational structure, key personnel     |
| Data entities/components | Jostin   | 🔄 In Progress | Data models, component definitions          |
| Application portfolio    | Pedro    | 🔄 In Progress | Application inventory, characteristics      |
| Interfaces               | Oriana   | 🔄 In Progress | Interface specifications, protocols         |
| Technology standards     | Randy    | 🔄 In Progress | Standards adoption, compliance guidelines   |
| Technology portfolio     | Randy    | 🔄 In Progress | Technology stack, infrastructure components |
| Requirements             | César    | 🔄 In Progress | System requirements, constraints            |

## Technical Implementation

### Data Structure Standards

- **Identifier Patterns**: Consistent ID schemes (`catalog-type:XXX` format)
- **Metadata Framework**: Standardized metadata including version, authorship, and licensing
- **YAML Format**: Human-readable, version-controllable format
- **Schema Validation**: JSON Schema validation for data integrity

### Quality Assurance

- **VS Code Integration**: Real-time validation during development (Red Hat YAML extension)
- **Documentation Alignment**: Issue descriptions match actual data structures
- **Peer Review Process**: Cross-team validation and feedback
- **Continuous Improvement**: Iterative enhancement based on usage patterns

## Strategic Context

### Domain Focus

Public Transportation Information System for Costa Rica, developed by the Laboratorio de Sistemas Inteligentes de Movilidad (SIMOVI) at Universidad de Costa Rica.

### Key Standards and Frameworks

- **TOGAF ADM**: Primary architecture methodology
- **ARC-IT**: Transportation system architecture reference
- **GTFS/GTFS-Realtime**: Transit data standards
- **SIMOVI Best Practices**: Local expertise and research

### Expected Outcomes

- **Architecture Governance**: Establish foundation for consistent architectural decisions
- **System Integration**: Enable effective integration with existing transportation infrastructure
- **Stakeholder Alignment**: Provide clear communication tools for diverse stakeholder groups
- **Future Scalability**: Create extensible framework for system evolution

## Main References

- [TOGAF Standard](https://pubs.opengroup.org/togaf-standard/adm/chap01.html) - Architecture Development Method
- [ARC-IT](https://www.arc-it.net/index.html) - Transportation Systems Architecture
- [GTFS](https://gtfs.org/) - General Transit Feed Specification
- [SIMOVI Research](https://simovilab.github.io/) - Intelligent Mobility Systems Laboratory
- SITGAM - Geographic Information System for Transportation Management

## Delivery Standards

- **Format**: YAML files in `catalogs/` directory
- **Validation**: JSON Schema compliance
- **Documentation**: Comprehensive issue descriptions with data structure specifications
- **Version Control**: Git-based collaborative development
- **License**: Creative Commons Attribution 4.0 (CC BY 4.0)

# Principles Catalog

File: `architecture/catalogs/principles.yaml`

## Definition according to TOGAF

> The purpose of the Principles catalog is to capture the key principles that will inform and guide how the organization fulfills its mission through IT. Principles are general rules and guidelines, intended to be enduring and seldom amended, that inform and support the way in which an organization sets about fulfilling its mission. These principles will be based on an organization's values, and will guide the organization in its use of IT. The Principles catalog provides a foundation for decision-making throughout the enterprise and a basis for architecture governance. The Principles catalog contains the following metamodel entities: Principle.

## Data structure

Each principle entry contains the following fields:

- **id**: Unique identifier following pattern `principles:XXX` (3 digits)
- **domain**: The architectural domain (e.g., "Software Architecture", "Data Architecture", "Technology Architecture")
- **name**: The principle name (e.g., "Separation of Concerns")
- **description**: Clear statement of what the principle requires
- **rationale**: Why this principle is important and beneficial
- **implications**: What this principle means for implementation and decision-making
- **related_principles**: List of IDs of related principles
- **references**: External links or documentation supporting the principle

## Current catalog content

The catalog currently contains foundational software architecture principles:

- **principles:001** - Separation of Concerns
- **principles:002** - Single Responsibility Principle
- **principles:003** - Don't Repeat Yourself (DRY)

## Relevant questions

- What are the fundamental principles that should guide the design and implementation of intelligent transportation systems?
- How should software architecture principles support public transportation information systems?
- What domain-specific principles are needed for data architecture, application architecture, and technology architecture?
- How do these principles align with SIMOVI's organizational values and mission?

## Expected expansion areas

- **Data Architecture principles**: Interoperability, open standards (GTFS), real-time data quality
- **Application Architecture principles**: Microservices, API-first design, service-oriented architecture
- **Technology Architecture principles**: Cloud-native, vendor neutrality, scalability
- **Security principles**: Data privacy, secure APIs, authentication/authorization
- **Integration principles**: Standardized interfaces, event-driven architecture

## Main references

- TOGAF Standard principles guidelines
- SIMOVI system design principles
- Mobility Data Interoperability Principles (MDIP)
- TransitOPS Manifesto
- MACH Principles

# Stakeholder Catalog

File: `architecture/catalogs/stakeholder.yaml`

## Definition according to TOGAF

> The purpose of the Stakeholder catalog is to identify the stakeholders for the architecture engagement, their influence over the engagement, and their key questions, issues, or concerns that must be addressed by the architecture framework. The Stakeholder catalog is referenced in creating a stakeholder map, showing which stakeholders are involved with a specific aspect of the Enterprise Architecture, their level of involvement, and their key concerns. Understanding stakeholders and their requirements allows an architect to focus effort in areas that meet the needs of stakeholders (see the TOGAF Standard — ADM Techniques). Due to the potentially sensitive nature of stakeholder mapping information and the fact that the Architecture Vision phase is intended to be conducted using informal modeling techniques, no specific metamodel entities will be used to generate a Stakeholder catalog.

## Data structure

Each stakeholder entry contains the following fields:

- **id**: Unique identifier following pattern `stakeholder:XXX` (3 digits)
- **name**: The stakeholder name or group (e.g., "Passengers", "Bus Operators")
- **description**: Detailed description of who this stakeholder is
- **role**: Their primary role in the system (e.g., "End Users", "Service Providers", "Regulators")
- **interests**: List of key interests, concerns, or requirements they have
- **influence**: Level of influence over the system (High/Medium/Low)
- **priority**: Priority level for engagement (High/Medium/Low)

## Current catalog content

The catalog currently contains key stakeholders for the public transportation system:

- **stakeholder:001** - Passengers (End Users)
- **stakeholder:002** - Bus Operators (Service Providers)
- **stakeholder:003** - City Transportation Authorities (Regulators and Planners)
- **stakeholder:004** - Maintenance Teams (Support Staff)
- **stakeholder:005** - IT Support Staff (Technical Support)

## Relevant questions

- Who are the organizations that participate in public transportation management in Costa Rica?
- What are their roles and responsibilities in the transportation ecosystem?
- Who manages the implementation of digital technologies?
- What are the specific interests and concerns of each stakeholder group?
- How should stakeholder influence and priority be assessed and managed?

## Expected expansion areas

- **Government entities**: ARESEP, CTP, MOPT, municipalities
- **Financial stakeholders**: Payment processors, banking institutions
- **Technology vendors**: Software providers, hardware suppliers
- **Research organizations**: Universities, think tanks (SIMOVI, Lanamme, ProDUS)
- **Civil society**: NGOs, passenger advocacy groups
- **International organizations**: GIZ, European Union, IDB, World Bank

## Main references

- SITGAM (attached document)
- Electronic payment committee (attached document)
- ARESEP, CTP, MOPT documentation
- Subject researchers (Lanamme, ProDUS, SIMOVI, etc.)
- NGOs (CPSU, etc.)
- Multilateral organizations (GIZ, European Union, CRUSA Foundation, IDB, etc.)

# Organization and Actor Catalog

File: `architecture/catalogs/organization-actor.yaml`

## TOGAF description

> The purpose of the Organization/Actor catalog is to capture a definitive listing of all participants that interact with IT, including users and owners of IT systems. The Organization/Actor catalog can be referenced when developing requirements in order to test for completeness. For example, requirements for an application that services customers can be tested for completeness by verifying exactly which customer types need to be supported and whether there are any particular requirements or restrictions for user types. The Organization/Actor catalog contains the following metamodel entities: Organization Unit, Actor, Location (may be included in this catalog if an independent Location catalog is not maintained)

## Data structure

The catalog contains two main sections:

### Organizations

Each organization entry contains the following fields:

- **id**: Unique identifier following pattern `organization:XXX` (3 digits)
- **name**: The organization's full name
- **description**: Brief description of the organization's purpose
- **type**: Organization type (e.g., "Research Lab", "Government Agency", "Private Company")
- **contact**: Primary contact information (email/phone)
- **website**: Organization's website URL
- **location**: Physical location or address
- **parentOrganization**: Parent organization ID if applicable (null for top-level)
- **roles**: List of roles the organization plays in the system

### Actors

Each actor entry contains the following fields:

- **id**: Unique identifier following pattern `actor:XXX` (3 digits)
- **name**: The person's full name
- **description**: Brief description of their role and responsibilities
- **type**: Actor type (typically "Person", but could include "System", "Role")
- **contact**: Contact information (email)
- **organization**: The organization they belong to
- **roles**: List of specific roles they perform

## Current catalog content

**Organizations:**

- **organization:001** - Laboratorio de Sistemas Inteligentes de Movilidad (SIMOVI) (Research Lab)

**Actors:**

- **actor:001** - Fabián Abarca Calderón (Lead Architect at SIMOVI)

## Relevant questions

- Who are the key organizations involved in public transportation system development and operation?
- What are the specific roles and responsibilities of each organization?
- Who are the key individuals (actors) responsible for system implementation and operation?
- How do organizations relate to each other hierarchically?
- What contact information and organizational details need to be maintained?

## Expected expansion areas

**Government Organizations:**

- ARESEP (Autoridad Reguladora de los Servicios Públicos)
- CTP (Consejo de Transporte Público)
- MOPT (Ministerio de Obras Públicas y Transportes)
- Municipal transportation departments

**Private Organizations:**

- Bus operating companies
- Technology vendors and suppliers
- Payment processing companies
- Maintenance service providers

**Academic/Research Organizations:**

- Universities and research centers
- International research collaborations

**Key Actors:**

- System architects and developers
- Transportation planners
- Government officials
- Bus operators and fleet managers
- IT administrators and support staff

## Main references

- SITGAM
- Electronic payment commission (BCCR)
- Others (SIMOVI)

# Data Entity/Component Catalog

File: `architecture/catalogs/data-entity-component.yaml`

## Definition according to TOGAF

> This catalog identifies and maintains a list of the data used across the enterprise, relating data entities to data components showing how data entities are structured. Its purpose is to identify all data used in the enterprise and encourage effective data use. The Data Entity/Data Component catalog contains the following metamodel entities: Data Entity, Logical Data Component and Physical Data Component.

## Data structure

The catalog contains two main sections:

### Data Entities

Each data entity entry contains the following fields:

- **id**: Unique identifier following pattern `data-entity:XXX` (3 digits)
- **name**: The entity name (e.g., "User", "Bus", "Route")
- **description**: Brief description of what the entity represents
- **attributes**: List of attributes that define the entity structure
  - **id**: Unique identifier for the attribute (`attribute:XXX`)
  - **name**: Attribute name (e.g., "User ID", "License Plate")
  - **type**: Data type (String, Integer, Boolean, Date, etc.)
  - **description**: Description of what the attribute represents

### Data Components

Each data component entry contains the following fields:

- **id**: Unique identifier following pattern `data-component:XXX` (3 digits)
- **name**: The component name (e.g., "User Management", "Bus Management")
- **description**: Description of the component's purpose and functionality
- **data_entities**: List of data entity IDs that this component manages

## Current catalog content

**Data Entities:**

- **data-entity:001** - User (with attributes: User ID, Name, Email, Phone Number)
- **data-entity:002** - Bus (with attributes: Bus ID, License Plate, Capacity, Route ID)

**Data Components:**

- **data-component:001** - User Management (manages User entity)
- **data-component:002** - Bus Management (manages Bus entity)

## Relevant questions

- What are the core data entities needed for the public transportation information system?
- How do data entities relate to each other through their attributes?
- What data components are needed to manage and process these entities?
- What data standards or specifications should be used (GTFS, NeTEx, SIRI)?
- How do logical and physical data components differ in implementation?

## Expected expansion areas

**Transportation Data Entities:**

- Route, Stop, Schedule, Trip, Agency
- Real-time position, arrival predictions, service alerts
- Fare products, payment transactions
- Vehicle maintenance records, driver information

**System Data Entities:**

- Authentication tokens, user preferences, notifications
- System logs, performance metrics, error reports
- Configuration settings, operational parameters

**Data Components:**

- Route planning and optimization
- Real-time tracking and predictions
- Payment processing and fare management
- Reporting and analytics
- Integration with external systems (GTFS feeds, payment gateways)

## Main references

- Articles developed by SIMOVI (attached)

# Application Portfolio Catalog

File: `architecture/catalogs/application-portfolio.yaml`

## Definition according to TOGAF

> The purpose of this catalog is to identify and maintain a list of all the applications in the enterprise. This list helps to define the horizontal scope of change initiatives that may impact particular kinds of applications. An agreed Application Portfolio allows a standard set of applications to be defined and governed. The Application Portfolio catalog provides a foundation on which to base the remaining matrices and diagrams. It is typically the start point of the Application Architecture phase. The Application Portfolio catalog contains the following metamodel entities: Application Service, Logical Application Component and Physical Application Component.

## Data structure

Each application entry contains the following fields:

- **id**: Unique identifier following pattern `application:XXX` (3 digits)
- **name**: The application name (e.g., "Real-Time Bus Tracking System")
- **description**: Brief description of the application's purpose and functionality
- **version**: Current version of the application
- **vendor**: The company or organization that developed/maintains the application
- **license**: License type (Commercial, Open Source, Custom, etc.)
- **support_contact**: Contact information for technical support
- **categories**: List of functional categories the application belongs to
- **technologies**: List of key technologies used by the application
- **stakeholders**: List of stakeholder groups that use or are affected by the application
- **status**: Current status (Active, Inactive, Development, Planned, Retired)
- **deployment_environment**: Where the application is deployed (Cloud, On-Premise, Hybrid)
- **criticality**: Business criticality level (High, Medium, Low)

## Current catalog content

The catalog currently contains:

- **application:001** - Real-Time Bus Tracking System (v2.3.1, TransitTech Solutions, High criticality)

## Relevant questions

- What are the applications enabled by implementing a public transportation information system?
- What are the recommended implementation phases for different application types?
- What is the recommended implementation order for each application, by phases?
- How do applications integrate with each other and external systems?
- What are the licensing and vendor management considerations?
- How should application criticality and deployment environments be assessed?

## Expected expansion areas

**Core Transportation Applications:**

- Route planning and optimization systems
- Fleet management and dispatch
- Passenger information displays
- Mobile passenger applications
- Real-time arrival prediction systems

**Supporting Applications:**

- Payment processing and fare management
- Vehicle maintenance management
- Driver management and scheduling
- Customer service and feedback systems
- Reporting and analytics platforms

**Integration Applications:**

- GTFS feed generators and consumers
- API gateways and service mesh
- Data synchronization and ETL tools
- Third-party integration adapters
- Monitoring and alerting systems

**Administrative Applications:**

- Configuration management systems
- User and role management
- Audit and compliance tracking
- Performance monitoring dashboards
- Backup and disaster recovery tools

## Main references

- [ARC-IT](https://www.arc-it.net/) (_service packages_)
- Other references (to search)

# Interface Catalog

File: `architecture/catalogs/interface.yaml`

## Description according to TOGAF

> The purpose of the Interface catalog is to scope and document the interfaces between applications to enable the overall dependencies between applications to be scoped as early as possible. Applications will create, read, update, and delete data within other applications; this will be achieved by some kind of interface, whether via a batch file that is loaded periodically, a direct connection to another application's database, or via some form of API or web service. The mapping of the Application Component-Application Component entity relationship is an important step as it enables the following to take place: Understand the degree of interaction between applications, identifying those that are central in terms of their dependencies on other applications, Understand the number and types of interfaces between applications Understand the degree of duplication of interfaces between applications, Identify the potential for simplification of interfaces when considering the target Application Portfolio, Support the gap analysis and determine whether any of the applications are missing and as a result need to be created. The Interface catalog contains the following metamodel entities: Logical Application Component, Physical Application Component, Application communicates with application relationship.

## Data structure

Each interface entry contains the following fields:

- **id**: Unique identifier following pattern `interface:XXX` (3 digits)
- **name**: The interface name (e.g., "User Authentication Interface")
- **description**: Brief description of the interface's purpose and functionality
- **type**: Interface type (REST API, GraphQL, SOAP, Message Queue, Database, File Transfer, etc.)
- **protocols**: List of communication protocols used (HTTPS, HTTP, TCP, UDP, etc.)
- **dataFormats**: List of data formats supported (JSON, XML, CSV, Protobuf, etc.)
- **security**: List of security mechanisms implemented (OAuth 2.0, API Keys, JWT, TLS, etc.)
- **version**: Current version of the interface specification
- **owner**: Person or team responsible for the interface
- **contact**: Contact information for interface support
- **relatedComponents**: List of components or services that use this interface
- **status**: Current status (Active, Deprecated, Development, Planned, Retired)
- **documentation**: URL or reference to detailed interface documentation

## Current catalog content

The catalog currently contains:

- **interface:001** - User Authentication Interface (REST API, HTTPS/JSON, OAuth 2.0, Active)

## Relevant questions

- How do the different parts of the system communicate with each other?
- What interface types and protocols are used (REST, GraphQL, messaging, file transfer)?
- What data formats and security mechanisms are standardized across interfaces?
- How are interface dependencies mapped between applications and components?
- What documentation and versioning strategies are used for interface management?
- What physical communication layers are used (cellular network, Wi-Fi, Ethernet)?

## Expected expansion areas

**Authentication and Authorization Interfaces:**

- User login and logout APIs
- Token refresh and validation services
- Role-based access control interfaces
- Single sign-on (SSO) integration

**Transportation Data Interfaces:**

- GTFS feed generation and consumption APIs
- Real-time vehicle position updates
- Route and schedule management interfaces
- Stop and arrival prediction APIs

**Payment and Fare Interfaces:**

- Payment processing gateways
- Fare calculation and validation APIs
- Electronic ticketing interfaces
- Financial reconciliation services

**External System Interfaces:**

- Third-party mapping and routing services
- Weather and traffic data feeds
- Government reporting and compliance APIs
- Maintenance management system integration

**Internal System Interfaces:**

- Microservice communication APIs
- Database access interfaces
- Message queue and event streaming
- Configuration and monitoring interfaces

## Main references

- [ARC-IT](https://www.arc-it.net/index.html) (_functional view_, _physical view_, _communications view_)
- Article on SIMOVI system-level design (attached)

# Technology Standards Catalog

File: `architecture/catalogs/technology-standards.yaml`

## Definition according to TOGAF

> The Technology Standards catalog documents the agreed standards for technology across the enterprise covering technologies, and versions, the technology lifecycles, and the refresh cycles for the technology. Depending upon the organization, this may also include location or business domain-specific standards information. This catalog provides a snapshot of the enterprise standard technologies that are or can be deployed, and also helps identify the discrepancies across the enterprise. The Technology Standards catalog contains the following metamodel entities: Technology Service, Logical Technology Component, Physical Technology Component. If technology standards are currently in place, apply these to the Technology Portfolio catalog to gain a baseline view of compliance with technology standards.

## Data structure

Each technology standard entry contains the following fields:

- **id**: Unique identifier following pattern `tech-standard:XXX` (3 digits)
- **name**: The standard name (e.g., "OpenAPI Specification", "OAuth 2.0")
- **description**: Brief description of what the standard defines and its purpose
- **version**: Current version of the standard being adopted
- **organization**: The organization or body that maintains the standard
- **website**: Official website URL for the standard
- **usage**: Description of how the standard is used within the system
- **relatedTechnologies**: List of technologies, tools, or frameworks that implement or support this standard
- **status**: Current adoption status (Active, Planned, Deprecated, Under Review)
- **documentation**: URL or reference to official standard documentation

## Current catalog content

The catalog currently contains:

- **tech-standard:001** - OpenAPI Specification (v3.0.3, OpenAPI Initiative, Active)
- **tech-standard:002** - OAuth 2.0 (RFC 6749, IETF, Active)

## Relevant questions

- What technology standards are appropriate for managing intelligent public transportation systems?
- Which standards should be adopted for API design, security, data exchange, and system integration?
- How do current technology implementations align with established standards?
- What are the version management and lifecycle policies for adopted standards?
- How do standards relate to each other and to the technologies that implement them?
- What new cloud computing and transportation-specific standards should be considered?

## Expected expansion areas

**API and Integration Standards:**

- REST API design standards (OpenAPI, JSON:API)
- GraphQL specifications
- Message queue protocols (AMQP, MQTT)
- Service mesh and microservices standards

**Security Standards:**

- Authentication and authorization (OAuth 2.0, OpenID Connect, SAML)
- API security (JWT, API keys, rate limiting)
- Data encryption (TLS, AES)
- Security frameworks (OWASP guidelines)

**Data Exchange Standards:**

- Transportation data formats (GTFS, GTFS-Realtime, NeTEx, SIRI)
- Geographic data standards (GeoJSON, KML)
- Payment standards (EMV, PCI DSS)
- Data serialization (JSON, XML, Protocol Buffers)

**Cloud and Infrastructure Standards:**

- Container orchestration (Kubernetes)
- Cloud-native standards (CNCF projects)
- Infrastructure as Code (Terraform, CloudFormation)
- Monitoring and observability (OpenTelemetry, Prometheus)

**Transportation-Specific Standards:**

- Vehicle communication protocols (CAN bus, J1939)
- Location services (GPS, GLONASS standards)
- Real-time communication (WebSocket, Server-Sent Events)
- Fleet management standards

## Main references

- GIS (geographic information systems) tender from CTP (attached)
- [ARC-IT](https://www.arc-it.net/index.html)
- Technology vendors
- SIMOVI system design article (attached)
- SIMOVI technologies (_[tech stack](https://github.com/simovilab/context/blob/main/tech_stack.md)_)

# Technology Portfolio Catalog

File: `architecture/catalogs/technology-portfolio.yaml`

## Definition according to TOGAF

> The Technology Portfolio catalog provides a comprehensive listing of the Technology Infrastructure that is deployed throughout the enterprise, including the software and hardware that comprises the Technology Platform. The Technology Portfolio catalog provides a foundation for determining current usage, costs, and standards compliance for technology, and for making decisions during the Technology Architecture phase. The Technology Portfolio catalog contains the following metamodel entities: Technology Service, Logical Technology Component and Physical Technology Component.

## Data structure

Each technology entry in the portfolio contains the following fields:

- **id**: Unique identifier following pattern `technology:XXX` (3 digits)
- **name**: The technology name (e.g., "PostgreSQL", "Node.js", "Vue.js")
- **description**: Brief description of what the technology is and its primary purpose
- **version**: Current version being used or recommended
- **organization**: The organization or entity that develops/maintains the technology
- **website**: Official website URL for the technology
- **usage**: Description of how the technology is used within the system
- **relatedTechnologies**: List of complementary or related technologies that work with this one
- **status**: Current deployment/adoption status (Active, Planned, Deprecated, Under Evaluation)
- **documentation**: URL or reference to official documentation

## Current catalog content

The catalog currently contains core technologies for the public transportation information system:

- **technology:001** - PostgreSQL (v13, Database Management)
- **technology:002** - Node.js (v14.x, Server-side Runtime)
- **technology:003** - Vue.js (v3.x, Frontend Framework)

## Relevant questions

- What technologies comprise the complete technology stack for the public transportation information system?
- How do different technologies integrate and work together within the architecture?
- What are the version management and upgrade strategies for each technology?
- Which technologies are core dependencies vs. optional/complementary tools?
- How do technology choices align with organizational standards and capabilities?
- What licensing, support, and maintenance considerations exist for each technology?

## Expected expansion areas

**Backend Technologies:**

- Application servers and runtime environments
- Database technologies (relational, NoSQL, time-series)
- Message queues and event streaming platforms
- Caching and session management solutions

**Frontend Technologies:**

- Mobile development frameworks (React Native, Flutter)
- Progressive Web App (PWA) technologies
- UI component libraries and design systems
- Build tools and development environments

**Infrastructure Technologies:**

- Container platforms (Docker, Kubernetes)
- Cloud services and serverless computing
- Load balancers and reverse proxies
- Monitoring and logging solutions

**Integration Technologies:**

- API gateways and service mesh
- ETL and data processing tools
- Protocol adapters and connectors
- Testing and quality assurance tools

**DevOps and Operations:**

- CI/CD pipeline tools
- Infrastructure as Code solutions
- Security scanning and compliance tools
- Backup and disaster recovery systems

## Main references

- SIMOVI tech stack documentation
- Technology vendor evaluations
- Open source technology assessments
- Industry best practices for transportation systems

# Requirements Catalog

File: `architecture/catalogs/requirements.yaml`

## Definition according to TOGAF

> The Requirements catalog captures things that the enterprise needs to do to meet its objectives. Requirements generated from architecture engagements are typically implemented through change initiatives identified and scoped during Phase E (Opportunities & Solutions). Requirements can also be used as a quality assurance tool to ensure that a particular architecture is fit-for-purpose (i.e., the architecture can meet all identified requirements). The Requirements catalog contains the following metamodel entities: Requirement, Assumption, Constraint, Gap

## Data structure

Each requirement entry contains the following fields:

- **id**: Unique identifier following pattern `requirement:XXX` (3 digits)
- **name**: The requirement name (e.g., "Real-Time Bus Tracking", "User Authentication")
- **description**: Clear statement of what the system shall do or provide
- **type**: Requirement type (Functional, Non-Functional, Business, Technical, etc.)
- **priority**: Priority level (High, Medium, Low, Critical)
- **status**: Current status (Approved, Pending, Rejected, In Review, Implemented)
- **rationale**: Explanation of why this requirement is important and beneficial
- **stakeholders**: List of stakeholder groups affected by or interested in this requirement
- **acceptanceCriteria**: List of specific, measurable criteria that define when the requirement is satisfied
- **relatedComponents**: List of system components that implement or are affected by this requirement
- **relatedInterfaces**: List of interfaces that support or enable this requirement
- **relatedDataEntities**: List of data entities involved in fulfilling this requirement
- **relatedActors**: List of actors (users, systems) that interact with this requirement

## Current catalog content

The catalog currently contains foundational requirements for the public transportation information system:

- **requirement:001** - Real-Time Bus Tracking (High priority, Functional requirement)
- **requirement:002** - User Authentication (Medium priority, Functional requirement)

## Relevant questions

- What functional capabilities must the system provide to meet user and business needs?
- What non-functional requirements (performance, security, usability) are critical for system success?
- How do requirements relate to stakeholder needs and business objectives?
- What are the acceptance criteria that define successful requirement implementation?
- How do requirements trace to system components, interfaces, and data entities?
- What assumptions and constraints affect requirement implementation?

## Expected expansion areas

**Functional Requirements:**

- Real-time vehicle tracking and positioning
- Route planning and trip management
- Payment processing and fare collection
- User registration and profile management
- Notification and alert systems
- Reporting and analytics capabilities

**Non-Functional Requirements:**

- **Performance**: Response times, throughput, scalability requirements
- **Security**: Authentication, authorization, data protection, privacy
- **Reliability**: Availability, fault tolerance, disaster recovery
- **Usability**: User experience, accessibility, internationalization
- **Interoperability**: Integration with external systems, standards compliance

**Business Requirements:**

- Compliance with transportation regulations
- Integration with existing payment systems
- Support for multiple transportation modes
- Real-time data sharing with authorities
- Passenger information accessibility

**Technical Requirements:**

- Mobile application compatibility
- Web browser support requirements
- Database performance and capacity
- API design and documentation standards
- Monitoring and logging capabilities

**Constraints and Assumptions:**

- Budget and resource limitations
- Technology platform restrictions
- Regulatory and legal requirements
- Timeline and delivery constraints
- Third-party system dependencies

## Requirements traceability

The catalog establishes traceability links between requirements and other architectural elements:

- **Components**: Maps requirements to implementing system components
- **Interfaces**: Links requirements to supporting system interfaces
- **Data Entities**: Connects requirements to relevant data structures
- **Actors**: Associates requirements with interacting users and systems
- **Stakeholders**: Traces requirements to originating stakeholder needs

## Main references

- SIMOVI articles (requirements engineering research)
- [SIMI requirements gathering methodology](https://simovilab.github.io/sistema-informacion/diseno/requisitos)
- [ARC-IT](https://www.arc-it.net/index.html) (transportation system requirements patterns)
- [GTFS specification](https://gtfs.org/) (data format requirements)
- IEEE 830 Standard for Software Requirements Specifications
- TOGAF Requirements Management techniques

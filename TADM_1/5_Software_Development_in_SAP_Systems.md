# Software Development in SAP Systems

## Data Structure of an AS ABAP Based SAP System

- A client in a SAP System is characterized by the fact that is has its own business data environment, own master data, transaction data and user data = CLIENT DEPENDENT DATA

- Repository = totality of all the objects you can access using the ABAP Workbench | It is cross - client

&emsp;&emsp; - A repository contains all dictionary objects (tables, data elements, domains, etc.)

- Any repository object developed or changed in any one client are used in exactly the same form in every client in that SAP System

- Package = Many repository objects

## Software Logistics for AS ABAP based SAP System

- Reasons for setting up a multisystem landscape:

1. Continous Maintenance for all SAP Systems

2. Audits required detailed logging of transport requests

3. ABAP Repository Objects works across across clients

**Example of Three Sytem Landscape**

1. Development

&emsp;&emsp; - DEV code

&emsp;&emsp; - Creates the changes

2. Quality Assurance

&emsp;&emsp; - QAS

&emsp;&emsp; - Focus on Functional Acceptance

3. Production

&emsp;&emsp; - PRD

&emsp;&emsp; - Focus on Productive Operation

### Transports in the ABAP Environmnet

- Trasnport requests are used to transfer changes for repository objects / newly created objects and / or customer-defined customizing

- Transport Organizer -> Transaction SE09

- Roles in developing and transporting:

1. Development Project Team Leader -> manages transport requests

2. Developer -> develops repository objects and performs customizing

3. Tester: tests newly developed or changed functions

4. Trasnport Administrator: responsible for software logistics

- Transport Organizer: the tool to manage these transport requests

- **Structure of a Transport Request:**

1. A trasnport is created based on Tasks

2. A Task is created based on Repositories / Customer Objects

3. A Task is assigned to one developer

- An object can be modified only by the assigned developer => an object lock is created

- The Transport Organizer creates versions of the repository objects

#### Actions upon Development Completion: Export and Import

- When the work in a task is ready => Release the task

- When all the tasks are ready the development project leader can release the transport request

- **EXPORT:** Once a transportable request is released, the customizing objects and repository objects are copied from source database to a central trasnport directory

- **IMPORT:** in target is NOT automatic (in generla). It is triggered by the trasnport administrator in the Transport Management System (TMS)

- In general, de DEV exports the changes into the Central Transport Directory at file system level and the QAS and PRD import the changes

### Accessing and Editing ABAP Repository Objects

- **Software Development Cycle:**

1. Analysis / Desing

&emsp;&emsp; - Modelling

2. Implementation

&emsp;&emsp; - Object Navigator, ABAP Dictionary, Screen Painter, Menu Painter, ABAP Editor, Function Builder

3. Test

&emsp;&emsp; -Debugger, Extended Computer Aided Test Tool

4. Administration

&emsp;&emsp; - Performance Tools, PM, Transport Organizer

- **ABAP Workbench:** Programming Environment for developing enterprise - wide business solutions

#### ABAP Development Tools (ADT) for Eclipse

- Older Eclipse Dev Tools: Sap NetWeaver Visual Composer, SAP NetWeaver Developer Studio for Java Development, Sybsae Unwired Platform and SAP Hana Studio

- Features of ABAP Development Tools:

1. New ABAP Development experience on Eclipse Platform

2. Open platform for developing new ABAP-based tools

3. Open-language and platform-independent APIs to build new user-defined tools for ABAP environment

4. Support for creation of Core Data Services (CDS) entities in ABAP development

- **Classic ABAP Project:** Represents the connection to an on-prem system

- **Cloud ABAP Project:** Represents the connection to SAP BTP ABAP environment

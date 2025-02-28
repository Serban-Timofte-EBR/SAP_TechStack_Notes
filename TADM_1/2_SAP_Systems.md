# SAP Systems

## SAP Business Suite vs SAP S/4 HANA

- In SAP Business Suite we have specialized apps for each task like SAP CRM, ERP, SCM, PLM

- In SPA S/4 HANA all these systems are reprezented as tables into a big cloud database

- Old SAP world: SAP ERP, SAP CRM, SAP SRM, SPA PLM

- New SAP world: SAP S/4HANA and SAP BW/4HANA

## Applications

### SAP S/4 HANA

- Lastest collection of business applications from SAP

- Offers multiple applications from SAP already optimezed for user on SAP HANA

- Uses SAP Fiori for UI

### SAP BW /4 HANA

- Evolution of SAP Business Warehouse optimez for SAP HANA

## How are the data stored?

- In SAP ECC there are integrated these DB versions: SAP ASE, SAP MaxDB, Oracle DB, IBM DB2, MS SQL Server

- SAP ECC is designed for row-based data and needs to aggregate tables

- SAP ECC does not use DB procedures

- In **SAP S/4 HANA** there are column-based data (much faster reading of specific values) and does not aggregate tables

- In SAP S/4 HANA the tables are not normalized to be able to have access to all the data

- Most traditional enterprise relational database tables are based on row storage. However, SAP HANA fully supports OLTP (online transactional processing)

- SAP HANA supports both row tables and column tables in the same database

- Column tables are efficient for analytical applications where requests for data selection are not predictable

- The downside of column tables is the cost of reconstructing complete records from the separately stored columns

## SAP Systems and Application Server ABAP and Application Server Java

Application:             SAP S/4HANA Server          SAP Enterprise Portal

Basic Functionality:        AS ABAP                         AS Java

- Both application systems offers: multi-level arhitecture, reliable, tried and tested runtimes env, high scalability

- The systems have three layers: Presentation layer (SPA GUI, SAP Business Client, Browser), Application layer (support different OSs), Database level

### SAP NetWeaver AS for ABAP

- Complete infrastructure in which ABAP-based applications can be developed and used

### SAP NetWeaver AS Java

- Complete infrastructure in which JEE-compliant applications can be developed and used

## ABAP and Java

- SAP NetWeaver provides two different runtime environments for this (ABAP runtime and JAVA runtime env)

## ABAP Workbench

- Used for developing completely new applications as well as enhancing and modifying SPA standard applications

## Client - Server Based Architecture

1. Hardware Oriented View:

&emsp;&emsp; - Server means the central server in a network that provides data, memory and resources for the workstations (clients)

&emsp;&emsp; - Ex: The client communicates with the server via LAN/WAN

2. Software Oriented View:

&emsp;&emsp; - Client and server are both defined at the process level (service). It is provided by a software component

&emsp;&emsp; - A software component can consist of a process or a group of processes.

&emsp;&emsp; - The client communicate with the server via require / providing a process

- In SAP systems, the terms are used as in software - oriented view

## Client - Server Configuration for SAP Systems

- The following processes are often used for operating business application software: Presentation, Application, Database

- Configuration are either single - tier or multi - tier depending of the number of hardware layers

1. Single - tier configurations

&emsp;&emsp; - All processing tasks are performed by one computer.

&emsp;&emsp; - This is a classic mainframe processing

2. Two - tier configuarions

&emsp;&emsp; - Implemented using special presentation computers that are responsible solely for formatting the GUI

&emsp;&emsp; - A classic separation between server and the client as separated apps

3. Three - tier (Multi - tier) configuration

&emsp;&emsp; - Each layer runs on its own host

&emsp;&emsp; - Many different application servers can simultaneosly work with the data of the database server

- In SAP systems there are NOT implemented two-tier configurations (the ones with a powerful desktop systems and to use these for presentation and applications)

- In SAP S/4HANA and SAP Business Suite environment more complex client/server configurations consisting of more than three tiers are possible and used

### ABAP Workbench Functionalities and Tools

1. ABA Editor -> write ABAP programs

2. ABAP Dictionary -> Define and describe tables, data elements, lock objects, etc

3. Screen Painter -> create UI

4. Function Builder -> create and manage function modules

- **Flow:** Development Environment (ABAP tools, Data Modeler, Screen Painter) ---> ABAP Dictionary ---> Runtime environment of the application (ABAP Interpreter, Dialog - control, Interfaces, DnproInterpreter)

- Table definition is database - independent

#### Excursus: Core Data Services Views (CDS Views)

- ABAP Dictionary allows the creation of views = grouping of columns from one or more database tables

- When joining tables, a view usually implements a join with statically 
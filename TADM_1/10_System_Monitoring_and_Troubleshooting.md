# System Monitoring and Troubleshooting

## Technical Basics: Data Supplier

- CCMS monitorign arhitecture = Local monitoring arhitecture

- There are 2 types of data supliers:

1. Passive Data Suppliers

&emsp;&emsp; - Started by monitoring arhitecture

&emsp;&emsp; - Passive = the behavior of the data supplier in relation to the monitoring arhitecture (It does not start itself, but must be started by the monitoring arhitecture)

&emsp;&emsp; - Also known as data collection methods

2. Active Data Suppliers

&emsp;&emsp; - Started by monitored applications

- The data suppliers write the info in a shared memory = **monitoring segment**

- There are three layers of monitoring

```txt
Data                    Analysis Methods                SAP Monitors            3rd-Party Product   
Analysis              (Auto Reaction Method)           (local/central)               (API)
                                |                            |                         |
                                |                            |                         |
Data              ---------- Monitoring Segment (each instance has a monitoring segment) ----------
Storage           Monitoring Object   Monitoring Object   Monitoring Object   Monitoring Object   
                        |                      |                  |                    |
Data              Data Collector        Data Collector      Data Collector      Data Collector
Collection             (DB)                   (OS)           (Dispatcher)       (Other/Non-SAP)
```

### Data Collection Level

- Small subareas of an SAP System are monitored by special programs called data collectors

- Each data collector checks its sub-component at regular intervals and stores the collected monitoring data in the local monitoring segment

- **Important:** The monitoring segment is the area of main memory that contains the monitoring data from the data collectors => **perform data storage**

- If the system identify a problem, it can execute a specifically prepared **Auto-reaction Method**

- Predefined **Analysis Method** are used to clarify problem situations

- Tools to display data from the monitoring segments:

1. SAP MC (SAP Management Console) & SAP MMC (SAP Microsoft Management) display functions

2. SAP command line programs like *dpmon* and *msmon*

3. SAP ABAP based SAP System the Aler Monitor to display and analyze alerts

4. SAP Application Lifecycle Management (SAP Solution Manager, SAP Focused RUN, SAP Cloud ALM) for metrics

5. Third-party vendors and partners

### Monitoring with SAP Management Console (SAP MC)

- SAP MC provides alert monitoring information based on predefined thresholds

- SAP MC offers info about the state of the system and severe alers that exist

- Monitoring area is divided in two parts: Open Alerts and Current Status

### Additional Monitoring Options

- **Thread List:** Information about the created worker threads

- **Connection List:** Information about the existing connections

- **Cache List:** Information about all objects currently in the ICM Server Cache (sub-node from the ICM tree structure)

- **Proxy List:** Information about the proxy server list

- Additional Monitoring information: Enqueue Server / Messsage Server

### Operating the Alert Monitor

- Alerts from a central element of monitoring are displayed in the Alert Monitor

- This reduces the workload for the system administration (now see only the error messages, not all system data)

- The CCMS Monitor has this structure:

1. Monitor Set

&emsp;&emsp; - Is a collection of different monitors

&emsp;&emsp; - Monitor sets usually represent a product that needs to be monitored

2. Monitor Definitions

&emsp;&emsp; - Describes the selection of monitor objects and monitoring attributes that you want to examine in more detail

3. Monitoring Segment (many Monitoring Objects)

4. (Not part of CCMS) Monitor

&emsp;&emsp; - Display of monitoring objects and monitoring attributes that are included for display in the monitor definition

- The monitoring data for an attribute can be displayed in several monitors

### Monitor Structure

- The Monitor Strucutre is a tree structure of a monitor

- A node in this tree is called a monitor tree element (MTE)

- The collected information by the data collectors are displayed at the lowest level in the leaves of the tree. Leaves = monitoring attributes

- Monitoring attributes are grouped at the second-lowest level using monitoring objects

- A monitor can obtains data from multiple SAP Systems

### SAP Command Line Programs

- The user <sid>adm on OS level or folder /usr/sap/SYS/exe/run of program mon can offer monitoring tools

- Important tools:

1. dpmon

&emsp;&emsp; - Used to get the process overview of an instance in text mode (Dispatcher Monitor)

2. icmon

&emsp;&emsp; - Used to monitor and manage the ICM (Internet Communication Manager)

3. wdispmon

&emsp;&emsp; - SAP Web Dispatcher Monitor program

4. gwmon

&emsp;&emsp; - Monitors the SAP Gateway

5. msmon / msprot

&emsp;&emsp; - Message Server Monitor Utility

6. lgtst

&emsp;&emsp; - Testprogram for SAP Login Info

7. msprot

&emsp;&emsp; - Message Server Test Progrma

8. esmon / es2mon

&emsp;&emsp; - Monitor the enqueue server and the enqueue replication servers

- To start a program ```<sapprogram> pf=<profile>```

- **dpmon** is an instance-specific tool and offers a Monitor-Menu which allows to get details for the assigned work processes

#### Usage examples

- In general, there is not recommanded to use the SPA Command Line Programs, expect when the classic tools are not available

1. If you are using a standalone gateway

2. Test the designed logon groups works correct using lgtst

3. Generate a client load to check if hte configuration is able to handle the amount of requests it is configured for .icmon or wdispmon

4. Forgot the passsword for admon user

5. Manage enqueue replication server at OS level (esmon or es2mon)

## Tracing and Logging in the SAP System

### Important terms

- **Trace:** In SAP context, a trace ussually refers to an option for logging system processes that users can activate and deactivate

- **Log:** Continuosly recorded information flow that records certain events

### Dump Analysis (ST22)

- ABAP programs are checked statically when they are created and dynamically when they are running

- Runtime errors are identified dynamically by the ABAP runtime environment

- When a runtime errror occurs (runtime error identified and cannot be handled), the ABAP runtime environment terminates the execution of the program and generates a short dump

- Error situations:

1. Internal Error

&emsp;&emsp; - Kernel identifies an error state

2. Installation and evnironment/resource error

&emsp;&emsp; - Incorrect System installation or missing resourceses (Ex: database is shut down)

3. Error in application program

## Troubleshooting Procedures

1. Isolate the problem area

2. Problem analysis: Check the scenatio to find out whether all required settings are correct and analyze the logs

3. Gain additional knowledge

4. Compare error-free and erroneous processes

- *Guided Answers* is dedicated to support customers and partners => output of a search is Guided Answer Tree

## Using Local Monitoring functions for AS Java (SAP MC and NWA)

- SAP NetWeaver AS Java provides an infrastructure that makes monitoring data available (available in SAP NetWeaver Administrator)

### Monitoring Infrastructure

```txt
                               | -------------------- |           AS JAVA
Applications ----------------- |    Monitoring        |                      ICM
                               |           Segment    |                       |
Kernel ----------------------- |                      |                       |
                               |                      |      (collect)        |
Services --------------------- |                      | <---------------- SP (JMX)
                               |                      |
Performance ------------------ |                      |
                               | -------------------- |
                                           |
                                           | (create)
                                           |
                                        sapstartsrv
```

- The data of JMX monitors is stored in the monitoring segment. The external tools connect through the JMX API and can display all current values in the JMX Monitors

1. Applications

&emsp;&emsp; - Contains information about the satus that are running on AS Java and for which monitoring functions are implemented in the coding

&emsp;&emsp; - Configurable type of monitor

2. Kernel

&emsp;&emsp; - Status information for the managers registered for monitoring is displayed under the Kernel Entry

&emsp;&emsp; - Reserved for data that is directly and automatically collected by the system

3. Services

&emsp;&emsp; - Status information for the services registred for monitoring is displayed under the Service entry

&emsp;&emsp; - Reserved for data that is directly and automatically collected by the system

4. Performance

&emsp;&emsp; - Performance area displays available data about performance measurements of AS Java (e.g. communication to external services)

## Explaining the Concept of Monitoring Tools in SAP Solution Manager

- MAI = Monitoring and Alerting Infrastructure (for Centralized Monitoring)

- MAI is introduced in SAP Solution Manager

- Components for SAP Solution Manager:

1. CA Introscope Adapter (IS Adapter)

&emsp;&emsp; - Collect performance data and metrics from various components

2. CA APM Introscope Enterprise Manager (EM)

&emsp;&emsp; - Serves as central Storage System where all data callected by IS Agents (see nr. 1) is stored centrally

3. SAP Solution Manager Diagnostics Agent

&emsp;&emsp; - Creates connection between SAP Solution Manager and managed system

&emsp;&emsp; - Collect information from the remote system

4. SAP Host Agent

&emsp;&emsp; - Monitors the interaction between the host sustem and OS

5. Extractor Framework

&emsp;&emsp; - Processes the information from the connected ABAP systems and from teh CAP APM Introscope Enterprise Manager

6. ST-PI and ST-A/PI

&emsp;&emsp; - An interface for the collection and transmission of dat and performance metrics of ABAP components

### System and Application Monitoring Use Cases

1. System Monitoring

&emsp;&emsp; - System Monitoring application provides an overview of the current status of technical systems, including their associated instances, databases and hosts

&emsp;&emsp; - Based on automated checks in regular time intervals in the Availability, Performance, Exceptions and Configurations

2. User Experience Monitoring

&emsp;&emsp; - UXMon (formerly EEM) is a toolbox for evaluating and reporting the availability and performance of your productive systems from a client-side perspective

3. Interface Monitoring

&emsp;&emsp; - Monitor various interface technologies within the landscape

4. Process Integration Monitoring

&emsp;&emsp; - Unified alert notifications, exceptions and status of PI componets form single-entry point

5. Business Intelligence Monitoring

&emsp;&emsp; - Includes status overview for all technical components involved in SAP Business Intelligence Solution

## Important Information

- Transaction RZ20: Monitor the database and SAP System

- Active trace for SQL Statements in the SAP System: Performance Analysis, System trace

- Using Monitor Browser in NWA: Changes to threshold values, Display monitoring data for Java instances

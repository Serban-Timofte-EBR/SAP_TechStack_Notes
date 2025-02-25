# SAP System Kernel

## Basic Arhitecture of AS ABAP and AS Java

- **SAP Instance / SAP Application Server** is an administrative unit that combines SAP system components providing one or more services

- The services provided by an application server are started or stopped together

- Each application server has it own buffer areas in RAM and run on a host

- Multiple application servers can run on a single host

- When installing a SAP system there is the option of separating the processes at application level from processes at database level

- The database for an SAP system can be installed and operated on a separate host, separated from the AS of the SAP System

- **Important:** Usually, there is exactly one database for each SAP System

- Factors that have an influence on the application server desgin of an SAP SysteM:

1. Release of the SAP system (due to arhitecture changes throughout the releases)

2. Type of SAP System (AS ABAP or AS Java)

3. Decision of the SAP customer (scalability, high availability)

## SAP System Processes

- SAP runtime system consists of a large number of parallel processes that work together

- Here we can distinguish between the runtime environment for ABAP (AS ABAP) and Java (AS Java)

### AS ABAP Arhitecture and Processes

```txt
ABAP Message Server ------- Enqueue Server                                          SAP Web Dispatcher
                                   | 
                                RFC Gateway ------ Internet Communication Manager
                                -----------------------------------------------------------------------
                                |                             ABAP Dispatcher                         |
                                -----------------------------------------------------------------------
                                    |               |               |                       |
                                  Dialog        Background        Update                  Spool
```

- In AS ABAP the processes on every application server include the ABAP dispatcher and a number of work processes

**The information flow**

1. **ABAP Dispatcher** distributes the requests to the work processes

2. **Dialog work process** fulfill all requests for the execution of dialog steps triggered by an active user

&emsp;&emsp; - Dialog work process = is the request that goes from the FE to the dispatcher and on the return. Practically it is the process that communicates with the user / GUI / FE

3. **Background work process** execute programs that run without interacting with the user.

&emsp;&emsp; - You need at least two background work processes for each SAP System.

&emsp;&emsp; - It is invisible for the user

4. **Update work process** execute the update requests.

&emsp;&emsp; - You need at least one update work process per SAP System

5. **Spool work process** pass sequential data flows on to output devices (printers)

&emsp;&emsp; - At least one spool process is required per SAP System

- In older SAP System we can configure enqueue work processes. The administrator can lock tables in the host's working memory. 

- Lock tables contains the logical database lock of the ABAP runtime environment.

### Additional services in AS ABAP runtime system provides

- These are NOT work processes

1. ABAP Message Server (MS)

&emsp;&emsp; - Handles communication between the distributed dispatches withtin the AS ABAP

&emsp;&emsp; - Enables scalability of several parallel application servers

&emsp;&emsp; - Provides the AS ABAP with a central message service for internal communication. The message server also provides information on which application servers of the system are currently available

&emsp;&emsp; - At login on AS ABAP (using SAP GUI for Windows, SAP GUI for JAVA) using logon groups, the MS performs a load distribution of users to the available instances => **Logon Load Balancing** => After, the SAP GUI communicates directly with the dispatcher

2. Enqueue Server (ES)

&emsp;&emsp; - Manages the lock table with the logical database locks

3. RFC Gateway (GW)

&emsp;&emsp; - Enables communication between SAP Systems or between SAP Systems and external application systems

&emsp;&emsp; - Communication via RFC (Remote Function Controll) with other SPA systems

4. Internet Communication Manager (ICM)

&emsp;&emsp; - Enables the communication with the SAP system using web protocols such as HTTP(S) and SMTP

&emsp;&emsp; - Receives requests from the client and forwards them to the SAP systme fro processing

&emsp;&emsp; - When communicating via Web protocol, ICM receives the requests. It forwards the requests to the dispatcher of its application server

- ABAP dispatchers of the individual application servers communicate via message server which is installed exactly once per SAP System

- Transaction *SM04* -> overview of users who are logged on the same application OR System -> Status ...

#### Communication from End Users

- Web Browser -> ICM via HTTP(S)

- SAP Business Client -> ICM via HTTP(S) **OR** ABAP Dispatcher via DIAG

- SAP GUI for Windows / Java -> ABAP Dispatcher via DIAG

### Primary Application Server

- PAS = Primary Application Server

- Is the application server that was first installed for the SAP systems

- If an AS ABAP based SAP System does not have a central service instance, PAS will include the enqueue work process and the message server

- Cannot log on the Cnetral Service Instance as a dialog user. It is not called Application Server

- Central Service Instance is located at file system level */usr/sap/<SID>/ASCS<instance_number>*

- All other application servers of an SAP System are called Additional Application Servers (AAS)

## AS Java Arhitecture and Processes

```txt
Message Server (MS) ----- Enqueue Server ----- RFC Gateway

                                --------------------------------------
                                |                 ICM                |
                                --------------------------------------
                                    |                             |
                                    |                             |
                              Server Process                Server Process
                                    SP                            SP
```

1. **Internet Communication Manager (ICM)** distribuites incoming requests to the server processes

&emsp;&emsp; - Before AS Java 7.10, the Java Dispatcher performed this task

2. **Server Process** executes the Java Applications

&emsp;&emsp; - Every server process is multi-threaded, which means it can process queries in parallel

&emsp;&emsp; - It is based on the memory sizing how many server processes one ICM can have

3. **Java message service** manages a list of server processes

4. **Java enqueue service** manages logical locks that are set by executed Java application program in a server process

5. **RFC Gateway** enables communication between SAP systems or between them and externa application systems

## Describing AS ABAP

- The users can log on to the SAP System using SPA GUI or Web Clients, for example

- Users can log on through the ABAP MS (load balancing) or directly on the ABAP Dispatcher

- Processing of a user request in AS ABAP involves different processes on all three layers: presentation, application and database

### Information Flow in AS ABAP

- The screen entries of a user are accepted by a Front-End software and converted to an internal format and forwarded to the dispatcher

- **ABAP Dispatcher** is a central process of AS ABAP. It manages the resources for the applications written in ABAP in coordination with the respective OS. **MAIN TASK:** Distributing of the requests to its work processes, integration of the presentation layer and the organization of the communication activities

&emsp;&emsp; - ABAP Dispatcher distributes the requests one after the other to the available work processes

&emsp;&emsp; - Data is actually processed in the work process

&emsp;&emsp; - Once the work process is completed, the result is sent via dispatcher back to the SAP GUI. SPA GUI interprets the data and generates the output screen for the user

### Work Processes

- Execute the process logic of the application programs

- A work process has a task handler that coordinates the actions within a work process, software processors and database interface.

- **Dynpro processor** executes the screen flow logic of the application program, calls proessing logic of ABAP application and trasnsfers field content to the processing logic

- The actual processing logic of ABAP application is executed by the **ABAP Interpreter**

```txt
|---------------|----------------------------|---------------|
|               |           Dynpro           |               |
|               |          Processor         |               |
|               |----------------------------|               |
|   Internal    |           ABAP             |      Task     |
|   Memory      |         Interpreter        |     Handler   |
|               |----------------------------|               |
|               |         Database           |               |
|               |         Interface          |               |
|---------------|----------------------------|---------------|
```

- The dialog work process selected by the dispatcher performs a roll-in of the user context first.

### Database Interface of AS ABAP

- RDBMS = Relational Database Manager System

- Is generally used to manage large sets of data

- RDBMS save data in the form of two-dimensional tables

- ABAP SQL is used ot access the application data in the database

#### ABAP SQL

- When interpreting the ABAP SQL stataments, SAP DB interface checks for syntax of statement and checks for optimal utilization of the local SAP buffers in the shared memory

- The most frequently used information is stored in these buffers

```txt
|-------------------------------|
|          ABAP Dispatcher      |
|-------------------------------|
                        |
                        |
            |-------------------------------------------------------------------------|
            |                                                                         |
            |    ABAP Interpreter                                    |----------|     |
            |       SELECT *            -----------> (ABAP SQL)      |   DB     |     |
            |       FROM ...            <-----------   (Data)        | Inteface |     |
            |                                                        |----------|     |
            |        ADBC                                                             |
            |-------------------------------------------------------------------------|
                        |
                        |
                    Database 
                      Layer
```

- In ABAP is possbile to send native SQL commands directly into the database

- ADBC = ABAP Database Connectivity Framework is available for this action describe upper

- The SQL native commands are not checked for syntax correctnerss

- Using native SQL => the database independence of the used programs is no longer guaranteed

### Dialog Request Processing

- Execution of dialog requests is characterized by the following:

1. A program dialog step is assign to one specific dialog work process during execution

2. The individual dialog steps for a program consisting of several screens can be executed by different dialog wrok processes during program runtime.

3. A dialog work process sequentially processes dialog steps for various users and programs

- The user interactions are technically realized using screens (**dynpros**)

- The Dynpro processor of the work process executes the screen flow logic of the application program

- Check again page 89 !!!

### Transactional Processing in AS ABAP

- Transaction = Processing units grouped to provide specific units

- Transaction are ACID (Atomic, Consistent, Independent, Durable)

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

- **Dynpro processor** executes the screen flow logic of the application program, calls processing logic of ABAP application and trasnsfers field content to the processing logic

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

- Every work process is connected to a specific communication partner at database level. Cannot change it at runtime

- Business transactions are processing units groupped to provide a specific function. These processing units execute changes to the database that are consistent and make sense in business terms.

### Lock Management

- To ensure consistency, data cannot be accessed and changed by more than one user at any one time. => **Lock Management Concepts**

- The lock management is implemented via enqueue process

- Lock entries for data records are processed into a lock table. Lock entries can only be made if none already exist for the table entries to be locked

- The enqueue process can be implemented in one of the following ways:

1. As a work process

2. As part of ABAP Central Service Instance (preffered)

#### Lock Modes

1. Write Locks

&emsp;&emsp; - Lock data can be edited only by one user

&emsp;&emsp; - Other requests are rejected

2. Read Locks

&emsp;&emsp; - Several users can have access to the locked data at the same time

&emsp;&emsp; - Additional read locks are accepted

&emsp;&emsp; - Write locks are rejected

3. Enhanced write locks

&emsp;&emsp; - Write Locks can be successively requested and released by the same transaction

&emsp;&emsp; - An ENHANCED Write Lock can only be requested once, even by the same transaction

4. Optimistic Locks

&emsp;&emsp; - Respond like read lock ar first and can be changed to write locks

&emsp;&emsp; - Is set if the user displays the data in change mode

&emsp;&emsp; - Optimistic Locks on the same object do not collide

&emsp;&emsp; - To save data, the optimisitc lock should be changed to a write lock

- There are two ways to delete locks held by users: 

1. Ending user session in the user overview (Transaction SM04)

2. Manually deleting the lock entries in SM12/SMENQ

### Update Processing

- In SAP System a business process is mapped using an SPA transaction (can contain several screen changes)

- If user want to change a data record in an SAP transaction, they call the corresponding transaction in the dialog, make the appropiate entries on the screens and then initiate the update process by saving the data

- The steps of making a change in a data record in SAP Systems:

1. The program locks the data record for the user

&emsp;&emsp; - Addressing the enqueue work process

&emsp;&emsp; - The enqueue work process makes the relevant entry in the lock table or returns errors if there is a problem with the lock

2. If enqueue work process succeeded in writing the lock entry to the lock table, it passes the lock key it created to the user

&emsp;&emsp; - Program reads the record to be changed from the database and the user can change the record on the screen imagine of the SAP transaction

3. In the current dialog work process the program calls a function module using CAL FUNCTION ... IN UPDATE TASK

&emsp;&emsp; - After, it writes the update request to database update tables

&emsp;&emsp; - These funtions are called **VB** = act like temporary memory and store the data to be changed until it can be collected and written to the application tables in the database

4. At the end the transaction is closed with COMMIT WORK

&emsp;&emsp; - In this way the program initiatiates the close of the transaction after the end of the dialoag part of the transaction

5. Transfer from the dialog work processm update work process reads the log records that belong to this SAP transaction

6. The update work process transfer the changes marjed and collected in the VB tables to the datbase as an update request and evaluates the database response

&emsp;&emsp; - If an error occurs, the update work process triggers a database rollback leaves the log records in the VB tables and marks them as defective

7. The lock entries in the lock table are reset

### Printing

- A printer (fax, email and so on) must be first set up in the SAP System before it can be addressed

- Shortcut: CTRL + P

- After selecting a printer, a spool request contains information about data to be output, its formatting and the printer model used

### Background Processing

- SAP background processing is a method for automating routine tasks and for optimizing the use of computing resources

- In background processing, the developer instruct the SAP system to run programs

- It is suitable for long-running or resource-intensive programs at off peak times

- Segregation of background processing to special work processes gives an additional dimension for separating background processing and interactive work

### Communication Through RFC Gateway

- RFC = Remote Function call

- Each AS ABAP system contains a RFC

- When RCF or CPIC (Common Program Interface Communication) is used to communicate between application servers or SAP systems

#### Use case: Dialog work process has to establish an RFC connecton to a remote SAP System

- In the context of a request: retrieve customer data

1. The dialog work process uses a gateway of a remote SAP System

2. The remote gateway then transfers the request to the dispatcher

3. The dispatcher forwards the request to one of its work processes

4. The work process communicates directly with its gateway

### Processing Web requests

- ICM = Internet Communication Manager

- ICM enables SAP Systems to communicate using the protocols like HTTP(S) and SMTP

- ICM process the request and HTTP(S) requets can be processed in the ABAP work process

- If data is needed from the AS ABAP database, "memory pipes" are used to establish a connection to a work process

- ICM forwards the request to the ABAP Dispatcher which can handle the request as a normal one

```txt
Web Browser ------------|---------|                                           (3)
                  (1)   |   ICM   | ---------------------> ABAP Dispatcher ----------> D -------> ABAP Database
                  (1)   |         |          (2)                                                        |
Web Browser ------------|---------| <----------------------- Memory Pipes  <---------- D  <-------------| 
                                                                (4)                           (same D)
```


- The work process (D) can directly generate Web-enabled content which can be transferred to the browser via the ICM

### Administration Tasks for AS ABAP

| Transcation Code  | Action  |
| ----------------- | ------- |
| SM51 | Application Server(s) |
| SM50 | Work Process |
| SM04 | Active Users |
| SU01/SU10 | User Maintenance |
| SM36/SM37 | Background Processing |
| SM21 | System Log(s) |
| SM12/SMENQ | Lock Entries |
| SM 13 | Update Records |
| SM02 | System Messages |

### Functions of the Computing Center Management Systems (CCMS)

- The CCMS is a collection of integrated tools for managing, running and monitoring SAP Systems

- Roles of CCMS:

1. Background processing and job monitoring (SM37)

2. Configuration of the printer landscape (SPAD)

3. Tuning of the main memory areas of the SAP Systems (ST02)

4. Database Management (ex: backup) (DBACOCKPIT)

5. Configuration of SAP System Profiles (RZ10)

6. Dynamic load balancing (SMLG)

7. SAP System Monitoring (RZ20)

- The call of these functions are located in Tools -> CCMS

### Addendum: ABAP Message Server

- One MS runs in each SAP System

- Roles:

1. Central communication channel between the individual application servers of SAP Systems

2. Load Balancing of Logons

3. Information point for hte SAP Web Dispatcher and Application Server

- Application Server Started -> Dispatcher process contacts the message server -> Announce the services it provides

## Describing AS Java

- 3 Layers Infrastructure:

1. Presentation Layer: Web Browser

2. Application Layer: ICM redirects the information to SP + AS Java Buffer

3. Database Layer: DB - processes

- Web browser = standard UI for AS Java

- User request for AS Java = HTTP(S) request (usually) - it is received by ICM

- Processing -> takes place in the server process

- Nodes = server processes of AS Java

### Transactional Processing in AS Java

- Respects the ACID concept

- In AS Java changes and entries in UI are not made persistent immediately

- Only at save time the DB Transaction is performed

#### Persistence

- OpenSQL for Java framework

- Flow: Java Program -> Open SQL Engine (Communicates I/O with AS Java Buffer) -> Java

#### AS Java Administration

- SAP NetWeaver Administrator = combines the most important administration and monitoring tools

- To start SPA NetWeaver Administrator access https://<host name>:<port number>/nwa

##### Functional Areas of SAP NetWeaver Administrator

1. Availability and performance

2. Operations (application manager, start / stop)

3. Configuration (licenses, AS Java system properties, log configuration)

4. Error Analysis (SAP System Information, Java Class loader, Viewer)

5. SOA (JCo RFC provider)

### ABAP Language

- Programming Language for business applications

```sql
REPORT first_program

WRITE 'My first ABAP program!'
```

- Each screen (screens, selection screens, lists) communicates with ABAP to perform database operations

- To access the ABAP Source Code: System -> Status ... and double click to navigate to relevant ABAP Workbench tool

# Communication and Integration Technologies

## Remote Function Calls and BAPIs

- SAP Systems have interfaces at different communication levels. These interfaces can be divided into SAP proprietary interfaces and open interfaces

- Considering SAP proprietary interfaces, all higher interfaces access business objects or processes using the same technology: Remote Function Call (RFC)

### Remote Function Call

- SAP interface protocol based on CPI-C and TCP/IP

- Simplify programming communication processes between different SAP Systems

- **RFC manage the communication process, parameter transfer and error handling**

- RFC describe an interface and can be used to call functions in non-SAP Systems

- Every RFC is bideirectional. DDL (Dynamic Link Library) is an RFC interface to access outside of the SAP System

```sql
CALL FUNCTION <NAME> DESTINATION <DESTIONATION TO FUNCTION DEFINITION>
    EXPORTING ...
    IMPORTING ...
```

- RFC has become the most important SAP proprietary interface in the SAP environment

### BOR and BAPIs

- BAPI = Business Programming Interface = standardized programming interface that facilitates internal and external access to business processes and data

- BAPIs are defined in the Business Object Repository (BOR) as methods of SAP business objects and are object-oriented view

- BAPIs allow integration at the business level, not technical level

```txt
BOR : Business Object Repository
            |
            | contains
            |
      BO: Business Object       (e.g. SalesOrder)
            |
            | has method
            |
    BAPI: Business Application  (e.g. SalesOrder.ChangeFromData)
      Programming Interface
```

#### Possible Uses for BAPIs

- Link business processes across system boundaries

- Used by SAP integrate various solutions in the framework of SAP Business Suite

- Connect an SAP system to the Internet

- Conjuction with SAP Business Workflow scenarios that extend beyond system boundaries

- Connect to third-party software and legacy systems

## Explaining Cross - System Business Processes

### Examples of Cross-System Business Processes

- For example, it may be the case that within a company, the Human Resources system is  separated from the other business software systems. Obviously, the systems cannot be  completely separated, since the accounting system needs the employees' wage data. In  this situation, you need cross-system business processes to exchange the relevant data.

- Cross-system business processes are also used, for example, if two companies  collaborate closely and send joint orders to a vendor. The companies' business IT systems  need to communicate with each other to consolidate the quantities to be ordered. In this case, the business process does not just cross system boundaries, but also company boundaries.

- An additional example is the transfer of a limited quantity of specific data, for example, the  electronic transfer of account statement data from a bank to a company

### Application Link Enabling (ALE)

- ALE means of creating and operation distributed applications using SAP proprietary integration technology

- **The basic concept of ALE is to ensure the operation of a distributed, yet integrated system landscape**

- System that use ALE to exhange data can or cannot be located at the same company

- The format of transmitted data is IDoc format using RFC asynchronously every 15 minutes

- Can also use HTTP and XML

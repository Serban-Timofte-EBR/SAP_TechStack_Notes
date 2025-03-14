# User and Authorization in AS Java

## Identify the Structure and Configuration of the User Management Engine (UME)

- AS Java provides an open arhitecture supported by service providers for the storage of user and group data

- AS Java's services which are also referred to "User Store":

1. DBMS provider: storage in the system database

2. UDDI provider: storage via external service providers

3. UME provider: Connection of the integrated User Management Engine

### UME

- Has it own identity management for administering users formally knows as UME Administration Console

- Security settings can be used to define password policies

- Provides different self-service scenarios that can be used by applications

- Provides different self-service scenarios that can be used by applications

- User data can be exchanged with other systems using export / import mechanism

- **Arhitecture of the UME:**

1. Applications Accessing User Management:

&emsp;&emsp; - CE, EP, BI Java, PI

2. UME UI

&emsp;&emsp; - Logon, User Administration

3. UME Services

&emsp;&emsp; - Authentification SSO, User profile / Provisioning, Authorization

4. UME API Layer:

&emsp;&emsp; - User API, User Account API, Group API, Role API, ACL API

5. UME Core Layer:

&emsp;&emsp; - Persistance Management

6. Persistence Layer

&emsp;&emsp; - Database, LDAP Directory, AS ABAP Client

- UME Persistance manager offers the option of storing user data in different data sources

#### Data Partitioning

- So, in theory the data can be stored in different data sources

- In practice, we are working with a combination of the data sources database + directory service and database + ABAP user management

1. Attribute based data partitioning

&emsp;&emsp; - A user in UME has certain attributes (some global attributes, other application-specific)

2. User based data partitioning

&emsp;&emsp; - Data source in which users are stored is decided depending on the category of the user

3. Type based data partitioning

&emsp;&emsp; - Different object types can be distributed to different data sources

### SAP Identity Manager (IDM)

- Provides integrated Identity Management functions for heterogeneous system landscape

- Uses a central identity store to consolidate and save data from various source systems

- Role assigments cna be automated using rule definitions

### Tools for UME Configuration

- User management (UME) configuration is a Web Dynpro application

- Integrated into SAP NetWeaver and in System Administration (SAP Enterprise Portal)

## Maintaining Users and Groups

| Principle | Meaning |
| --------- | ------- |
| User | General properties of a user (name, email, phone number, etc) |
| User account | Logon-related properties of a user (password, validity, lock indicator) |
| Group | Set of user / groups |
| Role | Ser of (Java) authorizations |

### Special Features of the ABAP System Data Source

- ABAP users are visible in AS Java and can logon to AS Java with their ABAP passwords

- ABAP roles are depicted in AS Java as UME groups of the same name

- In AS Java, the assigment of ABAP users to ABAP roles appears as the assignment of UME users to UME groups

| User Type / Security Policy | Logon to AS Java | Password Change Forced | Mapped ABAP User Type |
| --------------------------- | ---------------- | ---------------------- | --------------------- |
| Default | Possible | Yes | Dialog |
| Technical Users | Possible | No | System |
| Internal Service User | Not possible | - | - |
| Unknown | Depends on AS ABAP user type | Depends on AS ABAP user type | Communication, Service and Reference |
| Custom Profile | Possible | Yes | - |

- The user type is specified during creation process via Identity Management

## Differentiating and using Authorization Concepts

1. Protecting Access to Applications

&emsp;&emsp; - JEE Security role

2. Protecting Access to Individual Activites

&emsp;&emsp; - JEE Security role

&emsp;&emsp; - UME Action / UME Permissions

3. Protecting Access to Objects

&emsp;&emsp; - Access Control List (ACL)

- In AS Java we can use Activity - related access control with security roles, Instance-related access control with roles and Intance-related access control with access control lists

### Creating and Assigning UME Roles

- Use Identity Management to maintain UME roles

## Naming special Principles

| User | Database | LDAP Server | ABAP System Add-in (+ABAP Java) | ABAP System Remote |
| ---- | -------- | ----------- | ------------------------------- | ------------------ |
| Administration user | Administrator | Administrator | J2EE_ADMIN | J2EE_ADM_<SID> |
| Guest User | Guest | Guest | J2EE_GUEST | J2EE_GST_<SID> |
| Communication user to data source | SAP<SID>DB | Freely definable | SAPJSF | SAPJSF_<SID> |

- Every user assigned to the Administrator group are given extensive system authorizations

- Emergency users = user for the UME if the user management has been incorrectly configured and no one can log on to an application

### Role Tree

- Permissions are combined into actions. The administrator then conbined actions into roles. UME roles can be assigned to a user

```txt
Permission  Permission  Permission  Permission  Permission  Permission  Permission  Permission
    |           |           |           |           |           |           |           |
    |           |           |           |           |           |           |           |
    | --------- | --------- |           | --------- | --------- |           | --------- |       
                |                                   |                              |
              Action                              Action                        Action
                |                                   |                              |
                | --------------------------------- | ---------------------------- |
                                                    |
                                                   Role
```

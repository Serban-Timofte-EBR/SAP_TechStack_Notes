# Users and Authorizations in AS ABAP

## Creating, Copying and Maintaining User Master Records

- SAP User operates in FrontEnd Leve

```txt
FrontEnd (Operating System User):   SAP GUI (SAP User)
                                        |
                                        |
                                        |
Application                         Dispatcher         (Operating System User)
Server                             |    |     |        
                                   D    D     B
                                     |     |
                                Database Server (DB User)
                                (Operating System User)
```

- Users can log on to an OS, database or SAP System using a combination of a user ID and password

### User Master Records

- **User Master Record** = allows users to log on to an ABAP-based SAP System

- **User Master Record** contains all data and settings that are required to log on to a client of the SAP System

#### Users and Technical Users

|   User    |   Technical User  |
| --------- | ----------------- |
| Described by a user master record | Does not have a business partner associated with it |
| Have the address tab | Does NOT have the address tab |
| Identified by user ID | Ussually work in the background or in RFC interfaces between systems |

#### Elements of User Master Record

- Logon Data -> displays the password and validity period of the user + user type

- Database Management System (DBMS) -> enables the SAP system to manage users and their authorizations

- Secure Network Communications (SNC) -> used for managing security functions that are not directly available but have been prepared in SAP Systems

- Defaults -> tab displays default values such as the default printer, the default logon language and so on

- Role and Profiles -> shows the roles and profiles that are assigned to the user

#### User Types

1. Dialog

&emsp;&emsp; - Parallel: Dialoag work process

&emsp;&emsp; - Normal dialog user is used for all logon types by just one person.

2. System

&emsp;&emsp; - Prallel: Background work process

&emsp;&emsp; - Dialog - free communication within a system or for background processing within a system

&emsp;&emsp; - System users are also used for RFC communication in various applications

3. Communications Data

&emsp;&emsp; - Dialog - free communication between systems

&emsp;&emsp; - Cannot use this type for dialog logon

4. Service

&emsp;&emsp; - Is available to a large, anonymous group of users

&emsp;&emsp; - Should only assign highly restricted authorizations to used of this tyep

&emsp;&emsp; - Example of usage: Anonymous system accesses using an ICF service

5. Reference

&emsp;&emsp; - General user, not specific to a particular person

&emsp;&emsp; - Cannot use reference to log on

| Password Change |   Enabled for Interaction (SAP GUI / ICF) |   Not Enabled for Interaction |
| --------------- | ----------------------------------------- | ----------------------------- |
| Yes | Dialog | Communications Data |
| No | Service | System |

- User Group Authorization Check (tab Logon Data) = Required if you want to divide user maintenance among several user admins

&emsp;&emsp; - Only the administrator can maintan users of this group

## Maintaining User Authorizations with Roles and Profiles

```txt
| ------------------------ |                | ------------------------ |
| User Master Record       |                | User Master Record       |
| ------------------------ |                | ------------------------ |
| Role E:                  |                | Role A:                  |
|    Authorization A ... H |                |    Authorization D ... F |
| -------------------------|                | -------------------------|
            |                                           |
            |                                           |
            | ----------------------------------------- |
                                    |
                                    |
                             Authorization Checks:                          
                            1. Program start allowed?
                            2. Authorizations exist?
                            3. Sensitive Objects: 
                                - Customer Master Record
                                - User Master Record
                                - Lock Entries
                                - Company Code
```

- **Important:** Communication or System user cannot logon using SAP GUI

### Authorization Objects and Authorization Checks

- Authorization Object: User Master Maintance (User Groups) -> Creates Authorizations (CRUD)

- Authorization Objects allows complex checks that involve multiple conditions that allow a user to perform an action

- An authorization is always associated with exactly one authorization object and contains the value for the fields of an authorization object

- For a transaction, the system checks the User Context to check if there are the necessary persimions granted

### User SAP*

- Is defined in the system code => only user in the SAP System for which no master record is required

- By default, a user master record for SAP* is created in client 000

### DDIC User

- Responsible for maintaining the ABAP Dictionary

- By default, a user master record for DDIC is created in client 000

### EarlyWatch user

- Dedicated for SAP's EarlyWatch users

- Usually, under client 066

## Evaluate Users and Authorizations

- To find information about users: Transaction SUIM (Information -> Information System)

- Failed authorizations are displayed in transaction SU53

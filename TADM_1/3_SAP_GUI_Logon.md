# SAP GUI and SAP Logon

## SAP GUI

- Part of the presentation layer

- Support the user to interact with SAP systems that are based on AS ABAP

- SAP GUI is based on Windows Style Guide

- There are 3 variants of the SAP GUI: SAP GUI for the Windoes environment, SAP GUI for the Java environment, SAP GUI for HTML

### SAP GUI for Windows

- SAP GUI for Windows environments is a Microsoft Windows environment written in C or C++ design for Windows based platforms

- The data flow between the presentation layer and the application layer does not consist of prepared screens, but rather of logical information about control elements

- This type of communication is DIAG Protocol = sends to the application layer compact information about control elements and user input

### SAP GUI for Java

- SAP GUI for Java environmnet is written in Java and is the platform - independent implementation of SAP GUI

- SAP GUI for Java uses DIAG protocol, too

### SAP GUI for HTML

- Requires Internet Transaction Server (ITS) which is part of AS ABAP on the server side

- SAP ITS provides the services required to generate responses in HTML format. These responses are sended in HTML format within the SAP Systems or to the Web Server or Web Client outside the SAP Systems

```txt
SAP GUI for Windows             SAP GUI for Java            SAP GUI for HTML
        |                               |                           |
        | ______________________________|                           |
                                        |                           |
                                ABAP Dispatcher ------------------- ICM
                                |       |     |
                                WP      WP    WP

                                Database level: ABAP
```

## SAP System Logon

- Many solutions shipped by SAP can be accessed using the SAP GUI

- SAP Logon is other program for starting the Front-End

- After calling the SAP Logon a list of SPA systems displays for which the log on process can be started (file SAPUILandscape.xml) - this file is preconfigured centrally and provided by the end user

- During the login, SAP Logon enables the log on and load distribution using the available resources for the selected SAP system

- During loggin on to the SAP system, the user authentificates himself using the username and the password (unless Single Sign-On - SSO was implemented)

- **Important:** A client usually corresponds to the mapping of a company in an SAP system. The client has a corresponding key field in the tables of the database used by the SAP systems.

### Managing user data using SAP Logon

- User data in SAP system = user master record

- User master records are stored in SAP system for each client

- **Important:** If you have a user for client 100, you can log on to client 100. If you have several clients, you have several user master records. these permit you to execute different activities depending on which client you are logged on

### Logging off from the SAP System

1. Closing all SAP GUI windows

2. Choosing System -> Log Off

3. Executing transaction code */nEx* (without confirmation pop up)

## Screen Structure

- The first screen that appearce after loggin is called SAP Easy Access

- This screen can be changed via Extras Tab -> Administration Information

## SAP GUI Functions, Help and Personalization

### User Menu and SAP Menu

- SAP Easy Access menu automatically displays after loggin on

- It represents the standard access point to an SAP system for he SAP GUI for Windows

- The entries of the SAP menus and the user menus can only be changed by system administrators

- The end user can switch from role-based user menu to standard menu if the system settings permit this

- To influence the design of the initial screen we can use Extras -> Settings (on the SAP Easy Access screen)

### Favourites Management

- The user is provided with functions in the Favourites area

- Ex: Links to frequently used transactions, web links or files can be stored in the Favourites area

- The Favourites liest contains references to SAP system functions or links to internet content or to files pn the end user's FE computer

- How to add to favourites: Favourites Tab -> Add OR Drag and Drop OR Adding links

- To delete on favourites: Highlish the entry -> Right-Click -> Choose Delete all favourites

### Calling Functions in SAP GUI

- There are multiple options to do this: Enter transaction codes in Command Field, Selecting entries from SAP menu, selecting entries from user menu, Selecting entries from the list of favourites, Choosing items from menus in the menu bar

- Alt + # shortcut to reach the menus in the menu bar

- For SAP Easy Access screen: using keyboard or Command field

- F1 to display input options for this field

**Possible Entries in the OK Code Field**

- /n -> cancel current transaction

- /nXXXX -> call transaction XXX directly from another transaction. Without prefix, you can call the XXXX transaction from SAP Easy Access screen

- /o -> display an overview of sessions

- /oXXXX -> call transaction XXXX in a new sessions directly from another transaction

- /nEND -> end logon session with a confirmation dialog box

- /nEX -> end the logon session without confirmation dialog box

- /i -> delete the session currently using

### Help Options

- F1 Help means to press F1 to display an explanation of fields, menus, functions and messages. F1 displays technical information on the relevant field.

- Can use other buttons in the Performance Assistant dialog box to display information on the selected field. 

### Personalization of the SAP GUI

- How to adapt the local layout? Using SAP GUI settings and actions can manage the input history by choosing Options ... -> Local Data. If activatedm the input history creates a small database on the FE containing the last n entries made in the input fields in transactions.

## Describing Navigation using a Web Browser

- Transaction PAL (Printing Assitant for Landscape) opens in a web browser

## SAP Business Client

- Provides users with a local client with a role-based navigation

- Central point of access for all SAP applications and transactions

**Comparison of SAP Business Client Functions**

| SAP Business Client for HTML    | SAP Business for Windows |
| -------- | ------- |
| No installation required  | Is installed on the end user device    |
| Integrated into the browser (SAP GUI for HTML) | Includes SAP GUI functionality     |
| Restricted functional scope on search functions, dropdown menus, drag and drop    | Offers functional scope    |
| No SAP Enterprise Portal functionality    | Can be used for SAP Enterprise Portal including role content    |
| Available for Windows, Linux and Mac OS    | Available for Windows only    |

## SAP Business Client for Windows

- UI intended for power users

- Is Used as a rendering engine

- SAP Business Client for Windows therefore replaces the SAP GUI as the central point of access for SAP applications

## SAP Business Client for HTML

- Browser-based interface with a restricted functional scope

- Used for ABAP transcations in order to access AS ABAP systems

1. Start SAP Business Client fot HTML

&emsp;&emsp; - Enter transcation *NWBC* in the SAP System

&emsp;&emsp; - OR: start the browser and navigate to https://<fully qualified host name> : <ICM_HTTPS_PORT>/sap/bc/nwbc

2. The business client for HTML opens in the browser windows

- SAP Business Client depends on the role assigned to the user. *Transaction for role maintenance is PFCG*

## Observations

- We can work in multiple windows (sessions) at a time in an SAP System within one log on

- SAP GUI for HTML can be used to log on to AS ABAP-based SAP systems. SAP GUI for HTML it is not available for AS Java-based SAP Systems

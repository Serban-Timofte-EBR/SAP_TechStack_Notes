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

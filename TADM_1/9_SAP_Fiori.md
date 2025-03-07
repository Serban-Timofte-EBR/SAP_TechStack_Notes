# SAP Fiori Foundation

## Introduction SAP Fiori

- SAP Fiori is a design language

### Principles

1. Role-based

2. Adaptive

3. Coherent

4. Simple

5. Delighful

- SAP Build Classic is a tool for prototyping web applicatios using SAP Fiori UI

1. Functional-based Applications

&emsp;&emsp; - **FROM:** One application for multiple roles

&emsp;&emsp; - **FROM:** Multiple entry points for the user

2. Role-based Applications

&emsp;&emsp; - **TO:** Decomposed apps for each role

&emsp;&emsp; - *TO:** One entry point for the user

## Using SAP Fiori Launchpad

- FLP = SAP Fiori Launchpad

- FLP offers a coherent user experience across different enterprise solutions by utilizing the capabilities of the user role to combine the decomposed apps in one surface

- The FLP marks atop of the page the Role assigned to the user

- SAP S/4HANA Cloud 2208 introduced SAP Fiori Horizon. There is a new theme including new features for the FLP. The theme (Horizon) introduces signature desgin elements to provide better focus on important parts on the screen

- SAP Fiori Horizon introduces *My Home space*: TODOs, Pages can be accessed directly without opening the space first, Recently of frequently used Apps and favourites can be started directly, Users can define Insights into analytical data as tiles or cards

- CAI = SAP Conversational Artifical Intelligence. It enables the use of digital assistants to interact with the SAP Systems.

## Personalizing SAP Fiori

- End users can personalize their own variant of SAP Fiori Launchpad (FLP) via User Actions Menu

- A catalog contains many tiles

- The catalogs hold all technical information to start an application.

- To see a tile in FLP it must embedded in a group

- Spaces concept can be used as alternative to groups in the home page. A space is visualized as a ribbon or tab at the top of the FLP and defines a frame for one or more pages. A page consists of sections showing tiles in the same way as groups have done before

- Spaces and pages are defined centrally in the system but only spaces are added to the launchpad

```txt
| ---------------------------------------------------------------------------- |
|                                      Space                                   |
|   | -------------------------------------------------------------------- |   |
|   |                                   Page                               |   |
|   |   | ------------------------------------------------------------ |   |   |
|   |   |                               Section                        |   |   |
|   |   |                                                              |   |   |
|   |   |  | ------- |                           | ------ |            |   |   |
|   |   |  |  Tile   |                           |  Tile  |            |   |   |
|   |   |  | ------- |                           | ------ |            |   |   |
|   |   |       |                                     |                |   |   |
|   |   | ------|-------------------------------------|--------------- |   |   |
|   | ----------|-------------------------------------|------------------- |   |
| --------------|-------------------------------------|----------------------- |
                |                                     |
                |                                     |
            | --|-------------------------------------|--- |
            |   |                  Catalog            |    |
            |   --------------> App Descriptor <-------    |
            | -------------------------------------------- |
```

- The App Descriptor connects the FLP with the app implementation in the system

### Personalization

- Action Mode for personalization: user should choose Edit Home Page in User Actions Menu of FLP

#### Tile Sizes

- (Basic) Tile -> Wide tile -> Flat tile -> Flat Wide tile -> Link

#### Themes

- SAP FIori Themese: SAP Belize (Deep) & SAP Quartz Light/Dark

- Design for HTML-apps like SAPUI5 and applications running in SAP GUI

## Application Types

1. Transactional

&emsp;&emsp; - Task-based Access

&emsp;&emsp; - Access to tasks like change, create or entire processes with guided navigation

2. Analytical

&emsp;&emsp; - Insights

&emsp;&emsp; - Visual overview of a dedicated topic for further KPI related analyses

&emsp;&emsp; - SAP HANA

3. Search and Explore

&emsp;&emsp; - View essential information about objects and contextual navigation between related objects

&emsp;&emsp; - Database: SAP HANA

- SAPUI5 is used in all application types for development <= Implementing JavaScript code directly or by defining metadata <= Generates JavaSript code at runtime

- **SAP Fiori apps reference library:** find detailed information on one of the thousands of SAP Fiori apps

- SAP Fiori App Recommendations analysis can be started on the main page by choosing Get SAP Fiori App Recommendations

## Describing SAP S/4HANA

### Landscape of SAP Fiori for SAP S/4HANA

1. SAP Fiori Launchpad

2. SAP Web Dispatcher (Optional)

&emsp;&emsp; - SAP Fiori Launchpad running in a client still connects to the FES via the SAP Web Dispatcher

3. SAP Front-End Server

&emsp;&emsp; - SAP ASE, SAP HANA, SAP MaxDB

4. SAP S/4HANA

&emsp;&emsp; - SAP HANA

- All application types are available for SAP S/4HANA (S4H). The important difference to the SAP Business Suite is that there is only one arhitecture type for all application types

- All applications act like transactional apps communicating via SPA Gateway over the FES with the BES now an S4H

## Managing SAP Fiori Content

### Content Assignment

- Next there are the 3 layers of SAP Fiori Launchpad:

- **Cross-Client** (Configuration)

&emsp;&emsp;&emsp;&emsp; - **Client-Specific** (Customizing)

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; - **User** (Personalization)

```txt
------- | ------------------------------------------------------------------------------------------- |
        |    Configuration (Cross-client)                                                             |
Layer   |                                   Customizing (Client-Specific)                             |
        |                                                                   Personalization (User)    |
------- | ------------------------------------------------------------------------------------------- |
        |                               Business Role                                                 |
        |                                                                                             |
Topic   |               Group                                   Space                                 |
        |                                                                                             |
        |                                                        Page                                 |
------- | ------------------------------------------------------------------------------------------- |
Duty    |                           Business Catalog                                                  |
------- | ------------------------------------------------------------------------------------------- |
Area    |                           Technical Catalog                                                 |
------- | ------------------------------------------------------------------------------------------- |
```

- Catalogs are the basis of SAP Fiori content in the FLP

- Technical catalogs define apps per solution area, whereas business catalogs reference there apps per duty of the user

- A technical catalog can only be defined in configuration

- Business catalog can be defined in configuration and customizing

## Creating SAP Fiori Spaces and Pages

- Manage Launchpad Spaces is an SAP Fiori Launchpad (FLP) app based on SAPUI5

## Managing SAP Fiori Catalogs

- **Tile** = a container that represents an App on the FLP

- The technical catalogs (TCR) cut apps by solutuion area and provide app descriptos consiting of tiles and target mappings for web apps

- Business catalogs (BCR) reference tiles and target mappings of TCs and BECs according to segregation of duty

- In SPA Business Suite, both TCR and BCR are replaced by BR (Business Roles)

### Catalog Management

- Standard, replicable and back-end catalogs are visible as read-only catalogs in the FLPD (Designer) and FLPCM (Content Manager). Both tools can display only the apps defined inside these catalogs as tiles and target mapping

- Remote catalogs can be used to load additional tiles from a remote system

### FLP Content Manager (FLPCM)

- FLPCM ease mass-administration of catalogs

### Important Info for Recap

- Dimensions of SAP Fiori: Design, Principles, Technology

- Main principles of SAP Fiori: Role-based, Adaptive, Simple, Coherent, Delightful

- Clients can be used for SAP Fiori: Web browsers, SAP Business Client

- Platforms that can integrate SAP Fiori: SAP Enterprise Portal, SAP Build Work Zone, SAP Mobile Services

- Perosanlization elements can be assigned to user roles: SAP Fiori group / catalog / space

- Apps meant by the term classic applications: ABAP Transactions, Web Dynpro ABAP applications

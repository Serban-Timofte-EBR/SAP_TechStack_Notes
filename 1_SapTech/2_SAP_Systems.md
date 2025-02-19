# SAP Systems

## Arhitecture of SAP Systems

- Business processes are mapped in applications

- SAP systems are process oriented view

- Applications: SAP ERP, SAP CRM, SAP SCM, SAP SRM, SAP PLM

- SAP ECC is designed for row-based data and need to aggregate tables.

- SAP S/4HANA takes advantage from column-based data and is much faster of specific values => does not need aggregate tables

- Column tables are efficient for analytical applications where requests for selections of data 
are not predictable. Column tables are optimized for parallel processing, as each CPU core is able to work on a separate column.

## Client - Server Communication

1. In Hardware Oriented View

```txt
                LAN/WAN
Client < ---------------------- > Server
```

2. In Software Oriented View

```txt
                LAN/WAN
 Client      < ---------------------- > Server
(Process 1)                           (Process 2)
```

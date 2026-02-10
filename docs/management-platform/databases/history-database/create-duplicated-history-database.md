# Create a Duplicated History Database

1. On the "**Databases**" -> "**History Database**" page, click the "Add" button. 
    ![alt text](1.png)
2.  In the following pop-up window, select the Duplicated History Database and click "Next" button.
    ![alt text](2.png)
3. Fill in the configuration and click "OK" button to save. 
    ![alt text](3.png)

**Configuration** ** Description**

| **Configuration Item** | **Description**    |
|----------------------------------|---|
| Name                             | Name of the history database.|
| Description                      | Description Information of the history database.|
| Database Connection 1            | The database connection used for this configuration, derived from the history database configured on the History databse list page. |
| Database Connection 2            | The database connection used for this configuration, derived from the history database configured on the History databse list page.|
| Enable Hierarchical Query        | Whether or not to hierarchize historical data queries.   <br> **Off**: All historical data query database connection 1, when database connection 1 fails query database connection 2   <br>**On**: All historical data query according to the query configuration, respectively query database connection 1 and database connection 2, when database connection 1 fails query database connection 2 |
| Master Database Query Range      | Historical data queries with query time within this configuration range will query database connection 1.|


# Product License

The trial version provided by the WAGO SCADA website, and the official version activated after purchasing a license have completely identical functions. Therefore, you can trial our product indefinitely before deciding to purchase WAGO SCADA. After purchasing a license , simply enter the license  code into the trial version to activate it, converting the trial version to the formal version.

The only limitation in trial mode is that WAGO SCADA will stop service every two hours, and you can start a new trial round by clicking the "Reset Trial" button on the interface.

## Product Authorization Explanation

 WAGO SCADA's product license is a server-based method and does not limit the number of clients and points. The upper limit of connected points and clients depends on the server's performance.

 Server license is composed of a combination of functional modules. You can purchase different functional modules according to your needs, referring to WAGO SCADA's[Typical Architecture Selection Guide](typical-architecture-selection-guide.md)  .

 Below are the functional modules provided by WAGO SCADA:

| **Functional Module** | **Dependency Module**     | **Description**       |
|:-----------------------|:---------------------------|:------------|
| Platform              | None                      | The  Platform Module is the only module that must be purchased. It includes common drivers such as Modbus TCP/RTU, OPC UA, Siemens S7, MQTT, as well as tag management, alarm management, background script calculation, schedule functions, etc. The Basic Platform Module also includes networking and redundancy Note 1  features. In a networking environment, the Basic Platform can operate independently as a data acquisition server and provide data to other WAGO SCADA nodes as needed. |
| 2D Visualization      | Platform                  | The 2D Visualization Module allows users to build monitoring screens using WAGO SCADA's Web editor.                                                                                                                                                                                                                                                                                                                                                                                                |
| 3D Visualization      | Platform，2D Visualization | The 3D Visualization Module allows users to build digital twin applications using WAGO SCADA's Web3D editor and can be displayed in conjunction with 2D pages.                                                                                                                                                                                                                                                                                                                                     |
| Database Connection   | Platform                  | The Database Connection Module allows WAGO SCADA to connect to third-party databases such as MySQL, PostgreSQL, InfluxDB, etc. WAGO SCADA can turn these databases into historical databases, storing data in them. The WAGO SCADA installation package comes witha SQLite database, suitable for small and simple scenarios.                                                                                                                                                                      |

 Note 1: The redundancy feature refers to two WAGO SCADA servers acting as primary and backup to each other. Therefore, you need to purchase two Platform Module license s for both servers.




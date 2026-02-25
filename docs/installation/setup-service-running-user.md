# Setup Service Running User

By specifying a particular user identity for the "WAGO SCADA" service, you can limit the service's permissions, granting it only the **minimum privileges necessary** for its operation. This helps prevent the service from being misused or exploited for malicious activities. Running different services under different users can **isolate** these services from each other, preventing vulnerabilities or issues in one service from affecting others. It also makes it easier to **track and audit** the activities of the "WAGO SCADA" service.

The default log-on identity for the WAGO SCADA service in Windows is the **Local System account**, while in Linux, it runs by default as the **root** user.

## "Log On As" for Windows Services

In Windows, you can set the "Log On As" identity for a Windows service using several different methods. Here are the steps to configure the service login identity using the Services Console and the command-line tool (`sc`).

Changing the service login identity requires administrator privileges.


**Method 1: Using the Services Console**

1. **Open the Services Console:**
    - Press `Win + R` to open the Run dialog.
    - Type `services.msc` and press Enter.
2. **Find and Right-Click the Target Service (WAGO SCADA):**
    - In the list of services, locate the service you want to modify (WAGO SCADA).
    - Right-click on the service and select **Properties**.
3. **Set the Log On Information:**
    - In the Properties window, switch to the **Log On** tab.
    - Select **This account**, then enter the account name and password.
    - Click **OK** to save the settings.    
   ![alt text](29.png)

**Method 2: Using the Command-Line Tool (**`sc`**)**

You can use the `sc config` command to configure the login information for a service.

```bash
sc config "WAGO_SCADA" obj= "Domain\Username" password= "Password"
```
 
- **Domain\Username:** This represents the account name, which can be in the format  `.\Username` (for local accounts) or `Domain\Username` (for domain accounts). <br>Using a domain account may be more appropriate if the service needs to access network resources or resources on other computers.
- **Password:** The password for the account.


## Setup Running User for Linux Services

WAGO SCADA only supports configuring services using `systemd`. Most Linux distributions use `systemd`, and you can set the startup and running user for a service by editing the service unit file.

1. Edit the Service Unit File:
Typically, service unit files are located in the `/etc/systemd/system/` or `/lib/systemd/system/` directories.
```bash
sudo nano /etc/systemd/system/wagoscada.service
```
2. Specify the User in the Service Unit File: 
Add or modify the `User` and `Group` options in the `[Service]` section to specify the user and group under which the service should run.
```plain
[Unit]
Description=WagoScada-Daemon
After=network.target

[Service]
WorkingDirectory=/usr/local/bin/wagoscada-4.0.3-linux-x64
ExecStart=/usr/local/bin/wagoscada-4.0.3-linux-x64/start.sh
Restart=always
RestartSec=10
SyslogIdentifier=wagoscada-log
User=myuser
Group=mygroup

[Install]
WantedBy=multi-user.target graphical.target
```

3. Reload the systemd Configuration and Start the Service: 
After editing the unit file, reload the systemd configuration and start the service.
```bash
sudo systemctl daemon-reload
sudo systemctl start wagoscada
```

**Notes:**

- Use the correct account and password to ensure the service can start and run properly.
- Avoid using weak passwords.
- Ensure the account follows the principle of least privilege, granting only the permissions necessary for the service to operate. The WAGO SCADA service requires read and write permissions for the **service installation directory** and the **service data directory**.
- Default service installation directory:

    Windows: `"C:\Program Files\WAGO SCADA"`

    Linux: `"/usr/local/bin/wagoscada"`

- Default data directory:

    Windows: `"C:\ProgramData\WAGOSCADA"`

    Linux: `"/usr/share/WAGOSCADA"`


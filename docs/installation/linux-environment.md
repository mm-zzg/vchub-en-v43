# Linux Environment

WAGO SCADA provides an installation package for the Linux environment, with the file name wagoscada-x.x.x-linux-x64-installer.run.
## **Installation Steps** 

1. Copy the installation package to a directory on the Linux server.
2. Grant the file owner the permission to execute the installation file 
   ![alt text](17.png)
3. Run the installation package in the directory using the command ./ followed by the file name. 
   ![alt text](18.png)
4. Select the installation language.
   ![alt text](19.png)
5. Customize the installation directory or use the default directory. If the installation directory does not exist, the installer will create it automatically.
   ![alt text](20.png)
   ![alt text](21.png)
6. Customize the data directory or use the default directory.
   ![alt text](22.png)
7. Wait for the installation to complete. This process may take some time, so please be patient. 
   ![alt text](23.png)
8. The installation is complete.
   ![alt text](24.png)
9. After completion, the default access to the VC Hub site is: `http://localhost:8066`. After the installation, you will enter the configuration wizard interface.

**Notes:** 

1. The program is supervised and managed by the systemd service manager that comes with the Linux system. Ensure that the systemd on the server is running properly.
2. The installation script includes operations such as creating scripts, so make sure you have sufficient permissions.

## Configuration

1. Read and agree the license agreement
   ![alt text](25.png)           
2. Create an administrator user. Remember this username and password, as you will use them to log in for the first time. 
   ![alt text](26.png)
3. Port configuration, configure HTTP, HTTPS ports, and remember the access port. 
   ![alt text](36.png)
4. After completing the above steps, wait for the program to load, and then you can log in to the default workspace with the administrator user created in step 2.

**Note**: If you perform an upgrade installation, a new empty workspace will be created by default. To return to the original workspace, you need to log in to the new workspace first and then manually open the original workspace from the workspace list. 

## Security Configuration (Optional)

To further enhance system security, it is recommended to perform the following steps after configuration to set permissions on the **service directory and application data directory**, allowing only specific users to access or modify them. This ensures that sensitive data is well protected and potential risks are minimized.

1.  Create a Dedicated Service Account
    Create a dedicated system account (e.g., wago_scada) with no interactive login, used only to run service processes:
    ```
    sudo useradd -r -s /sbin/nologin wago_scada
    ```
    Then, configure passwordless sudo for this account via the sudoers file:
    ```
    wago_scada ALL=(ALL) NOPASSWD: ALL
    ```
2. Set Service Installation Directory Permissions
    
    
    Assign ownership of the service installation directory (e.g., /usr/local/bin/wagoscada) to wago_scada and restrict access to other users:
    
    
    ```
    sudo chown -R wago_scada:wago_scada /usr/local/bin/wagoscada
    sudo chmod -R 750 /usr/local/bin/wagoscada
    ```
   **Note:** Perform this step before changing the service run account, otherwise the service may lose access.  

3. Modify Service Run Account
   Configure the service to run under the wago_scada account:
   ```
   sudo systemctl edit wagoscada.service
   ```
   Add the following lines under the [Service] section:
   ```
   User=wago_scada
   Group=wago_scada
   ```
   Then reload the systemd configuration and restart the service:
   ```
   sudo systemctl daemon-reexec
   sudo systemctl restart wagoscada.service
   ``` 
4. Set Application Data Directory Permissions<br>
    Assign ownership of the data directory (e.g., /usr/share/WAGOSCADA) to wago_scada and ensure read/write access while restricting other users:
   ```
   sudo chown -R wago_scada:wago_scada /usr/share/WAGOSCADA
   sudo chmod -R 750 /usr/share/WAGOSCADA
   ``` 
5. Verify Configuration
   Check that the service is running under the wago_scada account and confirm the site is accessible:
   ```
   systemctl status wagoscada.service
   ``` 
   Open a browser and visit the WAGO SCADA site (e.g., http://localhost:8066) to verify it is running correctly.

## **Uninstallation Steps**

1. Go to the parent directory of the installation directory.
2. Grant the file owner the permission to execute the file "wagoscada-uninstall.sh"
![alt text](27.png)


3. Run the script "wagoscada-uninstall.sh".
![alt text](28.png)
4. After these operations, all program-related files will be removed, and the process supervisory service will also be removed.

**Notes:**  

The uninstallation script includes operations such as deleting files, so ensure you have sufficient permissions.


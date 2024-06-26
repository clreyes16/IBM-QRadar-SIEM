# Configure QRadar Autoupdate in Air Gapped Deployment
<sub>Expectations/Requirements: Access to system that has outbound internet connection is required, as well as the ability to transfer the autoupdate.tgz into the air gapped environment.</sub>

IBM QRadar will automatically update the deployment nightly if connected to the internet, retrieving updates, and applying any changes automatically. This how to guide is not for clients whose QRadar is currently pulling automatic updates from IBM. This how to guide is for deployments with internet connection, it is for those whose systems are in completely air-gapped or are unable to retrieve automatic updates. Examples of such environments are SCIF’s and other highly sensitive areas where the organization has deemed the risk of being connected to the public internet too great and has instead opted to remove internet connection. Ensuring that the clients QRadar deployment stays up to date is of critical importance. These weekly updates provide updates to DSMs for enhanced parsing, configuration updates which help to eliminate false positives and protects the deployment from the latest malicious sites, botnets, and other suspicious activity. Below is a description of all the information which updates provide.


Update files can include the following updates:
* Configuration updates that are based on content, including configuration file changes, vulnerabilities, QID maps, supportability scripts, and security threat information updates.
* DSM, scanner, and protocol updates that include corrections to parsing issues, scanner changes, and protocol updates.
* Major updates, such as updated JAR files or large patches, that require restarting the user interface service.
* Minor updates, such as daily automatic update logs or QID map scripts, that do not restart the user interface service.

**Table of Contents**

  * [Download QRadar Auto Update from IBM Fix Central](#download-qradar-auto-update-from-ibm-fix-central)
  * [Configure QRadar Console for local Auto Update](#configure-qradar-console-for-loca-auto-update)
  * [Modify QRadar Auto Update Settings](#modify-qradar-auto-update-settings)
  * [Update QRadar](#update-qradar)

## Download QRadar Auto Update from IBM Fix Central
<sub>Expectations/Requirements: This section requires both an internet connection and a w3 account to access the IBM Fix Central site.</sub>

1. Open a web browser, such as FireFox or Chrome.

2. Within the URL address bar enter the following link: https://www.ibm.com/support/fixcentral/

3. Within the "Product selector" window type qradar, scroll down and select "IBM Security QRadar SIEM", as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/6e4be290-d3a4-4b1f-80be-c51566f50fc3)

4. After selecting IBM Security QRadar SIEM, the next step is select both the "Installed Version", "Platform" and click "Continue"

* Installed Version = 7.5.0
* Platform = Linux

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/27a0da5c-7090-45c0-9cae-be4513a7acee)

5. The next page is the "Idenfity fixes" page, leave the default option of "Browse for fixes", as shown and click "Continue"

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/d472361f-3177-4b7a-aae9-baa329e01ef1)

6. After clicking continue, the following page of "Select fixes" will be loaded. Select "AUTOUPDATE" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/f061be25-97f9-4bff-817f-5ce05e0dc871)

7. This will automatically send you to the "AUTOUPDATE" section of the page. Locate the latest autoupdate and click on the name as shown.


   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/6b26109f-36f5-42f7-85bc-2b41993f2e21)

8. You will then be redirected to the IBM Login page as shown. Enter your IBMid and click "Continue", as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/7960cb14-c1be-4035-858d-62e7b832fb00)

9. The next webpage redirection will be to the selection of single sign on. Select the applicable option.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/cca828a8-8154-4f27-8f90-a1bf1bb97775)

10. Enter your information and click "Sign in".
    
    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/b098feaa-1898-4c3e-883b-407201af9dce)

11. Once successfully logged in you will be redirected to the Download options page, as shown. Select "Download using your browser (HTTPS) and click "Continue".

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/7823c7df-1381-4c0a-a6a9-42d27b2fbe89)

12. You will be redirected to the "Order fixes" page as shown. Click on the .tgz autoupdate file in order to download the updates file.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/09de87f4-76b7-494a-bee0-b9be4f64827a)


13. Once the download for the autoupdate file is completed, verify it is in the your downloads directory, as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/bbd21b36-4990-4bdb-88ff-0921d575b2f5)


## Configure QRadar for Local Autoupdate
1. Login to QRadar Console CLI via Putty or other terminal emulator

2. Verify the /opt parition has sufficient available space via the following command:

   ```bash
   df -h
   ```
3. Verify the autupdates directory is not present within the /opt/qradar/www directory via the following command:

   ```bash
   ls /opt/qradar/www
   ```
   
   ![image](https://media.github.ibm.com/user/379722/files/438b29eb-7c4a-4bf1-a295-2969c4b87468)

4. If the autoupdates directory is present, you can remove it via the following command:

   ```bash
   rm -rf /opt/qradar/www/autoupdates
   ```
   
5. Create the /store/downloads/autoupdates directory via the following command:

   ```bash
   mkdir -p /store/downloads/autoupdates
   ```
   
   ![image](https://media.github.ibm.com/user/379722/files/829018e1-33a8-462d-8cfa-625d3b2ebf71)

6. After creating the autoupdates directory, the next step is to create a symbolic link between /store/downloads/autoupdates and /opt/qradar/www via the following command:
   
   ```bash
   ln -s /store/downloads/autoupdates /opt/qradar/www
   ```
 
    ![image](https://media.github.ibm.com/user/379722/files/7fe06d7d-e1b5-4c44-8b20-211345acd103)

7. Verify the symbolic link was created via the following command:

   ```bash
   ll /opt/qradar/www
   ```
   
   ![image](https://media.github.ibm.com/user/379722/files/933a14ec-2f60-4781-bff0-ae1946091dd3)

8. Transfer autoupdate.tgz from downloads directory to the QRadar Console directory /opt/qradar/www/autoupdates via WinSCP or other file transfer agent as shown.
   
   ![image](https://media.github.ibm.com/user/379722/files/e113ef75-01f3-41c4-9eb3-d0611ebb6854)

9. Verify the autoupdate.tar.gz successfully transferred as shown.

   ![image](https://media.github.ibm.com/user/379722/files/1358eb5c-2fdc-4269-a965-2c694e2e8870)
   
10. Within the QRadar Console CLI change directories to the /opt/qradar/www/autoupdates via the following command:

    ```bash
    cd /opt/qradar/www/autoupdates
    ```
    
    ![image](https://media.github.ibm.com/user/379722/files/20d86e20-6b09-4abe-b6ec-ee86449f2732)
    
11. Extract the autoupdate.tgz within the /opt/qradar/www/autoupdates direcotry via the following command:

    ```bash
    tar -xvzf autoupdate-1718222549.tgz
    ```
    ![image](https://media.github.ibm.com/user/379722/files/b39539f8-09f8-4e2a-aa9f-413bb3323156)


12. Verify the contents of the autoupdate.tgz file completely extract as shown.

    ![image](https://media.github.ibm.com/user/379722/files/6dcd616c-b0aa-4060-8e95-e638ff11741c)
    
## Modification to QRadar Auto Update     

1. Log into QRadar webpage.

2. After logging into the QRadar webpage, click on the "Admin" tab as shown.

   ![image](https://media.github.ibm.com/user/379722/files/ffe570e9-b0ef-4061-bfe8-72c89f9766e1)
   
3. Select the Auto Update options as shown.

   ![image](https://media.github.ibm.com/user/379722/files/00961745-4484-4025-89e6-56b153dff42c)

4. The Auto Update pop-up window will appear as shown, click on "Change Settings" as shown.
  
   ![image](https://media.github.ibm.com/user/379722/files/8aa3e236-c84c-4dc4-bebf-3fa4cb3a1360)

5. The "Change Settings" window will appear as shown. Click on "Advanced".

   ![image](https://media.github.ibm.com/user/379722/files/babf686b-42c6-4683-9fa5-cf5fcd06c062)

6. The default internet information for autoupdate retrieves will be prepopulated as shown. 

   ![image](https://media.github.ibm.com/user/379722/files/1de6e7fa-b3c8-47e3-8761-e28328ad521b)

7. Modify the following fields, as shown.
   * Web Server = https://fqdnofconsole/
   * Directory = autoupdates/
   * Click "Save"
   
   ![image](https://media.github.ibm.com/user/379722/files/73f4696f-c226-41e5-887f-271fa8bf0ec3)


8. The "Application Restart Required" pop-up window will appear. Click "Yes" as shown.
   
   ![image](https://media.github.ibm.com/user/379722/files/23898df8-c7ce-4dbe-bfb0-b4202e748875)

9. After clicking "Yes", you will be returned to the advanced setting page. There will be the following message shown will appear. 

   ![image](https://media.github.ibm.com/user/379722/files/c731c29b-b20b-4098-a767-962227637744)

   
10. After receiving this message, navigate to the left pane and Click on "Check for Updates", after which click on "Get New Updates" as shown.
 
    
    ![image](https://media.github.ibm.com/user/379722/files/e38e768b-0c3d-4647-98e7-402874c048e4)

    
11. The following confirmation windows will appear, click "OK".

     ![image](https://media.github.ibm.com/user/379722/files/7a8d60e5-0515-4369-b3a5-6a086454884e)

12. After clicking "OK", you will receive the following message as shown. 
 
    ![image](https://media.github.ibm.com/user/379722/files/7cbd47d0-0696-449a-9df4-8774df6d4131)
    
13. Return to the QRadar Console CLI and run the following command and watch the output. Verify the auto updates complete successfully as shown.

    ```bash 
    tail -f /var/log/qradar.log | grep update*
    ```
    ![image](https://media.github.ibm.com/user/379722/files/eaa97a10-a571-417e-b845-e935c6043a4c)

14. Return to the Auto Update pop-up window and click on "View Log". Ensure you see the following message of "All updates completed successfully".

    ![image](https://media.github.ibm.com/user/379722/files/5ee9a634-3e8b-4e3a-a2ca-05b4f012b75b)




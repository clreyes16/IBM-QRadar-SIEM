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





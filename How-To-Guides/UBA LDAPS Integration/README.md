# QRadar UBA LDAPS Active Directory User Import
<sub>Requirements: Several requirements must be meet in order to properly accomplish this how to guide.  First, the Active Directory administrator must create and provide a service account that has the ability to LDAP bind with Active Directory.  Secondly, the QRadar Administrator must obtain the Root Certificate Authority certificate in PEM format. This can be done several ways, this guide will demonstrate one such way.  Finally, the user performing this how to guide needs administrator level access to the UBA application.<sub>
---
Purpose: This how to guide provides instruction on how to LDAPS import users from Active Directory into QRadar User Behavior Analytics application. 
----
**Table of Contents**
* [Obtain Root CA Certificate in PEM Format](#obain-root-ca-certificate-in-pem-format)
* [Download Root CA Certificate](#download-root-ca-certificate)
* [Import AD Users into UBA](#import-ad-users-into-uba)
* [Verify AD User Import into UBA](#verify-user-import-into-uba)
* [Conclusion](#conclusion)
---  
## Obtain Root CA Certificate in PEM Format
<sub>Expectations: This section expects that the QRadar webpage is already TLS encrypted and the "QRadar TLS Certificate Implementation" how to guide located in this repoistory was used to do. If the <sub>

1. Login to QRadar Console CLI via Putty or other terminal emulator.
   
2. Change directories to the /root/new.certs/ directory were the QRadar webpage cert should be located.

   ```bash
   cd /root/new.certs/
   ```

3. Locate the ca.crt certificate as shown via the ls command.

   ```bash
   ls
   ```
   
   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/d4944deb-131f-4479-925c-4be49085be88)

4. Convert the .crt formatted ca certificate into a PEM formatted certificate via the following command.

   ```bash
   openssl x509 -in ca.crt -out ca.pem -outform PEM
   ```

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/46b139f2-4ad0-4348-9ae2-5194c08f0c5d)

5. Verify the PEM certificate was created as shown.

   ```bash
   ls
   ```

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/77e7c838-9ee2-4eca-bd93-b8d12adf5067)

---
## Download Root CA Certificate

1. Open WinSCP or other file transfer program.

2. Enter the QRadar server information, example shown.

   * Host name: FQDN or IP Address of QRadar Console
   * User name: username such as root
   * Password: password for the selected user.
   * Click Login
    
   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/0d096efa-887b-48d1-8e00-bed8b0d90a03)

3. Navigate to the /root/new.certs directory within the QRadar server side as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/4780ae07-0693-48b6-b4fe-687766d96a90)

4. Drag the ca.pem file over to the local machine within the desired directory, as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/5c6d6b43-e709-469d-afe8-1ddaf0a86a9b)

5. Having extracted the ca.pem certificate to the local machine directory, proceed to the next section.

---

## Import AD Users into UBA

1. Log into the QRadar GUI.

2. Click on the "Admin" tab, scroll down to the "User Analytics" app and click on "User Import" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/a4bd77f2-87e4-45d8-ac14-3f7186cf84e5)

3. At the "User Import" page, click on "Add", as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/4ecd1d8b-b9dd-47de-9a4d-79f7df412bac)

4. Click on  the LDAP/AD option as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/19f660c5-d83f-4a65-9ce7-6797c0d2d33d)

5. You will be brought to the "LDAP server configuration" page as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/f5d910d7-877f-4d5c-839d-c7ac42daf977)

6. Enter all relevant LDAP information into the configuration page as shown. All this information can be different depending on environment the the OU which needs to be monitored.

   * Protocol: ldaps://
   * LDAP server host*: the FQDN of the LDAPS server
   * Port: 636 (LDAPS)
   * Username (Bind DN): service account created by the Active Directory administrator
   * Password: password for service account used in the Username (Bind DN) field.
   * Base DN: The DN of the OU you want to monitor
   * Filter: (&(sAMAccountName=*)(samAccountType=805306368))

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/90a371a8-c359-4da7-aa2a-14beba678617)

7. Click on the "Certificate" upload button as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/3e092cb9-2ccf-4ac1-97c0-df4a1102f58f)


8. Navigate to the location where the ca.pem was stored on the local machine. Select the ca.pem and click "Open" as shown. 

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/5f0b4b0d-0e2e-433b-b854-2e3a6e46881c)

9. Verify the ca.pem file was uploaded and then click "Test connection", as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/afdec403-cdf4-4da1-a4a7-03a47e834bc4)

10. If successful you should receive a green check mark next to "Test connection", "Number of attributes" and a list of attributes in the right window pane. Click "Next".

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/0397b34a-f60d-434a-9b34-4d4ee3c14999)

11. You will be brought to the "Other import settings" page. The "Configuration name*" field can be changed or left the default FQDN of the LDAPS server, as shown. Click "Next" after you have enter the desired name.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/c7e7f7c3-7c6b-4b4f-9a26-c561c5857161)


12. You will be brought to the "Summary" page, verify all the information and click "Save".

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/468be31b-414f-4c0a-b50f-91820c8a7d1e)


13. This will return you back to the "Import Configurations" page with the new import present, as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/0367822d-7acf-439a-a812-0b92b65f0f47)

14. Click on the play button to start the import, as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/d59c743b-f641-4759-ba56-926c68e7e62d)

15. The "Last poll status" will change from "Idle" to "Queued" and finally Succeded as shown along with the number of "Users extracted" and the Last poll date, as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/544298e5-6759-46db-97ce-bc1b4fe864f8)
---

## Verify User Import into UBA

1. Finally, click on "User Analytics" tab in the toolbar as shown. Verify the number of users which were imported and verify they are in the "Monitored users" left pane as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/72585350-1215-4523-b13d-6a747eb8096f)

---

## Conculsion

1. In conculsion each UBA LDAP import can only do up to 500K users. You can add more configuration as you see fit or add more for different user groups. 










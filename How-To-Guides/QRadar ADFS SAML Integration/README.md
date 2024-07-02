# QRadar ADFS SAML Integration
<sub>Expectations/Requirements: To successfully complete this how to guide a Windows administrator will be needed with access to both the ADFS and Certificate Authority (CA)servers. The QRadar administrator with access to both the webpage and CLI will be required as well.</sub>

This how to guide provides instruction on SAML integrating QRadar with Windows Active Directory Federation Services (ADFS) server. This allows for different forms of MFA such as token based logon and PIV/CAC, while still allowing the capability for username/password logon if desired.


**Table of Contents**

  * [Build ADFS Certificate Template](#build-adfs-certificate-template)
  * [Configure ADFS Certificate](#configure-adfs-certificate)
  * [Configure ADFS Server](#configure-adfs-server)
  * [Enable ADFS IDP Signon Page](#enable-adfs-idp-signon-page)
  * [Download FederationMetadata.xml File](#download-federationmetadata.xml-file)
  * [Configure QRadar SAML 2.0 Authentication](#configure-qradar-saml-2.0-authencation)
  * [Configure ADFS Relying Party Trusts](#configure-adfs-relying-party-trusts)
  * [Configure QRadar Accounts](#configure-qradar-accounts)
  * [Verify Successful QRadar Logon](#verify-successful-qradar-logon)
---
## Build ADFS Certificate Template
<sub>Expectations/Requirements: This section requires administrator access to the CA server and the ability to create and issue templates.</sub>

1. Log onto CA server or server that is hosting the certificate authority service.

2. Open the "Server Manager" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/f0c1fb00-10e2-40aa-94a8-4cfe23bf3851)


3. Click on "Tools" and then "Certification Authority", as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/8c5ecd6f-66f3-4019-9a6d-2ed9ff578689)

4. The certification authority pop-up window appear, expand the CA by clicking on the menu arrow as shown to see all certificate directories.    

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/89eb3439-49ec-4f1f-bb53-00b8c1886c28)

5. Right click on "Certificate Templates" and click on "Manage".   

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/4262f064-4fed-439b-aebe-5b6908f3f439)

6. The "Certificate Templates Console" will appear. Locate the "Web Server" template and right click on it and select "Duplicate Template".

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/855f9b02-4dab-441a-9565-90090f90456a)

7. The "Properties of New Template" window will appear as shown.   

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/aa497240-50e2-46de-8a7e-d44fb0c1a662)

8. Domain computers must be added to the security of the template. To do this click on the "Security" tab and then click "Add...".

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/e1f53625-5836-4613-9ca5-76a93cbdfe38)

9. The "Select Users, Computers, Service Accounts, or Groups" pop-up window will appear. Type "Domain Computers" and click "Check Names" as shown to ensure you entered the right object. After ensuring the right object was selected click "OK".

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/fc43aed7-ace4-4fbb-8b8a-c9c3d16fc9ab)

10. The "Select Users, Computers, Service Accounts, or Groups" pop-up window will close and you will be returned to the "Properties of New Template" window. Click on "Domain Computers" and provide "Allow" premissions for Read, Enroll and Autoenroll as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/171ac47b-a883-44a2-8617-fcda3807dd7e)

11. Having completed the security requirements for the certificate, the next step is to modify the request handling. Click on the "Request Handling" tab as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/2c90a292-6adf-4bb1-92c4-d245c8979064)

12. Locate the "Allow private key to be exported" and chck the box to enable this as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/f2885784-e741-4216-b3ab-e37390e57462)

13. After enabling the ability to export the private key, the next step is to provide a display name. To do this click on the "General" tab and within the "Template display name:" field enter the desired name as shown.    

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/770ca202-c190-42ca-b874-4450d8ca2bf7)

14. Close out the template by clicking on "OK" as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/467c783a-9dfb-4cb9-bb66-34ce5193f9db)

15. This will return you to the "Certificate Templates Console", verify you see the new created certificate via the display name you provided in step 13. Example: ADFSv2.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/53e53955-f532-4f7b-a522-ae5fba6ab3a9)

16. Close out the "Certificate Templates Console" window.

17. You will be returned to the "Certification Authority" page. Right click on the "Certificate Templates" directory and select "New>" and "Certificate Template to Issue".    

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/0972cbbd-29c7-4e7d-9657-8823bba77984)

18. The "Enable Certificate Templates" window will appear. Select the template you previously created, example: ADFSv2 and then click on "OK" as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/f72e6403-6aa6-487a-83be-b159c86b0130)

19. Finally, verify the new template is within the "Certificate Templates" directory as shown. Once verified you can close out the "Certification Authority" and log off of the server.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/df62de57-5f3f-499a-aa99-47a48f8160aa)
---
## Configure ADFS Certificate

1. Logon to ADFS server or server hosting ADFS service.

2. Click the "Windows" icon in the bottom left corner and type "mmc".

3. The "mmc" will appear, click on it to open.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/a4f73b98-1b64-4d23-bfe6-a3a77bd981a0)

4. The "User Account Control" pop-up window should appear, click "Yes" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/8a82e61a-0c83-4853-995a-7b46051b5736)

5. You will be brought to the mmc console. Click on "File" and "Add/Remove Snap in..." as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/3e39f199-70e5-4a31-b286-654aa82bdcd9)

6. The "Add or Remove Snap-ins" window will appear as shown. Select "Certificates" from the "Available snap-ins:" pane and then click "Add>" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/4c986d62-64e4-4c8f-b439-6d2b502eaa3a)

7. The "Certificates snap-in" window will appear. Select the radial button for "Computer account" and then click "Next" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/fc84dce1-75e0-47a6-93a5-08d98e8cdfd2)

8. The "Select Computer" window will appear. Leave the default "Local computer" option selected and click "Finish".

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/b7879ad3-497f-457e-bfa1-afc6edfeb284)

9. After clicking on finish, you will be returned to the "Add or Remove Snap-ins" window as shown. Verify the "Certificates (Local Computer)"    

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/1cfb65e7-4b45-4b3c-921e-aa1c41e05b98)

10. You will be returned to the Console page. Expand the "Personal" directory by clicking on the drop down arrow as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/56d27fc6-a32c-418d-a346-6c49fcc5637b)

11. Right click on the "Certificates" directory, select "All Tasks" and then select "Request New Certificate...".

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/86061b48-0c59-4704-903f-2af824d0d0c0)

12. This will launch the "Certificate Enrollment" window as shown. At this window click "Next".

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/a06ebf4d-407e-4beb-a631-f628a445ca5d)

13. The "Select Certificate Enrollment Policy" will appear, leave this as default and click "Next".

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/0b878d85-52af-4a23-a583-fa33c32404d6)
    
14. The "Request Certificates" page will appear. Select the certificate created in the previous section, example: ADFSv2. Then click on "More information is required to enroll for this certificate. Click here to configure settings."

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/9b3f9da7-71bf-44f7-ae85-dc454663aba6)

15. This will launch the "Certificate Properties" pop-up window. Perform the following actions within the "Subject" tab.
    * Subject name = Type: Common Name -> FQDN (example: adfs.dmz.fisc.domain)
    * Alternative name:  Type: DNS -> FQDN (example: adfs.dmz.fisc.domain)  

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/a86968f1-68da-4aa1-b3c8-050091492144)

16. After entering that information, click on the "Private Key" tab. Expand the "Key options" section and select to make the private key exportable as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/d2d0d54e-8f61-45e7-9746-64aef6af52bb)
    
17. Next, click on the "General" tab and enter a name within the "Friendly name:" field, example: adfs.dmz.fisc.domain. Then click "OK" as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/03ed9656-1d3a-46db-9041-38343ecfece6)


18. You will be returned to the "Request Certificates" window, click "Enroll" as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/c2d56632-a7cc-40ea-91b6-06914b75d661)


19. The certificate will begin to be enrolled. Ensure the "STATUS" equals "Succeeded" as shown. Click "Finish".

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/7b7a8b2f-526a-47f6-a8b4-50e171592a39)

20. You will be returned to the MMC Console window. Verify the certificate is found within the main window as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/ee6f5ee3-50d9-49b1-add5-855baee96dd5)

21. Double click on the certificate in order to open the certificate properties, as shown. Click on "Details" tab.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/7682bd17-2b16-486e-b3ac-6aa28c5ed9bc)

22. Within the details tab, click on "Copy to File..." as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/d204d9bc-4e7b-42ba-96e3-b429e06d6e38)
   
23. This will open the "Certificate Export Wizard". Click on "Next" as shown. 

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/f64937ee-12b3-4bc4-945b-b0db85863df6)

24. In the "Export Private Key" menu, select the "Yes, export the private key" and click on "Next" as shown.     

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/3d5e1116-a63e-4a20-8171-ec5690bd0d5e)

25. This will bring you to the "Export File Format" menu as shown. Select the following options:
    * Check: Personal Information Exchange - PKCS #12 (.PFX)
    * Check: Include all certificates in the certification path if possible
    * Check: Export all extended properties
    * Uncheck: Enable certificate privacy
    * Next


   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/7f6dce2f-9f88-4186-86ee-ca7d18a37cbd)

26. You will be brought to the "Security" page as shown. Select the "Password:" option and enter the desired password as shown in both fields. Click "Next". 

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/4decc30a-3cf6-4501-8328-597b7c5b204d)

27. This will bring you to the "File to Export" page. Click on the "Browse..." option as shown.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/530f7152-de36-4b11-b991-97b2428ef5a0)

28. Navigate to the desired directory where the certificate will be stored and provide it a name in the "File name:" field and click Save as shown.
    * Example: Desktop -> adfs -> save


    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/4f060a03-8d6a-4cb9-a594-91a80e6acc4b)

29. This will return you to the "File to Export" menu. Under the "File name:" field ensure the path and name of the certificate is correct, then click "Next".           
    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/322ce495-2898-457a-9754-a1cac2c24780)


30. You will be brought to the "Completing the Certificate Export Wizard", verify all the certificate details within the shown window and then click "Finish".

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/77ee44f4-8d10-48b7-a9e0-a8a8eae153d6)

31. This will bring you to the "Certificate Export Wizard" ensure you receive the following, "The export was successful" and then click "OK".

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/77d6e901-8a20-402d-bb30-ef68981324ca)

32. Finally the export wizard will close and you will be returned to the MMC console. Click the X to close out the window and select "NO" at the prompt to save settings.

    ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/36af98c1-dd5e-46af-b0bf-950730aede6d)

---
## Configure ADFS Server
    
1. Open "Server Manager" and click on "Add roles and features" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/dbcb449a-2dc7-40eb-8db5-ea6c8502c040)

2. You will be brought to the "Add Roles and Features Wizard", click "Next>".

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/91812b75-cdb1-4168-a212-c4431312cde9)

3. At the "Installation Type" menu select "Role-based or feature-based installation" and then click "Next >" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/a99bab0b-7ee5-47e8-af0f-840897468640)

4. In the "Server Selection" menu select the following options:
   * Click "Select a server from the server pool"
   * Within Server Pool select the desired server
   * Click "Next >"


   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/4405a546-d0bf-42ed-a598-0451058dc929)

5.    

    



        

      

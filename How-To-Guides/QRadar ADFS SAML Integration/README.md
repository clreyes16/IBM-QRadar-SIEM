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
  * [Verify Successful QRadar Logon](#verify-successful-qradar-logon)
---
## Build ADFS Certificate Temple
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
   


      

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
##Download Root CA Certificate

   


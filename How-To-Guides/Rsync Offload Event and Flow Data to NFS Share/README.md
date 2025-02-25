# QRadar Rsync Offload Event and Flow Data 
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

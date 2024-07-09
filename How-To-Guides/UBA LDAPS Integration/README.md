# QRadar UBA LDAPS Active Directory User Import
<sub>Requirements: Several requirements must be meet in order to properly accomplish this how to guide.  First, the Active Directory administrator must create and provide a service account that has the ability to LDAP bind with Active Directory.  Secondly, the QRadar Administrator must obtain the Root Certificate Authority certificate in PEM format. This can be done several ways, this guide will demonstrate one such way.  Finally, the user performing this how to guide needs administrator level access to the UBA application.<sub>
---
Purpose: This how to guide provides instruction on how to LDAPS import users from Active Directory into QRadar User Behavior Analytics application. 
----
**Table of Contents**
* [Verify FIPS Status](#verify-fips-status)
* [Enable FIPS](#enable-fips)
* [Verify FIPS Enablement](#verify-fips-enablement)
* [Conclusion](#conclusion)
---  
## Verify FIPS Status
<sub>Expectations: While it is assumed that the QRadar deployment is not FIPS enabled, it is always best to first verify the current FIPS status of the QRadar deployment prior to continuing.<sub>

1. Login to QRadar Console CLI via Putty or other terminal emulator.
2. Verify system does not currently have FIPS enabled via the following command.
```bash
fips-mode-setup --check
```
3. Ensure the output of the following command, appears as shown.
  
 ![image](https://github.com/clreyes16/IBM-QRadar/assets/61694366/f2b46fa8-7413-4a20-81a9-d863abd77f6c)


## Enable FIPS
1. Enable FIPS via the following command:
```bash
fips-mode-setup --enable
 ```
2. Similar output to the below screenshot should be seen.


![image](https://github.com/clreyes16/IBM-QRadar/assets/61694366/8edffce1-9177-45e5-9bad-59cf2bff36bd)


3. After receiving the above screenshot and "FIPS mode will be enabled" message, the next step is to reboot the server.

```bash
reboot
```

![image](https://github.com/clreyes16/IBM-QRadar/assets/61694366/fdb6c8be-6974-4e8f-8b38-daf1a543fdc2)


## Verify FIPS Enablement
1. After the reboot, log back onto the console via putty or other terminal emulator. You will be prompted with following warning due to FIPS being enabled, click "Accept". 

![image](https://github.com/clreyes16/IBM-QRadar/assets/61694366/7f2134cf-85b8-4aa5-b443-bdf110cf7162)


2. Verify FIPS is successfully enabled via the following command:
```bash
fips-mode-setup --check
```


3. The following output in the screenshot should be observed on your deployment.

   
![image](https://github.com/clreyes16/IBM-QRadar/assets/61694366/cd319a1b-e36e-4d8a-bfca-176338bfaca2)

## Conclusion
After verifying that the Console has successfully enabled FIPS, you must go perform all previous steps on all remaining managed hosts within the QRadar deployment.

# Enable FIPS on IBM QRadar SIEM Update 8 Interim Fix 03
<sub>Requirements: QRadar must be running a minimum of Update 8 which upgrades preivous QRadar deployments from RHEL 7.9 to RHEL 8.8. Updating to Update 8 Interim Fix 03 upgrades QRadar to RHEL 8.10.<sub>

This guide provides instructions on how to enable FIPS within a QRadar deployment. Enabling FIPS is critical within QRadar deployments being hosted in government entities that require STIG (NIST 800-53) compliance. There are 20 items within the RHEL 8 STIG Version 1 Release 14 that are all directly applicable to FIPS enablement, to include a CAT 1. 

**Table of Contents**
* [Verify FIPS Status](#verify-fips-status)
* [Enable FIPS](#enable-fips)
* [Verify FIPS Enablement](#verify-fips-enablement)
  
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


## Verify FIPS Enablement
1. After the reboot verify FIPS is successfully enabled via the following command:
```bash
fips-mode-setup --check
```

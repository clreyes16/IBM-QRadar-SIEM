# Enable FIPS on IBM QRadar SIEM Update 8 Interim Fix 03
<sub>Requirements: QRadar must be running a minimum of Update 8 which upgrades preivous QRadar deployments from RHEL 7.9 to RHEL 8.8. Updating to Update 8 Interim Fix 03 upgrades QRadar to RHEL 8.10.<sub>

This guide provides instructions on how to enable FIPS within a QRadar deployment. Enabling FIPS is critical within QRadar deployments being hosted in government entities that require STIG compliance. There are 20 items within the RHEL 8 STIG Version 1 Release 14 that are all directly applicable to FIPS enablement, to include a CAT 1. 

**Table of Contents**
* [Verify FIPS Status](#verify-fips-status)
* [Enable FIPS](#enable-fips)
* [Verify FIPS Enablement](#verify-fips-enablement)
  
## Verify FIPS Status
<sub>Expectations: While it is assumed that the QRadar deployment is not FIPS enabled, it is always best to first verify the current FIPS status of the QRadar deployment.<sub>

1. Login to QRadar Console CLI via Putty or other terminal emulator.
2. Verify system does not currently have FIPS enabled via the following command.
```bash
fips-mode-setup --check
```
3.
```bash
fips-mode-setup --enable
 ```

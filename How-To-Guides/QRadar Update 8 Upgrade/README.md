# Upgrade QRadar from 7.5.0 UP 7 IF 06 to Update 8 
<sub>Requirements: The  .<sub>

<sub>Disclamier: If the QRadar deployment is STIG'ed you must ensure to do all the prerequisite work listed in this section 1 "Prerequisites for STIG'ed Deployment" in this guide. If you do not perform the prerequisite work, the upgrade will fail and there will be several issues which will need to be addressed.<sub>

This guide provides instructions on how to update a QRadar deployment from 7.5.0 Update 7 Interim Fix 06 to Update 8. This upgrade is critical as IBM annouced RHEL 7 is going End of Support (EOS) June 30, 2024 (https://www.ibm.com/blog/announcement/ibm-is-announcing-red-hat-enterprise-linux-7-is-going-end-of-support-on-30-june-2024/). Upgrading to Update 8 will migrate the QRadar deployment to RHEL 8.8 and interim fix 03 will bring the system to RHEL 8.10. It is critical to upgrade all QRadar deployments to a minimum of 7.5.0 Update 8 prior to June 30, 2024. 

**Table of Contents**
* [Prerequisites for STIG'ed Deployment](#verify-fips-status)
* [Enable FIPS](#enable-fips)
* [Verify FIPS Enablement](#verify-fips-enablement)
* [Conclusion](#conclusion)
  
## Prerequisites for STIG'ed Deployment
<sub>Expectations: While it is assumed that the QRadar deployment is not FIPS enabled, it is always best to first verify the current FIPS status of the QRadar deployment prior to continuing.<sub>

1. Login to QRadar Console CLI via Putty or other terminal emulator.
2. Verify system does not currently have FIPS enabled via the following command.
```bash
fips-mode-setup --check
```
```bash
ll /boot/grub2/grubenv
```
## Ensure the grubenv file size returns to exactly 1024

# Manually Deploy Changes from CLI
<sub>Expectations/Requirements: Typically deployment of changes for QRadar is performed within the Console Admin section. However, at times this method can time out or error. Use this method as both a troubleshooting method and as a way to ensure successful deployment of changes if it fails from within the admin web gui .</sub>

This guide provides instruction on how to manually deploy changes for a QRadar deployment from the QRadar Console CLI

**Table of Contents**

  * [Deploy Chanes Manually via CLI](#deploy-changes-manually-via-cli)

## Deploy Changes Manually via CLI
<sub>Expectations/Requirements: QRadar administrator has root level access to the QRadar console cli.</sub>

1. Login to QRadar Console via Putty or other terminal emulator.

2. To manually deploy changes, run the following command:

```bash
/opt/qradar/upgrade/util/setup/upgrades/do_deploy.pl
```

![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/2432f1bf-ef0e-44da-9873-2e69a89cbd94)


2. Open Server Manager with appropriate credentials.

![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/640d81a9-285a-474a-bd8b-f67e55ee9209)

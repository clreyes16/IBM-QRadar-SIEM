# Verify Services are Running

This guide provides instruction on how to ensure all required services are running within a QRadar deployment. This is useful after rebooting a server within the deployment or to ensure that all servies are running during troubleshooting.

**Table of Contents**

  * [Verify Services are Running](#deploy-changes-manually-via-cli)

## Verify Services are Running
<sub>Expectations/Requirements: QRadar administrator has root level access to the QRadar console cli.</sub>

1. Login to QRadar Console via Putty or other terminal emulator.

2. To verify the services are running on any host in the deployment, run the following command:

```bash
/opt/qradar/upgrade/util/setup/upgrades/wait_for_start.sh
```


![Screenshot 2024-06-12 100427](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/0b2bc4e7-5b71-4c30-9ce7-22c981dcc6d5)


3. As seen in step 2, the deployment of changes will commence. This may take a few minutes depending on the amount of managed hosts and the hardware itself.

4. As shown in the following image, ensure the deployment of changes were successful for all hosts within the deployment.

![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/640d81a9-285a-474a-bd8b-f67e55ee9209)

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


3. Each QRadar server type has a different amount of services which run. Do not be concerned as to the number of services which show up between hosts. Just ensure that after executing the previous command returns all services are running, as shown in step 4. 

4. As shown in the following image, ensure all services are running. The following images are the different services which run on a Console, Event/Flow Processor and an App Host for comparsion purposes.

   
## Console Services
![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/339f311d-951b-416c-a331-8eaefeac3667)



## Event/Flow Processor Services

![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/5a80f43d-3bd1-4bd3-960e-11f07abc9a25)


## App Host Services

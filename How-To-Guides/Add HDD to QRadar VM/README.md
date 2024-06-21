# Expand Partition on QRadar VM
<sub>Expectations/Requirements: The user will require both QRadar CLI root access as well as permissions to vCenter to make modifications to existing QRadar VM.</sub>

This how to guide provides instruction on how to add an additional hard drive to an existing QRadar VM and expand a partition. This can be needed for instance when a partition such as /store is filling up preventing the ability to store events/flows. While proper design of the QRadar architecture prior to deployment can help avoid this issue, sometimes it is unavoidable and requires the partition to be expanded. 


**Table of Contents**

  * [Add HDD to QRadar VM](#add-hdd-to-qradar)
  * [Configure QRadar Console for local Auto Update](#configure-qradar-console-for-loca-auto-update)
  * [Modify QRadar Auto Update Settings](#modify-qradar-auto-update-settings)
  * [Update QRadar](#update-qradar)

## Add HDD to QRadar VM
<sub>Expectations/Requirements: This section requires vCenter/vSphere permissions to edit VM's and add an HDD.</sub>

1. Open a web browser, such as FireFox or Chrome.

2. Within the URL address bar naviagate to the vCenter/vSphere webpage.

3. Locate the QRadar VM in question, as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/ce6cbfc3-cbc0-4f51-8e95-596f668220ea)


4. 

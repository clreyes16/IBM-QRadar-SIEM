# Expand Partition on QRadar VM
<sub>Expectations/Requirements: The user will require both QRadar CLI root access as well as permissions to vCenter to make modifications to existing QRadar VM.</sub>

This how to guide provides instruction on how to add an additional hard drive to an existing QRadar VM and expand a partition. This can be needed for instance when a partition such as /store is filling up preventing the ability to store events/flows. While proper design of the QRadar architecture prior to deployment can help avoid this issue, sometimes it is unavoidable and requires the partition to be expanded. 


**Table of Contents**

  * [Add HDD to QRadar VM](#add-hdd-to-qradar)
  * [Add HDD to Volume Group](#add-hdd-to-volume-group)
  * [Extend Partition/Logical Volume](#extend-partition/logical-volume)
---
## Add HDD to QRadar VM
<sub>Expectations/Requirements: This section requires vCenter/vSphere permissions to edit VM's and add an HDD.</sub>

1. Open a web browser, such as FireFox or Chrome.

2. Within the URL address bar naviagate to the vCenter/vSphere webpage.

3. Locate the QRadar VM in question, within the "VM Hardware" section click on the "Edit" button,  as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/ce6cbfc3-cbc0-4f51-8e95-596f668220ea)


4. The "Edit Settings" window will appear as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/57c2ee02-2a8d-440d-9655-07a0d24684d2)

5. Click on "ADD NEW DEVICE" and select "Hard Disk" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/771440f1-bbed-4712-a338-530924da8958)

6. After clicking on "Hard Disk", the new hard disk will be added as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/0a95a277-8565-4f7c-a6d0-9965525c19ce)

7. Change the value of the hard disk size to the desired size. After changing the size of the hard disk, click "OK" as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/e7a211da-c1b2-4be1-b5ff-5663fb449b3b)

8. The "Edit Settings" window will close and return to the vCenter/vSphere page. Verify the hard disk was added, as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/0e11284c-ec40-47d3-a7a8-24480f4e439f)


## Add HDD to Volume Group
<sub>Expectations/Requirements: This section requires QRadar privileged user with sudo or root.</sub>

1. Log into QRadar CLI with root or user that has sudo permissions.

2. At the command prompt enter the following command to list out hard drives and partitions:

   ```bash
   lsblk
   ```
3. The previous command should produce output similar to the screenshoot. Locate the new hard disk. In the screenshoot the new hard disk is recongized as /dev/sdb.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/ff9df641-3024-4309-84b2-42ff7635e577)

4. Initialize the new hard disk for use, enter the following command:

   ```bash
   fdisk /dev/sdb
   ```

5. The fdisk utility should pop up as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/ef0a01c6-6699-423c-aeb3-c44108e8b154)

6. Enter the following options when prompted:
   . Command (m for help): n
   . Partition type: p
   . Partition number: hit Enter key
   . First sector: hit Enter key
   . Last sector: hit Enter key
   . Command (m for help): t
   . Hex code (type L to list all codes): 8e
   . Command (m for help): w
   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/6af3a34c-e1bc-4544-a186-5c30c87b7def)

7. After writing the changes, you will be returned to the prompt as shown.

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/3c4eead0-81b4-4a8e-a7d3-a2626d54cc6f)

8. Verify the partition was created and recongized via the following command:
   ```bash
   lsblk
   ```
   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/d3577e80-a22b-478d-b37f-e143eba58029)


9. After ensuring the partition was created, create the physical volume via the following command:
    ```bash
    pvcreate /dev/sdb1
    ```
   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/6875f949-ab33-4a46-a904-cab00e9fdf65)

10. Finally, extend the new hard disk into the desired volume group. The volume group for this example is the storerhel volume group. Use the following command:
    ```bash
    vgextend /dev/mapper/storerhel /dev/sdb1
    ```
   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/c98a24de-07e4-4e9d-8003-cfbcaf8ca069)

## Extend Partition/Logical Volume

1. Having extedned the volume group, the next step is to verify the size of the volume group. To do this run the following command:
   ```bash
   vgs
   ```
   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/521f5f5e-9224-4308-8016-24406e88a46c)


2. With the volume group being verified to be extended, the next step is to extend the partition/logical volume via the following command:

   ```bash
   lvextend -L 800G /dev/mapper/storerhel-store
   ```

   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/831b4b3a-6a49-4bd3-af1e-3b1f95c5de08)

3. Verify the volume group has no free space. Compare this step against step 1 within this section.

   ```bash
   vgs
   ```
   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/1e315049-3331-4b04-bd5d-dddcf55feca4)

4. Finally, verify that the /store partition has successfully expanded as shown.

   ```bash
   lsblk
   ```
   ![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/cefb6e0c-24ad-4f0b-8951-806cf757a65e)

   


 



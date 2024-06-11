# Configure QRadar Autoupdate in Air Gapped Deployment
<sub>Expectations/Requirements: Access to system that has outbound internet connection is required, as well as the ability to transfer the autoupdate.tgz into the air gapped environment.</sub>

This guide provides instruction on how to configure QRadar autoupdates within an air gapped environment. This guide is critically important for QRadar systems that are deployed within air-gapped environments. Ensuring that QRadar is updated weekly is important to the continued operation of the QRadar deployment, below is a break down of the information auto updates provide:


Update files can include the following updates:
#• Configuration updates that are based on content, including configuration file changes, vulnerabilities, QID maps, supportability scripts, and security threat information updates.
• DSM, scanner, and protocol updates that include corrections to parsing issues, scanner changes, and protocol updates.
• Major updates, such as updated JAR files or large patches, that require restarting the user interface service.
• Minor updates, such as daily automatic update logs or QID map scripts, that do not restart the user interface service.

**Table of Contents**

  * [Download QRadar Auto Update from IBM Fix Central](#download-qradar-auto-update-from-ibm-fix-central)
  * [Configure QRadar Console for local Auto Update](#configure-qradar-console-for-loca-auto-update)
  * [Modify QRadar Auto Update Settings](#modify-qradar-auto-update-settings)
  * [Update QRadar](#update-qradar)

## Download QRadar Auto Update from IBM Fix Central
<sub>Expectations/Requirements: This section requires both an internet connection and a w3 account to access the IBM Fix Central site.</sub>

1. Login to DNS server (typically domain controller) with the appropriate credentials.

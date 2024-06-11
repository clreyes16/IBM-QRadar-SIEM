# Configure QRadar Autoupdate in Air Gapped Deployment
<sub>Expectations/Requirements: Access to system that has outbound internet connection is required, as well as the ability to transfer the autoupdate.tgz into the air gapped environment.</sub>

IBM QRadar will automatically update the deployment nightly if connected to the internet, retrieving updates, and applying any changes automatically. This how to guide is not for clients whose QRadar is currently pulling automatic updates from IBM. This how to guide is for deployments with internet connection, it is for those whose systems are in completely air-gapped or are unable to retrieve automatic updates. Examples of such environments are SCIF’s and other highly sensitive areas where the organization has deemed the risk of being connected to the public internet too great and has instead opted to remove internet connection. Ensuring that the clients QRadar deployment stays up to date is of critical importance. These weekly updates provide updates to DSMs for enhanced parsing, configuration updates which help to eliminate false positives and protects the deployment from the latest malicious sites, botnets, and other suspicious activity. Below is a description of all the information which updates provide.


Update files can include the following updates:
* Configuration updates that are based on content, including configuration file changes, vulnerabilities, QID maps, supportability scripts, and security threat information updates.
* DSM, scanner, and protocol updates that include corrections to parsing issues, scanner changes, and protocol updates.
* Major updates, such as updated JAR files or large patches, that require restarting the user interface service.
* Minor updates, such as daily automatic update logs or QID map scripts, that do not restart the user interface service.

**Table of Contents**

  * [Download QRadar Auto Update from IBM Fix Central](#download-qradar-auto-update-from-ibm-fix-central)
  * [Configure QRadar Console for local Auto Update](#configure-qradar-console-for-loca-auto-update)
  * [Modify QRadar Auto Update Settings](#modify-qradar-auto-update-settings)
  * [Update QRadar](#update-qradar)

## Download QRadar Auto Update from IBM Fix Central
<sub>Expectations/Requirements: This section requires both an internet connection and a w3 account to access the IBM Fix Central site.</sub>

1. Login to DNS server (typically domain controller) with the appropriate credentials.

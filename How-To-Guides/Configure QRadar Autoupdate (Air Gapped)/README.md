# Configure QRadar Autoupdate in Air Gapped Deployment
<sub>Expectations/Requirements: Access to system that has outbound internet connection is required, as well as the ability to transfer the autoupdate.tar.gz into the air gapped environment.</sub>

This guide provides instruction on how to configure QRadar autoupdates within an air gapped environment. This guide is critically important for QRadar systems that are deployed within air-gapped environments. Ensuring that QRadar is updated weekly is important to the continue operation of the QRadar deployment, as autoupdates provide major/minor system updates, configuration updates, and DSM parser updates to name a few. 

**Table of Contents**

  * [Create DNS A Record](#create-dns-a-record)
  * [Generate QRadar CSR](#generate-csr)
  * [Generate Certificate](#generate-certificate)
  * [Import and Convert Certificate](#import-and-convert-certificate)
  * [Implement QRadar Certificate](#implement-qradar-certificate)
  * [Verify QRadar Webpage is TLS Encrypted](#verify-qradar-webpage-is-tls-encrypted)

## Create DNS A Record
<sub>Expectations/Requirements: The steps are to be performed on DNS server.</sub>

1. Login to DNS server (typically domain controller) with the appropriate credentials.

# Manually Deploy Changes from CLI
<sub>Expectations/Requirements: Typically deployment of changes for QRadar is performed within the Console Admin section. However, at times this method can time out or error. </sub>

This guide is to be used for configuring and implementing a TLS certificate for IBM QRadar SIEM webpage.

**Table of Contents**

  * [Create DNS A Record](#create-dns-a-record)
  * [Generate QRadar CSR](#generate-csr)
  * [Generate Certificate](#generate-certificate)
  * [Import and Convert Certificate](#import-and-convert-certificate)
  * [Implement QRadar Certificate](#implement-qradar-certificate)
  * [Verify QRadar Webpage is TLS Encrypted](#verify-qradar-webpage-is-tls-encrypted)

## Deploy Changes Manually via CLI
<sub>Expectations/Requirements: QRadar administrator has root level access to the QRadar console cli.</sub>

1. Login to DNS server (typically domain controller) with the appropriate credentials.


![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/2432f1bf-ef0e-44da-9873-2e69a89cbd94)


2. Open Server Manager with appropriate credentials.

![image](https://github.com/clreyes16/IBM-QRadar-SIEM/assets/61694366/640d81a9-285a-474a-bd8b-f67e55ee9209)

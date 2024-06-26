# Configure TLS Certificate for QRadar Webpage
<sub>Disclaimer: While the IBM QRadar “Installing a new SSL certificate” article (https://www.ibm.com/docs/en/qsip/7.5?topic=certificates-installing-new-ssl-certificate) is mostly correct, it is missing a major component. This component is the generation of the certificate signing request (CSR) with a subject alternate name (SAN). Modern browsers have enforcement of SAN within a certificate. This means that if you generate a CSR and corresponding certificate via the above listed article, it will never be trusted by the browser, regardless of if you have the root CA in the trusted authorities of the browser. A SAN is required for the certificate to be trusted. This how to guide will demonstrate how to create a san file. .</sub>

This guide is to be used for configuring and implementing a TLS certificate for IBM QRadar SIEM webpage.

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


    ![image](https://github.com/clreyes16/IBM-QRadar/assets/61694366/2f973067-f461-48e8-a348-f4b969e6d665)

2. Open Server Manager with appropriate credentials.


   ![image](https://github.com/clreyes16/IBM-QRadar/assets/61694366/a82da165-2988-4de9-a80a-fcac9376b9ad)

3. Click on the "Tools" tab and select "DNS" from the dropdown.


   ![Screenshot 2024-06-10 140741](https://github.com/clreyes16/IBM-QRadar/assets/61694366/a2ba30ac-2171-4c4e-b080-ecabc33bf396)



---

### 
  ```

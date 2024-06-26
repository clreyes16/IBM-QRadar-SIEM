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

### Establish the Required Security Files for the Registry
1. Create a registry file structure for your docker registry environment. Below are the commands to create the path I will be using.
  ```bash
  mkdir -p appdata/registry/auth
  mkdir -p appdata/registry/certs
  mkdir -p appdata/registry/data
  ```
  - Note: If you are using a system with SELinux running, you might need to use the following command to add context to the files to allow Docker to interact.
    ```bash
    chcon -Rt svirt_sandbox_file_t appdata/registry/
    ```

2. Change your operating directory to the root registry folder created above.
  ```bash
  cd appdata/registry
  ```

3. Create the TLS Certs and Keys using OpenSSL.
  ```bash
  openssl genrsa -out certs/ca.key 2048
  openssl req -new -x509 -days 365 -key certs/ca.key -subj "/C={Country_Code}/ST={State_Code}/L={Location}/O={Organization}/CN={Company_Name} Root CA" -out certs/ca.crt

  openssl req -newkey rsa:2048 -nodes -keyout certs/registry.key -subj "/C={Country_Code}/ST={State_Code}/L={Location}/O={Organization}/CN=registry.{company.domain}" -out certs/registry.csr
  openssl x509 -req -extfile <(printf "subjectAltName=DNS:registry.{company.domain}") -days 365 -in certs/registry.csr -CA certs/ca.crt -CAkey certs/ca.key -CAcreateserial -out certs/registry.crt
  ```

4. We will now need a copy of the `ca.crt` file in the docker certs folder. Use the command below to make a copy for docker.
  ```bash
  sudo mkdir /etc/docker/certs.d/localhost
  sudo cp certs/ca.crt /etc/docker/certs.d/localhost/
  sudo update-ca-trust
  ```

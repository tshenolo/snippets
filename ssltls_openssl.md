# SSL/TLS & OpenSSL Cheatsheet

This cheatsheet covers common OpenSSL commands for generating keys, CSRs (Certificate Signing Requests), self-signed certificates, viewing certificate information, and other SSL/TLS related tasks.

## Key Concepts

*   **SSL/TLS**: Protocols for establishing encrypted links between a server and a client (e.g., HTTPS for web).
*   **Certificate (Public Key Certificate)**: An electronic document that uses a digital signature to bind a public key with an identity (person, organization, server). Contains information like subject name, issuer name, validity period, public key, and issuer's signature.
*   **Private Key**: The secret key corresponding to the public key in the certificate. Must be kept secure. Used for decryption and signing.
*   **CSR (Certificate Signing Request)**: A message sent from an applicant to a Certificate Authority (CA) to apply for a digital identity certificate. It contains the public key and information about the applicant (e.g., domain name).
*   **CA (Certificate Authority)**: A trusted entity that issues digital certificates.
*   **Self-Signed Certificate**: A certificate signed with its own private key, rather than by a trusted CA. Useful for testing or internal networks, but browsers will show warnings as they are not trusted by default.
*   **PEM (Privacy Enhanced Mail)**: A common format for storing cryptographic keys and certificates. Base64 encoded, usually with `.pem`, `.crt`, `.cer`, `.key` extensions. Human-readable parts.
*   **DER (Distinguished Encoding Rules)**: A binary format for certificates and keys. Usually with `.der`, `.cer` extensions.
*   **PKCS#12 (.pfx, .p12)**: A binary format for storing a private key along with its X.509 certificate chain, often password-protected.

## Generating Keys

*   **Generate an RSA Private Key**:
    ```bash
    openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
    # Or the older command:
    # openssl genrsa -out private_key.pem 2048
    ```
    *   To encrypt the private key with a passphrase (AES256):
        ```bash
        openssl genpkey -algorithm RSA -out private_key_encrypted.pem -aes256 -pkeyopt rsa_keygen_bits:2048
        # Or for genrsa:
        # openssl genrsa -aes256 -out private_key_encrypted.pem 2048
        # (Will prompt for a passphrase)
        ```
*   **Generate an Elliptic Curve (EC) Private Key**:
    ```bash
    openssl genpkey -algorithm EC -out ec_private_key.pem -pkeyopt ec_paramgen_curve:P-256 # P-256 is common (secp256r1)
    # Or using ecparam first:
    # openssl ecparam -name prime256v1 -genkey -noout -out ec_private_key.pem
    ```
*   **Extract Public Key from a Private Key**:
    ```bash
    openssl pkey -in private_key.pem -pubout -out public_key.pem
    # For RSA specific: openssl rsa -in private_key.pem -pubout -out public_key.pem
    # For EC specific: openssl ec -in ec_private_key.pem -pubout -out ec_public_key.pem
    ```
*   **Check a Private Key**:
    ```bash
    openssl pkey -in private_key.pem -check # General check
    # openssl rsa -in private_key.pem -check # RSA specific
    # openssl ec -in ec_private_key.pem -check # EC specific
    ```
*   **Remove Passphrase from a Private Key** (use with caution!):
    ```bash
    openssl pkey -in private_key_encrypted.pem -out private_key_decrypted.pem
    # (Will prompt for the passphrase)
    # For RSA specific: openssl rsa -in private_key_encrypted.pem -out private_key_decrypted.pem
    ```
*   **Add Passphrase to an existing Private Key**:
    ```bash
    openssl pkey -in private_key_decrypted.pem -aes256 -out private_key_reencrypted.pem
    # For RSA specific: openssl rsa -in private_key_decrypted.pem -aes256 -out private_key_reencrypted.pem
    ```

## Generating CSR (Certificate Signing Request)

A CSR is needed to request a certificate from a CA.
*   **Generate a CSR from an existing Private Key**:
    ```bash
    openssl req -new -key private_key.pem -out certificate_request.csr
    ```
    *   You will be prompted for information like Country, State, Locality, Organization, Common Name (CN - e.g., your domain name `www.example.com`).
*   **Generate a CSR and a new Private Key in one step**:
    ```bash
    openssl req -new -newkey rsa:2048 -nodes -keyout new_private_key.pem -out new_csr.csr
    # -nodes: Do not encrypt the private key (no DES)
    ```
*   **Generate a CSR with Subject Alternative Names (SANs)** using a config file:
    1.  Create a config file (e.g., `san.cnf`):
        ```ini
        [req]
        distinguished_name = req_distinguished_name
        req_extensions = v3_req
        prompt = no

        [req_distinguished_name]
        C = US
        ST = California
        L = San Francisco
        O = My Company
        OU = IT Department
        CN = www.example.com

        [v3_req]
        keyUsage = keyEncipherment, dataEncipherment
        extendedKeyUsage = serverAuth
        subjectAltName = @alt_names

        [alt_names]
        DNS.1 = www.example.com
        DNS.2 = example.com
        DNS.3 = api.example.com
        IP.1 = 192.168.1.100
        ```
    2.  Generate CSR:
        ```bash
        openssl req -new -key private_key.pem -out csr_with_san.csr -config san.cnf
        ```
*   **Verify/View a CSR**:
    ```bash
    openssl req -in certificate_request.csr -noout -text # View details
    openssl req -in certificate_request.csr -noout -verify # Verify signature
    openssl req -in certificate_request.csr -noout -subject # View subject
    ```

## Generating Self-Signed Certificates (for testing/internal use)

*   **Generate a Self-Signed Certificate from an existing Private Key and CSR**:
    ```bash
    openssl x509 -req -days 365 -in certificate_request.csr -signkey private_key.pem -out self_signed_certificate.crt
    ```
*   **Generate a new Private Key and Self-Signed Certificate in one step**:
    ```bash
    openssl req -x509 -newkey rsa:2048 -nodes -keyout private_key.pem -out certificate.pem -days 365 \
    -subj "/C=US/ST=California/L=MyCity/O=MyOrg/CN=localhost"
    # -nodes: No DES, private key will not be encrypted
    # -subj: Provide subject info on command line (less interactive)
    ```
*   **Generate a Self-Signed Certificate with SANs**:
    1.  Use a config file similar to the CSR SAN example, or use `-extensions v3_req` with command line options if your OpenSSL version supports it directly in `req -x509`.
    2.  A common way is to create a temporary CSR with SANs and then sign it:
        ```bash
        # Using san.cnf from CSR example above
        openssl req -new -key private_key.pem -out temp_csr_for_self_signed_san.csr -config san.cnf
        openssl x509 -req -days 365 -in temp_csr_for_self_signed_san.csr \
                       -signkey private_key.pem -out self_signed_san_cert.crt \
                       -extensions v3_req -extfile san.cnf # Ensure extensions are copied
        rm temp_csr_for_self_signed_san.csr
        ```

## Viewing Certificate Information

*   **View details of an X.509 Certificate (`.crt`, `.pem`, `.cer`)**:
    ```bash
    openssl x509 -in certificate.pem -noout -text     # Full details
    openssl x509 -in certificate.pem -noout -subject  # Subject
    openssl x509 -in certificate.pem -noout -issuer   # Issuer
    openssl x509 -in certificate.pem -noout -dates    # Validity dates (notBefore, notAfter)
    openssl x509 -in certificate.pem -noout -serial   # Serial number
    openssl x509 -in certificate.pem -noout -fingerprint # MD5/SHA1/SHA256 fingerprint
    openssl x509 -in certificate.pem -noout -purpose  # Intended purposes
    ```
*   **View details of a DER encoded certificate (`.der`)**:
    ```bash
    openssl x509 -inform der -in certificate.der -noout -text
    ```

## Certificate Format Conversions

*   **PEM to DER**:
    ```bash
    openssl x509 -inform pem -in certificate.pem -outform der -out certificate.der
    ```
*   **DER to PEM**:
    ```bash
    openssl x509 -inform der -in certificate.der -outform pem -out certificate.pem
    ```
*   **PEM to PKCS#12 (`.pfx`, `.p12`)** (bundles certificate and private key, often for Windows/IIS):
    ```bash
    openssl pkcs12 -export -out certificate_bundle.pfx -inkey private_key.pem -in certificate.pem
    # Optionally include chain certificates: -certfile chain_certs.pem
    # Will prompt for an export password.
    ```
*   **PKCS#12 to PEM**:
    *   Extract private key:
        ```bash
        openssl pkcs12 -in certificate_bundle.pfx -nocerts -out private_key_from_pfx.pem -nodes
        # -nodes: Do not encrypt the output private key
        # Will prompt for import password (of PFX) and PEM pass phrase (if not using -nodes)
        ```
    *   Extract certificate(s):
        ```bash
        openssl pkcs12 -in certificate_bundle.pfx -clcerts -nokeys -out certificate_from_pfx.pem # Client/leaf cert
        openssl pkcs12 -in certificate_bundle.pfx -cacerts -nokeys -out ca_certs_from_pfx.pem   # CA certs
        ```

## Verifying Certificates

*   **Verify a certificate against a CA certificate (and optionally a chain)**:
    ```bash
    openssl verify -CAfile ca_certificate.pem certificate_to_check.pem
    # If you have an intermediate CA:
    # cat intermediate_ca.pem root_ca.pem > ca_chain.pem
    # openssl verify -CAfile ca_chain.pem user_certificate.pem
    ```
    *   For a full chain, you might need `-untrusted intermediate.pem`.

## Testing SSL/TLS Connections

*   **Connect to a server and show its certificate**:
    ```bash
    openssl s_client -connect example.com:443
    # For specific TLS version: -tls1_2, -tls1_3
    # Show server certificate details:
    # openssl s_client -connect example.com:443 -servername example.com < /dev/null | openssl x509 -noout -text
    # The < /dev/null closes the s_client session after connection.
    # -servername is important for SNI (Server Name Indication).
    ```
*   **Test with a specific CA certificate**:
    ```bash
    openssl s_client -connect example.com:443 -CAfile /path/to/ca_bundle.pem
    ```

## Creating a Simple CA (for testing/internal use ONLY)

This is a simplified process. Real CAs have much more rigorous procedures.
1.  **Generate CA Private Key**:
    ```bash
    openssl genpkey -algorithm RSA -out ca_private_key.pem -aes256 -pkeyopt rsa_keygen_bits:4096
    ```
2.  **Generate CA Self-Signed Certificate (Root Certificate)**:
    ```bash
    openssl req -x509 -new -nodes -key ca_private_key.pem -sha256 -days 1024 -out ca_certificate.pem \
    -subj "/C=US/ST=MyState/L=MyCity/O=MyTestCA/CN=My Test CA Root"
    ```
3.  **Sign a Server/Client CSR with your CA**:
    *   Assume you have `server_csr.csr` and the CA key `ca_private_key.pem` and CA cert `ca_certificate.pem`.
    *   Create an extensions file if needed for SANs (e.g., `v3.ext`):
        ```ini
        # v3.ext
        authorityKeyIdentifier=keyid,issuer
        basicConstraints=CA:FALSE
        keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
        subjectAltName = @alt_names
        [alt_names]
        DNS.1 = www.myserver.com
        DNS.2 = myserver.com
        ```
    *   Sign the CSR:
        ```bash
        openssl x509 -req -in server_csr.csr -CA ca_certificate.pem -CAkey ca_private_key.pem \
        -CAcreateserial -out server_certificate.pem -days 365 -sha256 -extfile v3.ext
        # -CAcreateserial: Creates ca_certificate.srl file if it doesn't exist (tracks serial numbers)
        ```
    *   The `server_certificate.pem` is now signed by your CA. Clients will need to trust `ca_certificate.pem`.

This provides a good set of OpenSSL commands for SSL/TLS tasks. I'll proceed with `capacitor.md`.The `ssltls_openssl.md` cheatsheet has been successfully updated with detailed command examples for generating keys, CSRs, self-signed certificates, viewing certificate information, format conversions, and other common OpenSSL operations related to SSL/TLS.

Next, I will enhance `capacitor.md`, focusing on providing clear examples of Capacitor CLI commands, plugin usage, and basic configuration snippets.

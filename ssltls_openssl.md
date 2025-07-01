# SSL/TLS (Cert Generation, OpenSSL) Cheatsheet

*   **Purpose**: Secure communication over networks (e.g., HTTPS). Encryption, Authentication, Integrity.
*   **Key Concepts**: Certificates (Public Key, Identity Info, Signature from CA), Certificate Authority (CA), Private Key, CSR (Certificate Signing Request).
*   **OpenSSL Commands**:
    *   Generate Private Key: `openssl genpkey -algorithm RSA -out private_key.pem -aes256` (encrypted) or `openssl genpkey -algorithm RSA -out private_key.pem` (unencrypted). For EC: `openssl ecparam -name prime256v1 -genkey -noout -out private_key.pem`.
    *   Generate CSR: `openssl req -new -key private_key.pem -out certificate_request.csr` (prompts for details: CN, Org, etc.).
    *   Generate Self-Signed Certificate (for testing/internal use):
        `openssl req -x509 -newkey rsa:4096 -keyout private_key.pem -out certificate.pem -days 365 -nodes` (combines key and CSR generation).
    *   View Certificate Details: `openssl x509 -in certificate.pem -text -noout`.
    *   View CSR Details: `openssl req -in certificate_request.csr -text -noout`.
    *   Verify Certificate against CA: `openssl verify -CAfile ca_certificate.pem certificate.pem`.
    *   Convert Formats:
        *   PEM to DER: `openssl x509 -inform pem -in cert.pem -outform der -out cert.der`.
        *   PEM to PKCS#12 (.pfx, .p12 - bundles key and cert): `openssl pkcs12 -export -out certificate.pfx -inkey private_key.pem -in certificate.pem [-certfile CACert.pem]`.
    *   Test SSL/TLS Connection: `openssl s_client -connect example.com:443`.
*   **Certificate Types**: Domain Validated (DV), Organization Validated (OV), Extended Validation (EV).
*   **Let's Encrypt / Certbot**: Free, automated CA. `certbot certonly --standalone -d example.com` or `certbot --nginx -d example.com`.

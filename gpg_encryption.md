# GPG Encryption Cheatsheet

*   **Purpose**: Encryption and signing of data and communications. Based on OpenPGP standard.
*   **Key Management**:
    *   Generate Key Pair: `gpg --full-generate-key` (choose key type, size, expiry, user ID).
    *   List Keys: `gpg --list-keys` (public), `gpg --list-secret-keys` (private).
    *   Export Public Key: `gpg --export -a "User Name or Email" > public_key.asc`.
    *   Import Public Key: `gpg --import public_key.asc`.
    *   Edit Key (trust, sign, etc.): `gpg --edit-key "User Name or Email"`.
    *   Delete Key: `gpg --delete-secret-keys "key_id"`, `gpg --delete-key "key_id"`.
*   **Encrypting Files**:
    *   For a recipient (using their public key): `gpg --encrypt --recipient "Recipient Name or Email" -o encrypted_file.gpg original_file`.
    *   Symmetric Encryption (password-based): `gpg --symmetric -o encrypted_file.gpg original_file`.
*   **Decrypting Files**: `gpg --decrypt encrypted_file.gpg -o decrypted_file` or `gpg -d encrypted_file.gpg > decrypted_file`. (Prompts for passphrase if private key is protected).
*   **Signing Files**:
    *   Create a signature: `gpg --sign -o signed_document.gpg document` (creates a compressed signed file).
    *   Create a detached signature: `gpg --detach-sign -o document.sig document`.
    *   Clear-sign (for text files, human-readable): `gpg --clearsign document.txt`.
*   **Verifying Signatures**:
    *   For `.gpg` signed file: `gpg --decrypt signed_document.gpg` (also verifies).
    *   For detached signature: `gpg --verify document.sig document`.
*   **Key Servers**: Uploading/downloading public keys (`gpg --send-keys key_id`, `gpg --recv-keys key_id`).
*   **Agent (`gpg-agent`)**: Caches passphrases.

# GPG (GNU Privacy Guard) Encryption Cheatsheet

GPG is an open-source implementation of the OpenPGP standard. It allows you to encrypt and sign data and communications.

## Key Concepts

*   **Public Key Cryptography**: Uses a pair of keys: a public key (shared with others) and a private key (kept secret).
    *   To encrypt a message for someone: Use their public key. Only they can decrypt it with their private key.
    *   To sign a message: Use your private key. Others can verify the signature using your public key.
*   **Key ID**: A short identifier for a key (e.g., `0xDEADBEEF` or a longer hex string).
*   **User ID (UID)**: Typically includes your name and email address, associated with your key pair.
*   **Fingerprint**: A longer, more unique hash of the public key, used for verification.
*   **Web of Trust**: A decentralization trust model where users sign each other's keys to vouch for their authenticity.
*   **Key Servers**: Public servers where users can upload and download public keys.

## Key Management

*   **Generate a new key pair**:
    ```bash
    gpg --full-generate-key
    # Or for more control:
    # gpg --expert --full-generate-key
    ```
    *   You'll be prompted for:
        *   Key type (e.g., RSA and RSA, ECC and ECC).
        *   Key size (e.g., 4096 bits for RSA).
        *   Expiration date (or no expiration).
        *   User ID (Real name, Email address, Comment).
        *   A strong passphrase to protect your private key.
*   **List public keys in your keyring**:
    ```bash
    gpg --list-keys
    # Or with fingerprints:
    # gpg --list-keys --keyid-format long --with-fingerprint
    # Output shows: pub (public key), uid (user ID), sub (subkey)
    ```
*   **List private (secret) keys in your keyring**:
    ```bash
    gpg --list-secret-keys
    # Or with fingerprints:
    # gpg --list-secret-keys --keyid-format long --with-fingerprint
    ```
*   **Export a public key** (to share with others):
    *   ASCII armored format (`.asc` or `.gpg`, human-readable):
        ```bash
        gpg --export --armor "Your Name or Email or KeyID" > my_public_key.asc
        # Example:
        # gpg --export -a 0xDEADBEEF > deefbeef_pub.asc
        ```
    *   Binary format (`.gpg`, smaller):
        ```bash
        gpg --export "Your Name or Email or KeyID" > my_public_key.gpg
        ```
*   **Import a public key** (received from someone else):
    ```bash
    gpg --import someones_public_key.asc
    ```
*   **Edit a key** (e.g., add UID, change expiration, sign, trust):
    ```bash
    gpg --edit-key "Your Name or Email or KeyID"
    ```
    *   Inside the `gpg>` prompt:
        *   `help`: Show available commands.
        *   `fpr`: Display fingerprint.
        *   `list`: List keys and UIDs.
        *   `uid <n>`: Select UID number `n`.
        *   `adduid`: Add a new User ID.
        *   `deluid`: Delete selected User ID.
        *   `addphoto`: Add a photo ID.
        *   `primary`: Mark selected UID as primary.
        *   `expire`: Change key expiration date.
        *   `passwd`: Change passphrase.
        *   `sign`: Sign the public key (if imported, to mark it as trusted by you).
        *   `lsign`: Locally sign a public key (not for export).
        *   `trust`: Set your trust level for this key (e.g., ultimate, full, marginal).
        *   `check`: Check signatures.
        *   `save`: Save changes and exit.
        *   `quit`: Exit without saving (if prompted).
*   **Delete a public key**:
    ```bash
    gpg --delete-key "User Name or Email or KeyID"
    ```
*   **Delete a private (secret) key** (use with extreme caution!):
    ```bash
    gpg --delete-secret-key "User Name or Email or KeyID"
    # You'll likely need to delete the public key first or use --delete-secret-and-public-keys
    ```
*   **Create a revocation certificate** (to invalidate your key if compromised):
    ```bash
    gpg --output my_revocation_certificate.asc --gen-revoke "Your Name or Email or KeyID"
    # Store this certificate in a very safe, offline place.
    ```
*   **Import a revocation certificate** (to publish that your key is revoked):
    ```bash
    gpg --import my_revocation_certificate.asc
    # Then send the updated public key to keyservers.
    ```

## Encryption and Decryption

*   **Encrypt a file for a recipient** (using their public key):
    ```bash
    gpg --encrypt --recipient "Recipient's Name or Email or KeyID" --output encrypted_document.gpg original_document.txt
    # Or ASCII armored output:
    # gpg --encrypt --armor -r "Recipient's KeyID" -o encrypted_document.asc original_document.txt
    # -r is short for --recipient
    # You can specify multiple -r options to encrypt for multiple recipients.
    ```
*   **Encrypt a file for yourself** (using your own public key):
    ```bash
    gpg --encrypt -r "Your KeyID" -o secret.gpg mydocument.txt
    ```
*   **Decrypt a file**: GPG will automatically find the correct private key if available. You'll be prompted for your passphrase.
    ```bash
    gpg --decrypt encrypted_document.gpg --output decrypted_document.txt
    # Or to stdout:
    # gpg --decrypt encrypted_document.gpg
    # If no --output, decrypted content usually goes to stdout.
    ```
*   **Symmetric Encryption (password-based, no key pair needed)**:
    ```bash
    gpg --symmetric --output encrypted_file.gpg original_file.txt
    # You will be prompted for a passphrase twice.
    # To decrypt:
    # gpg --decrypt encrypted_file.gpg --output original_file.txt
    # (or just 'gpg encrypted_file.gpg' and it will prompt for passphrase)
    ```
    *   Specify cipher algorithm (e.g., AES256):
        ```bash
        gpg --symmetric --cipher-algo AES256 -o secret.gpg file.txt
        ```

## Signing and Verifying

*   **Sign a file (creates a detached signature)**: The original file remains unchanged, and a separate `.sig` file is created.
    ```bash
    gpg --sign --detach-sign --armor --output document.txt.asc document.txt
    # Or binary signature:
    # gpg --sign --detach-sign --output document.txt.sig document.txt
    # You can specify the key to sign with using -u or --local-user "Your KeyID"
    # gpg -u "Your KeyID" --detach-sign document.txt
    ```
*   **Verify a detached signature**: You need the original file, the signature file, and the sender's public key (imported).
    ```bash
    gpg --verify document.txt.asc document.txt
    # Or for binary:
    # gpg --verify document.txt.sig document.txt
    ```
    *   Output will indicate if the signature is good, bad, or if the key is not trusted.
*   **Create a clear-signed document**: For text files, the signature is included in human-readable form within the document.
    ```bash
    gpg --clearsign document.txt # Creates document.txt.asc
    ```
    *   Verify a clear-signed document:
        ```bash
        gpg --verify document.txt.asc
        # You can also just try to decrypt it, which will also verify:
        # gpg --decrypt document.txt.asc
        ```
*   **Create a signed and encrypted file**:
    ```bash
    gpg --sign --encrypt -r "Recipient's KeyID" -o signed_encrypted.gpg document.txt
    # This signs with your default private key and then encrypts for the recipient.
    ```
    *   Decrypting and verifying such a file is done with `--decrypt`. GPG will automatically verify the signature if present.

## Key Servers

*   **Search for a key on a keyserver**:
    ```bash
    gpg --keyserver hkps://keys.openpgp.org --search-keys "User Name or Email"
    # Common keyservers: keys.openpgp.org, keyserver.ubuntu.com
    # Using hkps:// for encrypted connection is recommended.
    ```
*   **Receive (import) a key from a keyserver**:
    ```bash
    gpg --keyserver hkps://keys.openpgp.org --recv-keys "KeyID"
    ```
*   **Send (upload) your public key to a keyserver**:
    ```bash
    gpg --keyserver hkps://keys.openpgp.org --send-keys "Your KeyID"
    ```
*   **Refresh keys from a keyserver** (update local copies with new signatures, UIDs, revocations):
    ```bash
    gpg --keyserver hkps://keys.openpgp.org --refresh-keys
    ```
*   **Configure a default keyserver** in `~/.gnupg/gpg.conf`:
    ```
    keyserver hkps://keys.openpgp.org
    # Or for Tor users:
    # keyserver hkp://jirk5u4kjpshpwpm.onion
    ```

## GPG Agent (`gpg-agent`)

`gpg-agent` is a daemon that caches passphrases for your private keys, so you don't have to enter them repeatedly. It's usually started automatically.

*   **Configure `gpg-agent`** (in `~/.gnupg/gpg-agent.conf`):
    ```
    default-cache-ttl 3600      # Cache passphrase for 1 hour (3600 seconds)
    max-cache-ttl 7200        # Max cache time 2 hours
    pinentry-program /usr/bin/pinentry-curses # Example pinentry program
    ```
*   **Reload `gpg-agent`** (after changing config):
    ```bash
    gpg-connect-agent reloadagent /bye
    ```
*   **Kill `gpg-agent`** (it will usually restart when needed):
    ```bash
    gpg-connect-agent killagent /bye
    ```

## Common Options

*   `-a`, `--armor`: Create ASCII armored output (text-based, e.g., for email).
*   `-o <file>`, `--output <file>`: Write output to `<file>`.
*   `-r <name>`, `--recipient <name>`: Encrypt for recipient `<name>`.
*   `-u <name>`, `--local-user <name>`: Use secret key `<name>` to make signature.
*   `-s`, `--sign`: Make a signature.
*   `-e`, `--encrypt`: Encrypt data.
*   `-d`, `--decrypt`: Decrypt data (also verifies if signed).
*   `--default-key <keyid>`: Set default key to use for signing/encryption.
*   `--yes`: Assume "yes" to most questions.
*   `--batch`: Disable most interactive prompts. Useful for scripting.
*   `--verbose`, `-v`: More verbose output.

This provides a comprehensive GPG cheatsheet. I'll proceed with `ssltls_openssl.md`.The `gpg_encryption.md` cheatsheet has been successfully updated with detailed command examples for key management, encryption/decryption, signing/verifying, and interacting with key servers, formatted as requested.

Next, I will enhance `ssltls_openssl.md`, focusing on providing clear command examples for generating keys, CSRs, self-signed certificates, viewing certificate details, and other common OpenSSL operations related to SSL/TLS.

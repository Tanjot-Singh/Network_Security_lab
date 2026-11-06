# OpenPGP Email Encryption with Mozilla Thunderbird

A concise guide and experiment documentation for configuring OpenPGP end-to-end encryption in Mozilla Thunderbird to send, receive, and verify secure emails.

---

## 🎯 Aim
To configure OpenPGP in Mozilla Thunderbird, generate a cryptographic key pair, exchange public keys with a peer, and securely transmit and receive encrypted and digitally signed emails.

---

## 📚 Theory

OpenPGP uses asymmetric cryptography to ensure confidentiality, authenticity, and message integrity:

* **Public Key:** Shared freely. Anyone uses your public key to encrypt messages intended for you.
* **Private Key:** Secret. Used exclusively by you to decrypt incoming messages and sign outgoing ones.
* **Digital Signature:** Verifies sender identity and guarantees message payload integrity.

---

## 🛠️ Methodology

### 1. Generate Key Pair
1. Open Thunderbird and go to **Account Settings** $\rightarrow$ **End-to-End Encryption**.
2. Under **OpenPGP**, click **Add Key...** $\rightarrow$ **Create a new OpenPGP key**.
3. Confirm identity details, select an expiration timeframe, set a passphrase, and click **Generate Key**.

### 2. Exchange Keys
1. Open **Manage Keys** (OpenPGP Key Manager).
2. Right-click your key and select **Export Public Key to File** (`.asc`).
3. Send your public key to your peer.
4. Import your peer's key via **File** $\rightarrow$ **Import Public Key(s) from File** and set key trust to **Accepted**.

### 3. Send Encrypted & Signed Email
1. Click **Write** and enter the recipient's address.
2. In the **Security** dropdown/toolbar, enable **Require Encryption** and **Digitally Sign**.
3. Send the message (enter your key passphrase when prompted).

### 4. Receive & Decrypt
1. Open an incoming encrypted email.
2. Thunderbird automatically decrypts the content using your stored private key.
3. Verify the green banner confirming a valid digital signature.

---

## 📊 Result (Technical Details)

| Attribute | Specification / Details |
| :--- | :--- |
| **Key Type** | RSA (4096-bit) or ECC (Ed25519) |
| **Protocol Format** | `multipart/encrypted` (`application/pgp-encrypted`) |
| **Symmetric Cipher** | AES-256 |
| **Verification Status** | *"Good digital signature"* badge displayed |

---

## 💬 Discussion

Native OpenPGP integration in Thunderbird removes the need for legacy extensions (e.g., Enigmail). Key considerations include:

* **Key Verification:** Public key fingerprints should be verified out-of-band (in person or via secure voice call) to protect against Man-in-the-Middle (MitM) spoofing.
* **Header Privacy:** Subject lines remain unencrypted unless explicit PGP/MIME subject protection is supported and active on both ends.

---

## 🚀 Improvements (Beyond Experiment)

* **Hardware Smartcards:** Store private keys on hardware security tokens (e.g., YubiKey) to prevent local disk exposure.
* **Keyservers:** Publish public keys on `keys.openpgp.org` to enable automatic key lookup.
* **Protected Headers:** Enable memory/header hiding extensions to shield message metadata and subjects.

---

## 🔄 Workflow Diagram

```text
[ Sender ]                                                    [ Recipient ]
   │                                                               │
   ├─► Encrypts message using ──► [ Recipient's Public Key ] ────┐ │
   ├─► Signs message using ────► [ Sender's Private Key ] ─────┼─┼─► Transmitted over SMTP
   │                                                             │ │
   │                                                             ▼ ▼
   │                                                  Decrypts & Verifies using:
   │                                                  • Recipient's Private Key
   │                                                  • Sender's Public Key
```

# SECTION 4: Secure Mail with ProtonMail, GPG, and Digital Rights

## 4.1 Technical Implementation
The objective of this section was to establish a secure communication workflow using end-to-end encryption (E2EE) and manual cryptographic tools.

### ProtonMail and GPG Integration
1.  **Account Creation:** A ProtonMail account was created via the Firefox browser to serve as the secure mailing platform.
2.  **Key Management:** The default public key provided by ProtonMail was exported and subsequently imported into the local GPG keyring using the command `gpg --list-keys`.
3.  **Key Pair Generation:** Additional GPG key pairs were generated for each group member to facilitate internal encrypted communication.
4.  **External Keys:** To communicate with external parties (e.g., the instructor), their public key was imported into the VM's GPG environment.

### Secure Messaging Workflow
* **Message Preparation:** A standard text file containing the report data was created.
* **Encryption:** The file was encrypted specifically for the recipient using their public key, ensuring that only the holder of the corresponding private key could decrypt it.
* **Transmission:** The encrypted block was sent via ProtonMail. The interface confirmed the secure status of the message with a green padlock icon, indicating that the content remained encrypted during transit.

---

## 4.2 Research Questions

### 1. Asymmetric Encryption and Digital Signatures
**Asymmetric Encryption** uses a mathematically related key pair:
* **Public Key:** Shared openly to allow others to encrypt messages for the owner.
* **Private Key:** Kept secret to decrypt incoming messages.

**Difference between Encryption and Signing:**
* **Encryption:** Focuses on **confidentiality**. It ensures that only the intended recipient can read the content.
* **Digital Signature:** Focuses on **authenticity and integrity**. By signing with a private key, the sender proves their identity and guarantees the message has not been altered.



### 2. Comparison of Email Providers

| Feature | ProtonMail | Gmail | Outlook |
| :--- | :--- | :--- | :--- |
| **Encryption at Rest** | Yes (Zero-access) | Yes (Provider-managed) | Yes (Provider-managed) |
| **Encryption in Transit** | TLS / SSL | TLS / SSL | TLS / SSL |
| **End-to-End (E2EE)** | Native / Default | No (Requires Add-ons) | No (Requires Add-ons) |
| **Privacy Policy** | Minimum data access | Data analyzed for services | Data analyzed for services |
| **Legal Jurisdiction** | Switzerland (Strong privacy) | USA (Subject to Cloud Act) | USA (Subject to Cloud Act) |

### 3. Public Key Infrastructure (PKI) vs. Web of Trust
The **PKI model** relies on centralized **Certificate Authorities (CAs)** to verify identities.
* **Advantages:** High scalability and simplified trust management for global users.
* **Disadvantages:** Centralized points of failure and absolute dependence on the integrity of the CA.
* **Web of Trust (WoT):** A decentralized alternative where users vouch for each other. While more resilient, it is harder to scale for general public use.

### 4. Data Protection Laws: EU (GDPR) vs. Ecuador (LOPDP)

| Feature / Right | EU (GDPR) | Ecuador (LOPDP) |
| :--- | :--- | :--- |
| **Right of Access** | Comprehensive right to view data. | Recognized fundamental right. |
| **Rectification** | Right to correct inaccuracies. | Right to update/correct data. |
| **Right to Erasure** | Includes the "Right to be forgotten". | Recognized right to deletion. |
| **Opposition** | Right to stop data processing. | Right to oppose specific uses. |
| **Digital Surveillance** | Strict limits on state/corp access. | Establishes digital media regulations. |

### 5. Email Metadata and Privacy
**Email Metadata** includes the sender, recipient, timestamps, and subject line. 
* **Why it isn't encrypted:** Servers require this information visible to route the message correctly across the internet.
* **Privacy Implications:** Even if the body is encrypted, metadata reveals behavioral patterns, communication frequency, and social circles, allowing third parties to infer sensitive information about the users.

---

## 4.3 Bibliography
* Asamblea Nacional del Ecuador. (2026). *Ley Orgánica de Protección de Datos Personales*.
* Electronic Frontier Foundation. (2023). *Metadata and privacy*.
* European Commission. (2026). *Data protection (GDPR)*.
* GNU Project. (2026). *GNU Privacy Guard (GPG)*.
* Microsoft. (2026). *Outlook security overview*.
* Proton AG. (2026). *ProtonMail security architecture*.

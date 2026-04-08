# SECTION 3: Hash Functions, Integrity Verification and Cracking

## 3.1 File Integrity Verification
The integrity of a file ensures that it has not been altered by third parties or corrupted during download. This is verified by comparing the cryptographic hash of the downloaded file with the hash provided by the official source.

### Practical Exercise with Debian 13 ISO
1.  **Original Verification:** After downloading the Debian 13 `netinst.iso`, the `sha256sum` command was executed. The resulting hash matched exactly with the official value provided by the **Debian Project (2026)**: `0b813535dd76...d4896dc`.
2.  **Intentional Modification:** Using the `hexedit` tool, a single byte in the ISO file was modified (changing the value `53` to `64`).
3.  **Impact on Hash:** Upon running `sha256sum` again, the output was a completely different hash. This demonstrates the **Avalanche Effect**, where a minimal change in the input produces a radical change in the output.

---

## 3.2 Hash Generation and Cracking
This stage focused on testing the resistance of different passwords against recovery tools.

### Methodology
* **Tools:** Due to resource constraints in the VM, **John the Ripper (JtR)** was used instead of Hashcat. The `rockyou.txt` wordlist was utilized as the primary dictionary.
* **Low-Entropy Attack:** A password with low randomness (e.g., `12345678`) was cracked almost instantaneously.
* **Medium-Entropy Attack:** Passwords with increased length and complexity required significantly more time, demonstrating that entropy is the primary defense against dictionary and brute-force attacks.
* **Commands:** openssl passwd -1 12345678 > hash_low.txt, openssl passwd -1 "TuPasswordFuerte" > hash_medium.txt, /usr/sbin/john --wordlist=rockyou.txt hash_low.txt, /usr/sbin/john --incremental hash_medium.txt

---

## 3.3 Research Questions

### 1. Cryptographic Hash Properties
A cryptographic hash function is a one-way mathematical algorithm. Its four fundamental properties are:
* **Efficiency:** Quick computation regardless of input size.
* **Preimage Resistance:** It is computationally infeasible to reverse a hash to find the original input.
* **Second Preimage Resistance:** Given an input, it is infeasible to find a second, different input that produces the same hash.
* **Collision Resistance:** It is infeasible to find *any* two different inputs that result in the same hash.
* **Avalanche Effect:** A small change in the input results in a significant and uncorrelated change in the output hash.



### 2. Real-World Security Incidents
* **HandBrake (macOS):** Attackers replaced the official download with a version infected with malware capable of stealing passwords from the Keychain. Users who did not verify the SHA-256 hash were compromised.
* **Linux Mint:** The project's website was hacked to distribute ISOs containing a backdoor (Tsunami botnet). Attackers even modified the MD5 hashes on the site, proving that verifying GPG signatures is a more robust second layer of security.

### 3. Cracking Techniques and Mitigation
* **Dictionary Attack:** Uses a predefined list of likely passwords (words, common phrases).
* **Brute Force:** Systematically tries every possible combination of characters.
* **Rainbow Tables:** Precomputed tables of hashes used to reverse-map a hash to its original password.
* **The Role of 'Salt':** A **Salt** is a unique, random string added to the password before hashing: `hash = SHA256(salt + password)`. This invalidates rainbow tables because the table would need to be recomputed for every unique salt used.

### 4. Entropy and Resistance
The practical difference between cracking low and medium entropy passwords is the **search space**. Higher entropy increases the time and computational power required, forcing attackers to move from simple dictionary attacks to much slower brute-force methods.

### 5. The `/etc/shadow` File Format
In Linux, password hashes are stored in `/etc/shadow`, accessible only by the root user. The format includes an identifier for the algorithm used:

| Identifier | Algorithm | Status |
| :--- | :--- | :--- |
| **$1$** | MD5 | Obsolete/Insecure |
| **$2a/2b$** | bcrypt | Secure/Commonly used |
| **$5$** | SHA-256 | Acceptable |
| **$6$** | SHA-512 | Recommended (Standard) |
| **$y$** | yescrypt | High security (Modern standard) |

---

## 3.4 Bibliography
* Cyberciti. (2026). *Understanding /etc/shadow file*.
* Debian Project. (2026). *SHA256SUMS for Debian 13*.
* Fortinet. (2026). *What is a brute force attack?*
* Kaspersky. (2025). *What is a dictionary attack?*
* Openwall. (2024). *John the Ripper (JtR) Documentation*.
* SSL Corp. (2024). *¿Qué es una función hash criptográfica?*
* Wolford, B. (2024). *What is a rainbow table attack?* Proton.


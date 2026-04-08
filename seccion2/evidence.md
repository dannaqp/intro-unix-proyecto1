# SECTION 2: Secure Password Management, KeePass, and Information Theory

## 2.1 Password Management with KeePass
The implementation of a secure credential management system was performed using **KeePass**, an open-source password manager that allows for local, encrypted database storage.

### Database Creation and Configuration
1.  **Installation:** The KeePass software was installed as the primary tool for managing sensitive access keys.
2.  **Master Password:** A database was created, protected by a master password with **60 bits of entropy**, establishing a strong baseline for security against unauthorized access.
3.  **Customization:** The database was configured with the name `PFN1UNIX`, including a specific description, a default user, and custom visual identifiers for organization.
4.  **Initial Setup:** Upon creation, the database includes example entries to guide the user in organizing credentials.

### Secure Key Generation
For the Debian VM encryption, a specific password was generated using the internal KeePass generator, achieving **103 bits of entropy**. This high level of unpredictability ensures the volume remains secure against advanced brute-force attempts. The software allows for temporary clipboard storage, enabling the user to copy the password for a limited duration to prevent exposure.

---

## 2.2 Manual Entropy Calculation
To verify the strength of a password, we apply the following mathematical model:

**Password:** `Nu6os7LOqRwiUdFGV123`

* **Alphabet ($N$):** Uppercase (26) + Lowercase (26) + Digits (10) $\rightarrow N = 62$.
* **Length ($L$):** 20 characters.
* **Calculation:**
    $$H = L \times \log_2(N)$$
    $$H = 20 \times \log_2(62)$$
    $$H = 20 \times 5.95$$
    $$H \approx 119 \text{ bits}$$

---

## 2.3 Research Questions

### 1. What is Shannon entropy and how does it apply to passwords?
**Shannon entropy** is a mathematical measure of a password's unpredictability. In this context, it quantifies the resistance of a key to brute-force attacks by considering the character set ($N$) and the length ($L$).
* **Computational Effort:** Each additional bit of entropy effectively **doubles** the search space and the effort required for an attacker. 
* **Strength Standards:** Passwords below 28 bits are considered very weak, while those between 60 and 127 bits are categorized as strong enough for sensitive financial or administrative data.

### 2. Time to crack: 8-character lowercase password (37.6 bits)
Using the formula $\text{Time} = 2^H / R$, where $H$ is 37.6 bits and $R$ is $10^9$ attempts/second:
* **Search Space:** $2^{37.6} \approx 208,900,000,000$ combinations.
* **Calculation:** $208,900,000,000 / 1,000,000,000 = 208.9$ seconds.
* **Conclusion:** This password can be cracked in approximately **209 seconds**, highlighting the vulnerability of short passwords against modern hardware.

### 3. Theoretical Entropy vs. Practical Entropy
* **Theoretical Entropy:** Assumes maximum randomness and that every character in the set has an equal probability of being chosen.
* **Practical Entropy:** Accounts for human behavior and predictable patterns. 
* **Predictable Patterns:** The use of common substitutions (e.g., "P@ssw0rd") drastically reduces actual entropy because attackers prioritize these variations in dictionary-based attacks, significantly shrinking the search space.

### 4. Advantages of KeePass vs. Manual or Browser Management
KeePass provides superior protection by enabling the use of unique, complex passwords for every service. It mitigates the following risks:
1.  **Password Recycling:** Prevents a single leak from compromising multiple accounts.
2.  **Phishing and Auto-fill Exploits:** By not relying on browser-integrated scripts that can be targeted by malicious websites.
3.  **Human Error:** Eliminates the need for users to remember complex strings, which often leads to the selection of weaker passwords.

---

## 2.4 Bibliography
* FlashStart. (2024). *Password cracking techniques*.
* OWASP. (2023). *Authentication cheat sheet*. Open Web Application Security Project.
* ToolDone. (2026). *Password entropy calculator*.
* Trevino, A. (2024). *Password entropy: What it is and why it's important*. Keeper Security.
* Weir, M., et al. (2009). *Password cracking using probabilistic context-free grammars*. IEEE Symposium on Security and Privacy.

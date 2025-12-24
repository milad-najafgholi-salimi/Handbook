### 1. **MD5 (Message Digest 5)**

**Output:** 128 bits  
**Status:** ❌ Broken / Insecure

**Characteristics:**

- Very fast
    
- Easy to compute collisions (two inputs → same hash)
    
- No longer safe for security use
    

**Used today for:**

- Checksums (non-security)
    
- Legacy systems
    

**Not safe for:**

- Passwords
    
- Cryptography
    
- Digital signatures
    

---

### 2. **SHA-1**

**Output:** 160 bits  
**Status:** ❌ Broken

**Why it failed:**

- Collision attacks proven in 2017 (Google demonstrated it)
    

**Still seen in:**

- Old Git repositories
    
- Legacy systems
    

**Should not be used anymore**

---

### 3. **SHA-2 Family (SHA-256, SHA-512, etc.)**

**Output:**

- SHA-256 → 256 bits
    
- SHA-512 → 512 bits
    

**Status:** ✅ Secure (currently)

**Strengths:**

- No practical collisions known
    
- Used in Bitcoin, HTTPS, TLS, digital signatures
    
- Widely trusted and standardized
    

**Weaknesses:**

- Fast → not ideal alone for password hashing (needs salting + stretching)
    

---

### 4. **SHA-3 (Keccak)**

**Output:** Variable (256, 512, etc.)  
**Status:** ✅ Very secure

**Why it exists:**

- Designed as a backup in case SHA-2 is broken
    
- Different internal design (sponge construction)
    

**Use cases:**

- High-security systems
    
- Cryptographic research
    
- Government applications
    

---

### 5. **BLAKE2 / BLAKE3**

**Output:** Configurable  
**Status:** ✅ Very secure & fast

**Why people love it:**

- Faster than SHA-2 and SHA-3
    
- Secure
    
- Modern design
    

**Used in:**

- File integrity
    
- Modern cryptographic systems
    
- Git (newer versions experimenting)
    

---

### 6. **bcrypt / scrypt / Argon2 (Password Hashing)**

These are **not general-purpose hashes** — they are **password hashing functions**.

|Algorithm|Designed For|Key Feature|
|---|---|---|
|bcrypt|Passwords|Slow, salted|
|scrypt|Passwords|Memory-hard|
|Argon2|Passwords|Best modern choice|

✔ Resistant to brute-force attacks  
✔ Slows attackers using GPUs/ASICs

---

## Summary Table

|Hash Function|Secure?|Main Use|
|---|---|---|
|MD5|❌ No|Legacy checksums|
|SHA-1|❌ No|Deprecated|
|SHA-256|✅ Yes|Crypto, blockchain|
|SHA-3|✅ Yes|High-security apps|
|BLAKE3|✅ Yes|Fast hashing|
|bcrypt|✅ Yes|Password storage|
|Argon2|✅ Yes (Best)|Password storage|

---

## 🧩 Choosing the Right Hash

- **Passwords?** → Argon2 / bcrypt
    
- **File integrity?** → SHA-256 / BLAKE3
    
- **Cryptographic systems?** → SHA-256 / SHA-3
    
- **Speed-critical apps?** → BLAKE3
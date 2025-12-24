**Encryption** is the process of converting readable data (**plaintext**) into unreadable data (**ciphertext**) using a mathematical algorithm and a **key**.

Only someone with the correct key can **decrypt** it back into readable form.

### Simple idea:
```
Plaintext  →  Encryption (with key)  →  Ciphertext
Ciphertext →  Decryption (with key)  →  Plaintext
```

---

## Why Encryption Is Important

Encryption protects data from:

- Hackers
    
- Eavesdroppers
    
- Data theft
    
- Unauthorized access
    

It’s used in:

- Messaging apps
    
- HTTPS websites
    
- Online banking
    
- Wi-Fi security
    
- Cloud storage
    

---

## 🔑 Types of Encryption

### 1. **Symmetric Encryption**

Same key is used to encrypt and decrypt.

**Example:**

- AES (Advanced Encryption Standard)
    

**Pros:**

- Fast
    
- Efficient for large data
    

**Cons:**

- Key must be shared securely
    

`Sender & Receiver both have the same secret key`

---

### 2. **Asymmetric Encryption**

Uses **two keys**:

- **Public key** (shared with everyone)
    
- **Private key** (kept secret)
    

**Example:**

- RSA
    
- ECC
    

**How it works:**

- Anyone encrypts using your **public key**
    
- Only you can decrypt using your **private key**
    

Used in:

- HTTPS
    
- Email encryption
    
- Digital signatures
    

---

## Encryption vs Hashing (Quick Comparison)

|Feature|Encryption|Hashing|
|---|---|---|
|Reversible|✅ Yes|❌ No|
|Uses key|✅ Yes|❌ No|
|Purpose|Confidentiality|Integrity & verification|
|Example|AES|SHA-256|

---

## 🧩 Real-World Example (HTTPS)

When you visit a secure website:

1. Your browser gets the site’s public key
    
2. A secure session key is created
    
3. All data is encrypted using that key
    
4. Hackers only see scrambled data
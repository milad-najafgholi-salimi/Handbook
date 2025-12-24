In **computer science**, a _hash_ is the result of applying a **hash function** to some data.

A **hash function**:

- Takes an input of _any size_ (text, file, password, etc.)
    
- Produces a **fixed-size output** (called a _hash value_ or _digest_)
    
- Is **deterministic** (same input → same output)
    
- Is designed to be **fast** and **one-way**
    

### Example

Input:

`"hello"`

Hash (using SHA-256):

`2cf24dba5fb0a30e26e83b2ac5b9e29e...`

Even a tiny change:

`"Hello"`

produces a **completely different** hash.

---

## Why Hashing Is Useful

### 1. **Password Storage**

Websites don’t store your actual password.

Instead:

`password → hash → store hash`

When you log in:

- Your password is hashed again
    
- The hashes are compared
    

✔ Safer if the database is leaked  
❌ Attackers can’t easily reverse the hash

---

### 2. **Data Integrity**

Hashes verify that data hasn’t been altered.

Example:

- Download a file
    
- Compare its hash with the official one
    
- If they match → file is intact
    

Used in:

- Software downloads
    
- Digital signatures
    
- Blockchain systems
    

---

### 3. **Hash Tables (Data Structures)**

A **hash table** stores key–value pairs for very fast lookup.

Example:

`Key: "Alice" → Hash → Index 42 → Value: 555-1234`

This enables:

- O(1) average lookup time
    
- Fast dictionaries, maps, caches
    

---

## Cryptographic vs Non-Cryptographic Hashes

### Cryptographic Hashes

Used for security:

- SHA-256
    
- SHA-3
    
- BLAKE2
    

Properties:

- Hard to reverse
    
- Resistant to collisions
    
- Sensitive to small changes
    

### Non-Cryptographic Hashes

Used for speed, not security:

- MurmurHash
    
- xxHash
    

Used in:

- Hash tables
    
- Databases
    
- Caches
    

---

## ⚠️ Hash ≠ [[Encryption]]

|Hashing|Encryption|
|---|---|
|One-way|Two-way|
|Cannot recover original|Can decrypt with key|
|Used for integrity|Used for confidentiality|

A **Rainbow Table Attack** is a type of **password-cracking attack** that uses **precomputed hash values** to reverse hashed passwords **much faster** than brute force.

---

## What Is a Rainbow Table?

A **rainbow table** is a huge database that stores:

`Plaintext password  →  Hash`

for millions or billions of possible passwords.

Instead of computing hashes during an attack, the attacker **looks them up instantly**.

---

## How a Rainbow Table Attack Works

### Step 1: Attacker gets a password database

Example:

`username | password_hash`

### Step 2: Attacker looks up the hash in a rainbow table

If the hash exists in the table:

`5f4dcc3b5aa765d61d8327deb882cf99 → "password"`

✔ Password cracked instantly  
❌ No guessing required

---

## Why Rainbow Table Attacks Are Fast

Because:

- Hashing was done **in advance**
    
- Lookup is extremely fast
    
- No need to recompute hashes per target
    

That’s why early systems using **unsalted MD5 or SHA-1** were easily cracked.

---

## How Salting Stops Rainbow Tables

When a **salt** is added:

`hash(password + salt)`

Each user now has a _unique_ hash, even with the same password.

To crack it, an attacker would need:

- A **separate rainbow table for each salt**
    
- Which is computationally impractical
    

👉 One salt breaks the entire rainbow table concept.

---

## Example

Without salt:

`password123 → e99a18c428cb38d5f260853678922e03`

With salt:

`password123 + A9$k → 1f3870be274f6c49b3e31a0c6728957f`

The attacker must rebuild the entire table just for that salt.

---

## Rainbow Table vs Brute Force

|Attack Type|Uses Precomputation|Speed|Defended By|
|---|---|---|---|
|Brute Force|❌ No|Slow|Stretching|
|Rainbow Table|✅ Yes|Fast|Salting|
|Dictionary|Partial|Medium|Strong passwords|

---

## Modern Defense Summary

To fully defend against rainbow table attacks:

1. Use **unique salts**
    
2. Use **slow password hashing** (Argon2, bcrypt, scrypt)
    
3. Never store plain hashes
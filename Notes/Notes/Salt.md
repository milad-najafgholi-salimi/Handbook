A **salt** is a **random value added to a password before hashing**.

Instead of hashing just the password:

`hash(password)`

We hash:

`hash(password + salt)`

The salt is **stored together with the hash** (it is NOT secret).

---

## Why Salt Is Needed

### 1. **Prevents [[Rainbow Table Attacks]]**

Attackers often precompute hashes for common passwords.

Example without salt:

`password123 → e99a18c428cb38d5f260853678922e03`

Once cracked, **every user with that password is compromised**.

With salt:
```
password123 + X7f!2 → hash1
password123 + Q9@kL → hash2
```

Same password → different hashes  
➡ Precomputed tables become useless.

---

### 2. **Prevents Identical Hashes for Same Passwords**

Without salt:
```
User A password = "123456"
User B password = "123456"
→ Same hash
```

With salt:
```
User A → 9f3a...
User B → 81c2...
```

Attackers can no longer tell who shares the same password.

---

### 3. **Makes Brute-Force Attacks Slower**

Each password guess must be re-hashed **per user**, not once globally.

---

## How Salting Works (Step-by-Step)

1. User creates a password
    
2. System generates a **random salt**
    
3. Password + salt → hash
    
4. Store:
    
    `username | salt | hash`
    
5. During login:
    
    - Retrieve salt
        
    - Hash entered password + salt
        
    - Compare hashes
        

---

## Salt vs Pepper (Important Distinction)

|Term|Description|
|---|---|
|**Salt**|Random, unique per user, stored with hash|
|**Pepper**|Secret value stored separately (e.g., in server config)|

Pepper adds an extra layer if the database is stolen.

---

## Example (Conceptual)

```
Password:   hunter2
Salt:       9xA#1@
Combined:   hunter29xA#1@
Hash:       e4f3c9d1a2...
```

---

## Best Practices

- Always use **unique salt per password**
    
- Use **slow password hash functions** (Argon2, bcrypt, scrypt)
    
- Never invent your own crypto
    
- Never reuse salts
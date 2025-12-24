A **pepper** is a **secret value added to a password before hashing**, just like a salt — **but unlike a salt, it is NOT stored in the database**.

Think of it as a **global secret key** known only to the application or server.

`hash(password + salt + pepper)`

---

## Key Difference: Salt vs Pepper

|Feature|Salt|Pepper|
|---|---|---|
|Unique per user|✅ Yes|❌ No (usually global)|
|Stored with hash|✅ Yes|❌ No|
|Secret|❌ No|✅ Yes|
|Purpose|Stop rainbow tables|Protect even if DB is stolen|

---

## Why Pepper Is Useful

Imagine an attacker steals your entire user database:

`username | salt | hash`

If **no pepper** is used:

- Attacker can immediately start cracking passwords offline.
    

If **pepper is used**:

- The attacker **still can’t verify guesses** without knowing the pepper.
    
- Even with GPUs, they’re stuck unless they also breach the server or config.
    

Pepper acts like a **second lock**.

---

## Where Is the Pepper Stored?

A pepper should be stored:

- In **application configuration**
    
- In **environment variables**
    
- In a **hardware security module (HSM)** (best case)
    

🚫 Never store it in the database  
🚫 Never hard-code it in source control

---

## Example (Conceptual)
```
Password: hunter2
Salt:     7xA9
Pepper:   $eCrEtKey!

Input to hash:
hunter27xA9$eCrEtKey!
```

Even if the database is stolen, attackers **cannot test guesses** without the pepper.

---

## Important Caveats

- If the **pepper is leaked**, security drops back to salted-hash level
    
- Rotating pepper is difficult (requires re-hashing passwords)
    
- Pepper does NOT replace salting — it complements it
    

---

## Real-World Usage

Pepper is commonly used in:

- High-security systems
    
- Financial institutions
    
- Authentication servers
    
- Systems protecting sensitive credentials
    

Many frameworks don’t do this automatically — it’s an architectural decision.

---

## Summary

|Concept|Purpose|
|---|---|
|Salt|Prevents rainbow tables|
|Stretching|Slows brute-force|
|Pepper|Protects if database is stolen|

Used together:

`hash(password + salt + pepper)`

= **strong modern password protection**
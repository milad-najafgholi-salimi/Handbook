**Stretching** means **intentionally making the hashing process slow** by performing **many repeated computations** on the password.

Instead of:

`hash(password)`

You do:

`hash(hash(hash(hash(...password))))`

…thousands or even millions of times.

This process is called **key stretching**.

---

## Why Stretching Is Important

Computers (especially GPUs) can try **billions of passwords per second**.

Stretching makes each password attempt:

- **Slow**
    
- **Expensive**
    
- **Hard to parallelize**
    

So attackers can’t brute-force passwords efficiently.

---

## Example

Without stretching:
```
1 hash = 1 microsecond
→ 1 billion guesses per second
```

With stretching (e.g., 100,000 iterations):

```
1 login attempt ≈ 100 ms
→ attacker can only try ~10 passwords per second
```

That’s a **massive security improvement**.

---

## Salt + Stretch = Strong Defense

Modern password hashing uses:

`hash = f(password + salt, iterations)`

Where:

- **Salt** → prevents rainbow tables
    
- **Stretching** → slows brute-force attacks
    

---

## Algorithms That Use Stretching

|Algorithm|Stretching?|Notes|
|---|---|---|
|**bcrypt**|✅ Yes|Adjustable cost factor|
|**scrypt**|✅ Yes|Also memory-hard|
|**Argon2**|✅ Yes|Best modern choice|
|SHA-256|❌ No|Too fast alone|

---

## Real-World Analogy

Imagine a lock:

- **No stretching** → cheap lock you can pick fast
    
- **Stretching** → lock that takes 5 minutes per attempt
    

Even if the attacker knows how the lock works, time kills the attack.

---

## Summary

|Concept|Purpose|
|---|---|
|Salt|Prevents precomputed attacks|
|Stretching|Slows down guessing|
|Hashing|Converts password to fixed-size output|

Together, they form **secure password storage**.
The **`random` module** in Python is used to generate **pseudo-random numbers**. It is commonly used in:

- Simulations
    
- Games
    
- Sampling data
    
- Shuffling lists
    
- Random selections
    
- Probability experiments

---
## 1) What Does “Pseudo-Random” Mean?

The random module does not generate truly random numbers.

It uses a deterministic algorithm (Mersenne Twister) to generate numbers that appear random.

If you use the same seed, you get the same sequence of numbers.

---
## 2) Importing the Module
```
import random
```
Or:
```
from random import randint, choice
```

---
## 3) Generating Random Numbers
### 1. `random.random()`
Returns a float between 0.0 and 1.0
```
random.random()
```
Example output:
```
0.73458293
```
Range:
```
0.0 <= x < 1.0
```

---
### 2) `random.uniform(a, b)`

Returns a float between `a` and `b`
```
random.uniform(5, 10)
```
Output:
```
7.4321
```

---
### 3) `random.randint(a, b)`
Returns an integer between a and b (inclusive)
```
random.randint(1, 6)
```
Simulates a dice roll.

Range:
```
a <= x <= b
```

---
### 4) `random.randrange(start, stop, step)`

Similar to `range()`
```
random.randrange(0, 10, 2)
```
Possible outputs:
```
0, 2, 4, 6, 8
```

---
## 4) Random Selection from Sequences

### 1. `random.choice()`

Selects one random element from a sequence.
```
colors = ["red", "blue", "green"]
random.choice(colors)
```
### 2. `random.choices()`

Selects multiple elements (with replacement).
```
random.choices(colors, k=2)
```
May repeat elements.
### 3. `random.sample()`
Selects multiple unique elements (without replacement).
```
random.sample(colors, 2)
```
No repetition.

---
## 5) Shuffling Data

### `random.shuffle()`

Shuffles a list **in place**.
```
numbers = [1, 2, 3, 4, 5]
random.shuffle(numbers)
print(numbers)
```
Important:

- It modifies the original list.
    
- Returns `None`.

---
## 6) Controlling Randomness (Seeding)
### `random.seed()`
Used to make results reproducible.
```
random.seed(10)
print(random.randint(1, 100))
```
If you run this again, you’ll get the same number.

Useful in:

- Testing
    
- Research
    
- Debugging
    
- Machine learning experiments
    

---
## 7) Generating Random Floating Numbers
```
random.random()
random.uniform(a, b)
```

---
## 8) Probability-Based Selection

You can assign weights:
```
colors = ["red", "blue", "green"]
weights = [0.1, 0.3, 0.6]

random.choices(colors, weights=weights, k=5)
```
More likely to choose "green".

---
## 9) Random Boolean Example
```
random.choice([True, False])
```

---
## 10) Real-World Examples

### Dice Simulator
```
import random

dice = random.randint(1, 6)
print(dice)
```
### Shuffle Cards
```
import random

cards = ["A", "K", "Q", "J"]
random.shuffle(cards)
print(cards)
```
### Lottery Numbers
```
import random

lottery = random.sample(range(1, 50), 6)
print(lottery)
```

---
## 11) Important Notes for Exams

1. `randint(a, b)` includes both endpoints.
    
2. `randrange()` excludes stop value (like `range()`).
    
3. `shuffle()` changes the original list.
    
4. `sample()` does not allow duplicates.
    
5. `choices()` allows duplicates.
    
6. Setting a seed makes output predictable.
    

---

## 12) Security Warning

The `random` module is **NOT secure** for:

- Password generation
    
- Cryptography
    
- Security tokens
    

For secure randomness, use:
```
import secrets
```
Example:
```
secrets.token_hex(16)
```

---
## 13) Summary

The random module allows you to:

✔ Generate random integers
✔ Generate random floats
✔ Randomly select items
✔ Shuffle lists
✔ Sample data
✔ Control randomness with seeds

It is widely used in:
- Games
- Simulations
- Statistics
- Machine learning
- Testing

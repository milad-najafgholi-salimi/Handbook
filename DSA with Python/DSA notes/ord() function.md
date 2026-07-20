The `ord()` function is a built-in Python function that **returns the Unicode code point (an integer) for a given single-character string.**

In simpler terms: it converts a character into its corresponding number according to the Unicode standard.

### Basic Syntax
```
ord(character)
```
- **Parameter:** A string of length 1 (a single character).
    
- **Returns:** An integer representing the Unicode code point.

#### Examples
```
print(ord('A'))      # Output: 65
print(ord('a'))      # Output: 97
print(ord('0'))      # Output: 48
print(ord(' '))      # Output: 32 (space)
print(ord('€'))      # Output: 8364 (Euro sign)
print(ord('😊'))     # Output: 128522 (emoji)
```

---
## The Inverse: `chr()`

The opposite of `ord()` is `chr()`, which converts an integer back into a character.
```
print(chr(65))   # Output: 'A'
print(chr(128522))  # Output: '😊'
```

### Important Notes

- **Only works with single characters** — passing a string longer than 1 character raises a `TypeError`.
```
ord('AB')  # TypeError: ord() expected a character, but string of length 2 found
```
- **Works with any Unicode character**, not just ASCII (so emojis, accented letters, Chinese characters, etc., all work).
    
- **In Python 2**, `ord()` worked on ASCII/bytes, but in Python 3 it always works on Unicode characters.
Regular Expressions (RegEx) in Python are used for **pattern matching and text processing**. They allow you to search, extract, validate, split, and replace text based on patterns instead of exact strings.

RegEx is extremely powerful and widely used in:

- Input validation (email, phone numbers)
    
- Data cleaning
    
- Log analysis
    
- Web scraping
    
- Text processing
    
- Parsing structured text

---
## 1) The re Module
Python provides RegEx support through the built-in `re` module.
```
import re
```

---
## 2) Basic RegEx Functions in Python
The most important functions in `re`:

| Function        | Purpose                       |
| --------------- | ----------------------------- |
| `re.search()`   | Find first match anywhere     |
| `re.match()`    | Match at beginning only       |
| `re.findall()`  | Return all matches            |
| `re.finditer()` | Return match objects iterator |
| `re.sub()`      | Replace matches               |
| `re.split()`    | Split string                  |
| `re.compile()`  | Compile pattern for reuse     |

---
## 3) Basic Pattern Matching
Simple Example:
```
import re

text = "Python is powerful"

result = re.search("Python", text)

if result:
    print("Found!")
```

---
## 4) Special Characters (Meta Characters)
These characters have special meaning:
```
. ^ $ * + ? { } [ ] \ | ( )
```

---
## 5) Character Classes
### 1) Match Any Character
```
.
```
Matches any character except newline.
#### Example:
```
re.findall("p.t", "pat pet pit")
```
Matches: pat, pet, pit
### 2) Square Brackets [ ]
Match any one character inside.
```
re.findall("[aeiou]", "python programming")
```
Matches vowels.
### 3) Ranges
```
[a-z]    # lowercase letters
[A-Z]    # uppercase letters
[0-9]    # digits
```
### 4) Predefined Character Classes
| Pattern | Meaning                           |
| ------- | --------------------------------- |
| `\d`    | Digit (0–9)                       |
| `\D`    | Not digit                         |
| `\w`    | Word character (a-z, A-Z, 0-9, _) |
| `\W`    | Not word character                |
| `\s`    | Whitespace                        |
| `\S`    | Not whitespace                    |
#### Example:
```
re.findall("\d", "abc123")
```

---
## 6) Quantifiers (Repetition)
These specify how many times a character appears.

| Symbol  | Meaning         |
| ------- | --------------- |
| `*`     | 0 or more       |
| `+`     | 1 or more       |
| `?`     | 0 or 1          |
| `{n}`   | Exactly n       |
| `{n,}`  | n or more       |
| `{n,m}` | Between n and m |
#### Example:
```
re.findall("a+", "aa aaaa b")
```
Matches: `"aa"`, `"aaaa"`

---
## 7) Anchors
| Symbol | Meaning         |
| ------ | --------------- |
| `^`    | Start of string |
| `$`    | End of string   |
#### Example:
```
re.findall("^Hello", "Hello world")
```

---
## 8) Groups and Parentheses ( )
Used to group patterns.
```
text = "My number is 12345"
result = re.search(r"(\d+)", text)

print(result.group())  # Full match
print(result.group(1)) # Captured group
```

---
## 9) Alternation | (OR operator)
```
re.findall("cat|dog", "cat and dog")
```

---
## 10) re.findall()
Returns all matches as a list.
```
re.findall(r"\d+", "Age 25, year 2026")

#Output:
['25', '2026']
```

---
## 11) re.sub() (Replace)
```
text = "I love cats"
new_text = re.sub("cats", "dogs", text)
print(new_text)
```

---
## 12) `re.split()`
```
re.split(r"\s+", "Python is very powerful")
```
Splits on whitespace.

---
## 13) Raw Strings (Very Important)

Always use `r""` for regex patterns.

Wrong:
```
"\d"
```
Correct:
```
r"\d"
```
Because \ has special meaning in Python strings.

---
## 14) Compiling Patterns
If you use a pattern multiple times:
```
pattern = re.compile(r"\d+")

pattern.findall("123 abc 456")
```
More efficient.

---
## 15) Flags
Flags modify behavior.

| Flag            | Meaning             |
| --------------- | ------------------- |
| `re.IGNORECASE` | Case insensitive    |
| `re.MULTILINE`  | Multi-line mode     |
| `re.DOTALL`     | Dot matches newline |
#### Example:
```
re.findall("python", "Python is fun", re.IGNORECASE)
```

---
## 16) Email Validation Example
```
pattern = r"^[\w\.-]+@[\w\.-]+\.\w+$"

email = "test@example.com"

if re.match(pattern, email):
    print("Valid email")
```

---
## 17) Common Mistakes Students Make

1. Forgetting raw string (`r""`)
    
2. Confusing `match()` and `search()`
    
3. Forgetting `+` when matching multiple digits
    
4. Not escaping special characters like `.` or `?`
    
5. Misunderstanding greedy behavior (`*`, `+` are greedy)
    

---

## 18) Greedy vs Non-Greedy

By default, quantifiers are greedy.

Example:
```
text = "<tag>content</tag>"
re.findall("<.*>", text)
```
Matches entire string.

Non-greedy:
```
re.findall("<.*?>", text)
```
Matches minimal pattern.

---
## 19) Summary

RegEx in Python allows you to:

✔ Search patterns  
✔ Extract data  
✔ Validate input  
✔ Replace text  
✔ Split strings  
✔ Perform complex text processing

It is one of the most powerful tools in Python for working with text data.
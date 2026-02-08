**Unit testing** is a software testing technique where you test **small, individual pieces of code (units)**—usually functions or methods—to make sure they work correctly in isolation.

---
## 1. What Is a “Unit”?

A **unit** is the smallest testable part of a program.

In Python, a unit is typically:

- A function
    
- A method of a class
    

Example unit:
```
def add(a, b):
    return a + b
```
This function is a single unit.

---
## 2. What Is Unit Testing?

**Unit testing means:**

- Writing code that tests other code
    
- Checking whether a unit produces the expected output
    
- Running tests automatically
    

Example idea:

> “If I give `add(2, 3)`, I expect `5`.”

---

## 3. Why Unit Tests Are Important

### Benefits

✔ Catch bugs early  
✔ Prevent regressions (old bugs coming back)  
✔ Make code safer to change  
✔ Improve code design  
✔ Serve as documentation  
✔ Increase confidence in your code

In professional projects, **code without tests is considered risky**.

---

## 4. Unit Testing vs Other Testing Types

|Type|What It Tests|
|---|---|
|Unit testing|Individual functions/methods|
|Integration testing|How components work together|
|System testing|Entire application|
|Acceptance testing|User requirements|

👉 Unit tests are **fast, small, and isolated**.

---

## 5. Unit Testing in Python: `unittest`

Python has a built-in testing framework called **`unittest`**.
### Basic Structure
```
import unittest

class TestSomething(unittest.TestCase):
    def test_case_name(self):
        self.assertEqual(actual, expected)

if __name__ == "__main__":
    unittest.main()
```

---
## 6. Simple Unit Test Example
### Code to Test (`math_utils.py`)
```
def divide(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b
```
### Test Code (`test_math_utils.py`)
```
import unittest
from math_utils import divide

class TestDivide(unittest.TestCase):

    def test_normal_division(self):
        self.assertEqual(divide(10, 2), 5)

    def test_divide_by_zero(self):
        with self.assertRaises(ValueError):
            divide(10, 0)

if __name__ == "__main__":
    unittest.main()
```

---
## 7. How Tests Work
- test_ prefix tells Python this is a test
- Each test checks one behavior
- Tests either:
	- Pass ✅
	- Fail ❌
	- Error ⚠️

---
## 8. Common Assertions in Unit Tests
Assertions are checks that verify expected behavior.

| Assertion              | Purpose         |
| ---------------------- | --------------- |
| `assertEqual(a, b)`    | a == b          |
| `assertNotEqual(a, b)` | a != b          |
| `assertTrue(x)`        | x is True       |
| `assertFalse(x)`       | x is False      |
| `assertRaises(Error)`  | error is raised |
| `assertIn(a, b)`       | a in b          |
| `assertIsNone(x)`      | x is None       |
### Example:
```
self.assertIn(3, [1, 2, 3])
```

---
## 9. Test Naming Conventions
Good test names explain what is being tested.
```
def test_divide_returns_float(self):
    ...

def test_divide_raises_error_on_zero(self):
    ...
```
Bad:
```
def test1(self):
    ...
```

---
## 10. Arrange – Act – Assert (AAA Pattern)

A common structure for tests:
```
def test_add(self):
    # Arrange
    a = 2
    b = 3

    # Act
    result = add(a, b)

    # Assert
    self.assertEqual(result, 5)
```
This makes tests clear and readable.

---
## 11. Testing Edge Cases (Very Important)
- Good unit tests check:
	- Normal cases
	- Edge cases
	- Error cases

Example:
```
add(0, 0)
add(-1, 1)
add(10**6, 10**6)
```

---
## 12. What Unit Tests Should NOT Do

❌ Depend on databases  
❌ Call external APIs  
❌ Read/write real files  
❌ Require user input

These make tests:

- Slow
    
- Unreliable
    
- Hard to repeat
    

(These are tested with **integration tests**, not unit tests.)

---

## 13. Mocking (Basic Idea)

When a unit depends on something external, you **mock** it.

Example idea:

> “Pretend the database returned this value.”

Python uses `unittest.mock` for this (advanced topic).

---

## 14. Unit Tests and Code Quality

Unit tests work well with:

- **Linters** (Pylint, Ruff)
    
- **Type checkers** (Mypy)
    
- **CI/CD pipelines**
    

Together, they create **reliable software**.

---

## 15. Mental Model

> **Unit tests are small experiments that prove your code behaves correctly.**

If one test fails, you know **exactly where the problem is**.

---

## 16. Common Beginner Mistakes

❌ Writing one test for everything  
❌ Testing implementation instead of behavior  
❌ Skipping edge cases  
❌ Not running tests regularly

✔ Many small tests  
✔ Clear expectations  
✔ Fast execution
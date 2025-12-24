## 1. Basic Help Commands

### `?` or `help()`

These are the most common ways to access documentation for a function, dataset, or object.
```
?mean
help(mean)
```

This opens a help page that usually includes:

- **Description** – what the function does
    
- **Usage** – how to call it
    
- **Arguments** – explanation of each parameter
    
- **Details** – deeper technical notes
    
- **Value** – what the function returns
    
- **Examples** – runnable examples (very important!)
    

You can run examples directly:

`example(mean)`

---

## 2. Searching for Help When You Don’t Know the Exact Name

### `??` or `help.search()`

If you know _what_ you want to do but not the function name:
```
??"linear regression"
help.search("regression")
```

This searches across installed packages and help files.

---

## 3. Viewing Help in a Browser

### `help.start()`

Launches an HTML-based help system in your web browser:

`help.start()`

This gives access to:

- Manuals
    
- Package documentation
    
- Search interface
    

Useful if you prefer browsing instead of typing commands.

---

## 4. Getting Help for Packages

### Package documentation

`help(package = "ggplot2")`

Shows:

- Overview of the package
    
- Available functions
    
- Vignettes (tutorial-style documents)
    

### Vignettes (very important)
```
vignette()
vignette("ggplot2-specs", package = "ggplot2")
```

Vignettes are often **the best learning resource** for complex packages.

---

## 5. Understanding Function Structure

### `args()`

Shows function arguments without the full documentation:

`args(mean)`

### `str()`

Shows the internal structure of an object:

`str(mtcars)`

Very useful for understanding data frames, lists, and model objects.

---

## 6. Discovering Methods for Objects

Many functions behave differently depending on object type (S3 methods).

### `methods()`

`methods(class = "lm")`

Or:

`methods(plot)`

This shows all available methods for a generic function.

---

## 7. Getting Help from Examples and Source Code

### View source code

`getAnywhere(mean)`

or for user-defined functions:

`body(my_function)`

This is useful when you want to understand _how_ something works internally.
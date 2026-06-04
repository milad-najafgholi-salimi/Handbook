The difference between shallow and deep copying is only relevant for compound objects (objects that contain other objects, like lists or class instances):

- A _shallow copy_ constructs a new compound object and then (to the extent possible) inserts _references_ into it to the objects found in the original.
    
- A _deep copy_ constructs a new compound object and then, recursively, inserts _copies_ into it of the objects found in the original.

---
به زبان ساده shallow copy، یک پوسته جدید می‌سازد اما اعضایش به رفرنس به شیء اصلی است.

به زبان ساده deep copy، یک پوسته‌ی جدید می‌سازد و اعضایش را از شیء اصلی کپی می‌کند. اینگونه شیء جدید ارتباطی با شیء اصلی ندارد.
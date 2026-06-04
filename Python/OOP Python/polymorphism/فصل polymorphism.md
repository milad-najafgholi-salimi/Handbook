### عبارت Overriding (بازنویسی متد) در پایتون چیست؟

عبارت **Overriding** یعنی یک کلاسِ فرزند (subclass) **متدی با همان نام** (و معمولاً همان ورودی‌ها) که در کلاسِ والد (base class) وجود دارد را **دوباره تعریف کند** تا رفتار آن را **عوض کند یا گسترش دهد**.
برای مثال:
```
class Animal:
    def speak(self):
        return "some sound"

class Dog(Animal):
    def speak(self):        # override
        return "woof"

a = Animal()
d = Dog()
print(a.speak())  # some sound
print(d.speak())  # woof
```
اگر بخواهی رفتار والد را هم نگه داری: `super()`:
```
class Logger:
    def log(self, msg):
        print(f"[LOG] {msg}")

class FileLogger(Logger):
    def log(self, msg):   # override + extend
        super().log(msg)
        print("...and write to file")
```
**جمع‌بندی overriding:** ابزار اصلی برای _پلی‌مورفیسم_ (polymorphism) در OOP: یک متد واحد، رفتار متفاوت بسته به نوع شیء.

---
### عبارت Overloading (چندریختیِ تابع/متد) در پایتون چیست؟

در خیلی از زبان‌ها **Overloading** یعنی بتوانی چند تابع/متد با **یک نام** ولی با **پارامترهای متفاوت** تعریف کنی (مثلاً یکی ۲ پارامتر بگیرد، یکی ۳ تا)، و زبان خودش انتخاب کند کدام را صدا بزند.

اما:

#### در پایتون “method/function overloading” به شکل کلاسیک وجود ندارد

یعنی اگر در یک کلاس دوبار متدی با یک نام تعریف کنی، **تعریف آخر، قبلی را کامل جایگزین می‌کند**.
```
class A:
    def f(self, x):
        return x

    def f(self, x, y):   # overloading - this will run always
        return x + y

# A().f(1)  -> TypeError - because you didn't enter second argoman

```

---

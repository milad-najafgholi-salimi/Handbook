## بررسی مدل ۱ - single (simple) inheritance:
```
Parent class
	^
	|
	|
Child class
```

تمام کاری که باید انجام دهیم که child class ، کلاس والد (parent class) خود را بشناسد این است که بصورت زیر عمل کنیم:
```
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name
		
	def full_name(self):
		return f"{self.first_name} {self.last_name}"
		
class Employee(Person):
	pass
```
توضیحات:
به سادگی با پارامتر قرار دادن Person برای کلاس Employee، ما کلاس Employee را به child class و کلاس Person را به Parent class تبدیل کردیم ؛ اما هنوز child class کار خاصی انجام نمی‌دهد. فعلا صرفا کلاس والد و فرزند ساختیم.

بخش `def full_name(self)` را پارامتر `self` دادیم به این خاطر که object های کلاس را بشناسد . در غیر اینصورت object ها را نشناخته و نمی‌توانیم از آن‌ها همانطور که مشاهده می‌شود استفاده کنیم.

به کد زیر دقت کنید:
```
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name
		
	def full_name(self):
		return f"{self.first_name} {self.last_name}"
		
class Employee(Person):
	salary = 300 # class variable
	
	def __init__(self, position): # overriding
		self.position = position
		
	def job(self):
		return f"Hello I'm {self.first_name} {self.last_name} and I work at {self.position} position in the company."
		
emp1 = Employee("Milad", "Salimi", "Data Scientist")
print(emp1.job())

# output:
TypeError: Employee.__init__() takes 2 positional arguments but 4 were given
```

خطا خواهد داد زیرا متد `__init__` در کلاس فرزند بازنویسی شده است و ارتباط با متد `__init__` در کلاس والد قطع است؛ اما دلیل اصلی خطا آن است که متد override شده در کلاس فرزند ، دو آرگومان می‌گیرد درحالی که ما چهار تا وارد کردیم .

اما حال اگر به گونه‌ی زیر عمل کنیم:
```
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	def full_name(self):
		return f"{self.first_name} {self.last_name}"

class Employee(Person):
	salary = 300 # class variable

	def __init__(self, position): # overriding
		self.position = position

	def job(self):
		return f"Hello I'm {self.first_name} {self.last_name} and I work at {self.position} position in the company."

emp1 = Employee("Data Scientist")

print(emp1.job())

# output:
AttributeError: 'Employee' object has no attribute 'first_name'
```

ویژگی‌های (attribute) کلاس والد را شناسایی نمی‌کند و خطا می‌دهد.

اما حال به کد زیر دقت کنید:
```
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	def full_name(self):
		return f"{self.first_name} {self.last_name}"

class Employee(Person):
	salary = 300 # class variable

	def __init__(self, position): # overriding
		self.position = position

	def job(self):
		return f"Hello I work at {self.position} position in the company."

emp1 = Employee("Data Scientist")

print(emp1.job())

# output:
Hello I work at Data Scientist position in the company.
```

بدون هیچ مشکلی اجرا می‌شود؛ اما خطای منطقی دارد و ویژگی‌های کلاس والد را به ارث نبرده است.

##### تعریف Method Overriding

متد **Overriding** در برنامه‌نویسی شی‌گرا (OOP) زمانی رخ می‌دهد که **یک کلاس فرزند (Subclass)** متدی را که در **کلاس والد (Superclass)** تعریف شده است، **با همان نام و همان امضا (signature)** دوباره پیاده‌سازی کند تا رفتار آن را تغییر دهد؛ و اینگونه متد دوم جایگزین متد اول خواهد شد و متد اول نادیده گرفته می‌شود (اگر به درستی جدا نشده باشند).

---
### اما چگونه به درستی child class تمام یا بخشی از ویژگی‌های parent class را به ارث ببرد؟

برای حل خطاهای بالا و همچنین برای رفع مشکل override شدن متد `__init__` که بتواند به درستی ارث ببرد ، به گونه‌ی زیر عمل می‌کنیم:
```
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	def full_name(self):
		return f"{self.first_name} {self.last_name}"

class Employee(Person):
	salary = 300 # class variable

	def __init__(self, first_name, last_name, position):
		Person.__init__(self, first_name, last_name)
  # or: super().__init__(first_name, last_name)
		self.position = position
		
	def job(self):
		return f"Hello I'm {self.first_name} {self.last_name} and I work at {self.position} position in the company."
		
		
emp1 = Employee("Milad", "Salimi", "Data Scientist")
print(emp1.job())

# output:
Hello I'm Milad Salimi and I work at Data Scientist position in the company.
```

### بنابراین برای ارث بری درست باید به موارد زیر به ترتیب دقت کنیم:

**۱) کلاس والد باید پارامتر کلاس فرزند باشد.**

**۲) متد `__ini__` را تشکیل داده و تمامی attribute های قبلی بعلاوه‌ی جدید را بعنوان پارامتر وارد کنید.**

**۳) باید پارامتر‌هایی را که می‌خواهیم از متد `__init__` ارث برده شود را به همراه نام کلاس والد مشخص کنیم ؛ یا آنکه بجای نام کلاس والد، از کلید واژه `super` بجای آن استفاده کنیم؛ که مورد دوم حرفه‌ای‌تر و بهتر است.** مانند:
```
Person.__init__(self, first_name, last_name)

or 

super().__init__(first_name, last_name)
```

نکته: () ها در آخر هر چیزی که قابل صدا زدن و فراخوانی است، باعث صدا زدن آن می‌شود. مانند `()super` ؛ همچنین در کلاس‌ها  و توابع و موارد دیگر از این قبیل.

---
## بررسی مدل ۲ - Multi-level inheritance:
```
Parent class
	^
	|
	|
Parent/Child class
	^
	|
	|
Child class
```

به مثال زیر که بسط مثال قبل است دقت کنید:

```
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	def full_name(self):
		return f"{self.first_name} {self.last_name}"

class Employee(Person):
	salary = 300 # class variable

	def __init__(self, first_name, last_name, position):
		Person.__init__(self, first_name, last_name)
  # or: super().__init__(first_name, last_name)
		self.position = position
		
	def job(self):
		return f"Hello I'm {self.first_name} {self.last_name} and I work at {self.position} position in the company."
		
class CTO(Employee):
	salary = 6000 # class variable
	
	def job(self):
		return f"Hello I'm {self.first_name} {self.last_name} and I work at {self.position} position as CTO of the company."
		
		
emp1 = CTO("Milad", "Salimi", "Data Scientist")
print(emp1.job())

# output:
Hello I'm Milad Salimi and I work at Data Scientist position as CTO of the company.
```

---
## بررسی مدل ۳ - multiple inheritance:
```
Parent class    Parent class
       ^             ^
       |             |
        \           /
         \         /
          \       /
           \     /
            \   /
             \ /    
        Child class
```

به مثال زیر که بسط بیشتر مثال‌های پیشین است دقت کنید - کلاس جدیدی به نام کلاس Manager تعریف شد که کلاس CTO از دو کلاس Employee و Manager ارث بری 
می‌کند:

```
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	def full_name(self):
		return f"{self.first_name} {self.last_name}"

class Employee(Person):
	salary = 300 # class variable

	def __init__(self, first_name, last_name, position):
		Person.__init__(self, first_name, last_name)
  # or: super().__init__(first_name, last_name)
		self.position = position
		
	def job(self):
		return f"Hello I'm {self.first_name} {self.last_name} and I work at {self.position} position in the company."

class Manager:
	def authority(self):
		return "can fire anyone"	
	
class CTO(Employee, Manager):
	salary = 6000 # class variable
	
	def job(self):
		return f"Hello I'm {self.first_name} {self.last_name} and I work at {self.position} position as CTO of the company."
		
		
emp1 = CTO("Milad", "Salimi", "Data Scientist")
print(emp1.job())
print(emp1.authority())

# output:
Hello I'm Milad Salimi and I work at Data Scientist position as CTO of the company.
can fire anyone
```

---
## بررسی مدل ۴ - hierachrchical inheritance:
```
		Parent class
			^^
			||
		   /  \	
	      /    \
	     /      \
Child class     Child class
```

به مثال زیر که آخرین بسط از مثال‌های پیشین است دقت کنید - دو کلاس CTO و Intern هر دو از یک کلاس مشترک Employee ارث بری می‌کنند:
```
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	def full_name(self):
		return f"{self.first_name} {self.last_name}"

class Employee(Person):
	salary = 300 # class variable

	def __init__(self, first_name, last_name, position):
		Person.__init__(self, first_name, last_name)
  # or: super().__init__(first_name, last_name)
		self.position = position
		
	def job(self):
		return f"Hello I'm {self.first_name} {self.last_name} and I work at {self.position} position in the company."

class Manager:
	def authority(self):
		return "can fire anyone"	
	
class CTO(Employee, Manager):
	salary = 6000 # class variable
	
	def job(self):
		return f"Hello I'm {self.first_name} {self.last_name} and I work at {self.position} position as CTO of the company."
		
class Intern(Employee):
	salary = 1000
	
	def job(self):
		return "learning new things"
		
emp1 = Intern("Milad", "Salimi", "Data Scientist")
print(emp1.job())

# output:
learning new things
```
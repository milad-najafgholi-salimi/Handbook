متد‌های کلاس (class method) یک نوع دکوراتور هستند که باعث می‌شود تابعی که وابسته به object ها و instance های object است (همان ورودی‌هایی که به جای self می‌نشینند) ، از این وابستگی رها شود و وابسته به کلاس شود. 

اما static method ها از این هم فراتر رفته و تابعی که وابسته به کلاس است را هم رها و آزاد می‌کنند؛ (حتی اگر تابع واسته به object ها هم باشد، آن تابع را به یکباره از object ها و حتی کلاس، آزاد و مستقل می‌کند).

همانطور که پارامتر self به object اشاره دارد، در class method، پارامتر cls به نام کلاس اشاره دارد (یعنی object به جای self می‌نشیند و نام کلاس به جای cls).

```
class Employee:
	salary = 3000
	total_employee = 0
	
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name
		Employee.total_employee += 1

	def full_name(self):
		return f"{self.first_name} {self.last_name}"

	@classmethod
	def raise_salary(cls, new_salary):
		if type(new_salary) == int:
			cls.salary = new_salary
		else:
			raise ValueError

emp1 = Employee("Milad", "Salimi")
emp2 = Employee("Peter", "Parker")

print("before")
print(f"{emp1.full_name()} - {Employee.salary}")
print(f"{emp2.full_name()} - {Employee.salary}")

Employee.raise_salary(6000)

print("after")
print(f"{emp1.full_name()} - {Employee.salary}")
print(f"{emp2.full_name()} - {Employee.salary}")

# output:
before
Milad Salimi - 3000
Peter Parker - 3000
after
Milad Salimi - 6000
Peter Parker - 6000
```

به بیان شفاف‌تر، static method یک متددی است که درون کلاس تعریف شده اما با اضافه کردن دکوراتور `staticmethod@` مانند یک تابع مستقل عمل می‌کند.

متد کلاس (class method) متدی است که درون کلاس است که بطور عادی با object کار می‌کند اما با اضافه کردن دکوراتور `classmethod@` به آن، آن متد مانند یک متد وابسته به کلاس کار می‌کند.

به تیکه کدی که از بالا بریده شده و به شکل دیگری (و بهتری) آن را پیاده سازی کرده دقت کنید:
```
@classmethod
def raise_salary(cls, new_salary):
	if type(new_salary) == int:
		cls.salary = new_salary
		return cls.salary
	else:
		raise ValueError
		
print(Employee.raise_salary(6000))

# output:
6000
```
توضیحات:
از آنجایی که با اضافه کردن دکوراتور `classmethod@` به متد `raise_salary` آن را از سطح object method به سطح class method آوردیم، پس برای صدا زدن آن می‌توانیم از کلاس به جای object استفاده کنیم (هرچند که با object هم کار می‌کند).

به مثال زیر که یک مثال برای `static method` است دقت کنید:
```
class Employee:
	salary = 3000
	total_employee = 0
	
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name
		Employee.total_employee += 1

	def full_name(self):
		return f"{self.first_name} {self.last_name}"

	@classmethod
	def raise_salary(cls, new_salary):
		if type(new_salary) == int:
			cls.salary = new_salary
			return cls.salary
		else:
			raise ValueError

	@staticmethod
	def greetings(name):
		return f"Hello {name}"

print(Employee.raise_salary(6000))
print(Employee.greetings("Milad"))

# output:
6000
Hello Milad
```
توضیحات:
متد `greetings` مانند یک تابع مستقل معمولی عمل می‌کند، اما برای دسترسی به آن باید آدرس آن را درست وارد کنیم تا بتوانیم از آن استفاده کنیم. چون این متد درون کلاس قرار دارد، باید ابتدا نام کلاس را بعنوان آدرس وارد کرده و سپس متد را صدا بزنیم تا اجرا شود. 
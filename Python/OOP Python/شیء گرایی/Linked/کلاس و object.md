متغیر‌های کلاس (class variable) خصوصیات درون کلاس که برای تمام objectهایی که قرار است ساخته شوند، مشابه می‌شود.
```
class Employee:
	name = "Milad" # class variable

emp1 = Employee()
emp2 = Employee()

print(emp1.name)
print(emp2.name)

# output:
Milad
Milad
```

مناسب نیست . زیرا من می‌خواهم هر object که ساخته می‌شود خصوصیات خاص داشته باشد.

زمانی که یک کلاس ساخته می‌شود، یکی از اِلمان‌هایی که صدا زده می‌شود، متد `__init__` است. (پس `__init__` یک متد است - متد‌ها توابعی هستند که درون کلاس تعریف شده‌اند. متد `__init__` یک built-in متد است که به اینگونه متد‌ها magic method یا dunder method (double under-score method) هم می‌گویند.)

همواره اولین پارامتر `__init__` ، پارامتر `self` است. کاری که این `self` می‌کند بسیار ساده است. `self` فقط یک جایگشت است؛ یعنی زمانی که یک شیء تعریف می‌کنیم و به کلاس نسبت می‌دهیم، آن شیء بطور خودکار، جانشین `self` در متد `__init__` می‌شود.
```
class Employee:
	def __init__(self): # which means: def __init__(emp1):
		self.age = 22 # which means: emp1.age = 22
		pass

emp1 = Employee()
print(emp1.age) # output: 22
```

به تفاوت زیر دقت کنید:
```
class Employee:
	name = "Milad" # class variable
	def __init__(self):
		self.age = 22  # object variable
		
print(Employee.name) # Correct! Works
print(Employee.age) # Wrong! Error
```
به این دلیل است که متغیر name مختص کلاس است اما age مختص object ایجاد می‌شود.

به نکته زیر دقت کنید - پارامتر self می‌تواند هر اسم دیگری هم باشد اما باید در همه جا یکسان باشد:
```
class Employee:
	def __init__(self, age):
		self.age = age
		
emp1 = Employee(22)
print(emp1.age) # output: 22
```

```
class Employee:
	def __init__(self, age):
		self.sth = age
		
emp1 = Employee(22)
print(emp1.sth) # output: 22
```


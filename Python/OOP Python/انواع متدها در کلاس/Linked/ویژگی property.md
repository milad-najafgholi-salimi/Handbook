یک دکوراتور است که به متد درون کلاس ویژگی‌هایی می‌دهد که باعث می‌شود آن متد مانند یک attribute رفتار کند. 

به مثال زیر توجه کنید:
```
class Employee:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name
		
	@property
	def full_name(self):
		return f"{self.first_name} {self.last_name}"


emp1 = Employee("Milad", "Salimi")
print(emp1.full_name)

# output:
Milad Salimi
```
توضیحات:
چون با کمک دکوراتور `propery@` متد `full_name` مانند یک attribute رفتار می‌کند، نیازی نداریم که با `()` آن را صدا بزنیم.

اما اگر بخواهیم با `()` آن را صدا بزنیم این اتفاق می‌افتد:
```
class Employee:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	@property
	def full_name(self):
		return f"{self.first_name} {self.last_name}"

emp1 = Employee("Milad", "Salimi")
print(emp1.full_name())

# output:
    print(emp1.full_name())
          ^^^^^^^^^^^^^^^^
TypeError: 'str' object is not callable
```

حال برای آنکه بتوانیم این متد همراه با دکوراتور property را تغییر دهیم، نیاز به تابع `setter` داریم که به شیوه‌ی زیر عمل می‌کنیم:

```
class Employee:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	@property
	def full_name(self):
		return f"{self.first_name} {self.last_name}"

	@full_name.setter
	def full_name(self, new_name):
		self.first_name, self.last_name = new_name.split(" ")

emp1 = Employee("Milad", "Salimi")
print(emp1.full_name)
emp1.full_name = "Peter Parker"
print(emp1.full_name)

# output:
Milad Salimi
Peter Parker
```

همانطور که پیش‌تر گفتم، با کمک دکوراتور `property@` می‌توانیم از آن متد به عنوان یک attribute استفاده کنیم. 

از همین توضیح استفاده می‌کنیم و یک مثال دیگر را نشان می‌دهیم که می‌توانیم مانند یک variable آن را پاک کنیم:
```
class Employee:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	@property
	def full_name(self):
		return f"{self.first_name} {self.last_name}"

	@full_name.setter
	def full_name(self, new_name):
		self.first_name, self.last_name = new_name.split(" ")

	@full_name.deleter
	def full_name(self):
		self.first_name = None
		self.last_name = None


emp1 = Employee("Milad", "Salimi")
print(emp1.full_name)

emp1.full_name = "Peter Parker"
print(emp1.full_name)

del emp1.full_name
print(emp1.full_name)

# output:
Milad Salimi
Peter Parker
None None
```

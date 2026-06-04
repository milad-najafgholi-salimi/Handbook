در درس پیش دیدیم که چطور می‌توان یک `private variable` ساخت. 

حال می‌گوییم که با همین قائده می‌توان `private method` هم ساخت.

به مثال زیر توجه کنید:
```
class Computer:
	def __init__(self):
		self.a = 10
		self._b = 20
		self.__c = 30
		
	def public_process(self):
		self.__c
		print("public")
		
	def __private_method(self):
		print("private")
		
pc = Computer()
pc.public_process()
pc.__private_method()

# output:
public
    pc.__private_method()
    ^^^^^^^^^^^^^^^^^^^
AttributeError: 'Computer' object has no attribute '__private_method'
```

توضیحات:
اولین متد صدا زده شده به درستی اجرا می‌شود اما متد دوم را وقتی صدا می‌زنیم ، به ما خروجی نداده و خطا می‌دهد زیرا به ما اجازه‌ی دسترسی نمی‌دهد.

اما امکان دسترسی بصورت محدود و مشروط وجود دارد؛ برای مثال:
```
class Computer:
	def __init__(self):
		self.a = 10
		self._b = 20
		self.__c = 30
		
	def public_process(self):
		self.__c
		print("public")
		self.__private_method()
		
	def __private_method(self):
		print("private")
		
pc = Computer()
pc.public_process()


# output:
public
private
```
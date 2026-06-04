مثال زیر ، نحوه‌ی ساخت یک دکوراتور را نشان می‌دهد:
```
def decor(func):
	def wrapper():
		print("before")
		print(func())
		print("after")
	return wrapper # returns an object - without ()

def greetings():
	return "Hello"

say_hello = decor(greetings) # wrapper object
say_hello()

# output:
before
Hello
after
```


همچنین به فرق ریز زیر هم توجه کنید:
```
def decor(func):
	def wrapper():
		print("before")
		print(func())
		print("after")
	return wrapper()

def greetings():
	return "Hello"

decor(greetings)

# output:
before
Hello
after
```

مثال بالا (یک مثال با دو صورت مختلف (اما تفاوت کوچک)) شکل ساده‌ی ساخت و اعمال و اجرای یک دکوراتور را نمایش می‌دهد؛ 

اما در پایتون برای آنکه آن را ساده‌تر، بهتر و حرفه‌ای‌تر انجام و نشان دهند، به صورت زیر عمل می‌کنند:

علامت @ را برایش اختصاص داده که پس از آن نام wrapper (در بر گیرنده) یا decorator را وارد کرده ، و در خط بعدی تابع را قرار می‌دهیم؛

اینگونه بصورت خودکار، تابع موجود در خط بعد از دکوراتور، بعنوان آرگومان وارد دکوراتور شده و از آنجا اجرا می‌شود.

بصورت شهودی منظور ما این است:
```
@decorator/wrapper
def func():
	...
```

به مثال زیر توجه کنید:
```
def decor(func):
	def wrapper():
		print("before")
		func()
		print("after")
	return wrapper    # returns an object - without ()
	
@decor
def greetings():
	print("Hello")
	
greetings()

# output:
before
Hello
after
```

این نوع نوشتن بسیار ساده‌تر، تمیزتر، زیباتر و حرفه‌ای‌تر است.
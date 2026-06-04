به مثال زیر دقت کنید:
```
class Car:
	def __init__(self):
		self.a = 10
		self._b = 20   # private variable
		self.__c = 30  # private variable
		
bmw = Car()

print(bmw.a)
print(bmw._b)
print(bmw.__c)

# output:
10
20

    print(bmw.__c)
          ^^^^^^^
AttributeError: 'Car' object has no attribute '__c'
```

توضیحات:

عبارت `print(bmw.a)` مانند همیشه بصورت خیلی عادی اجرا شده و خروجی می‌دهد.

عبارت `print(bmw._b)` نشانگر `b_` مشخص می‌کند که این attribute یک attribute خصوصی (private) است؛ اما بطور عملی ما را محدود نمی‌کند بلکه این یک قرارداد برای برنامه نویس‌هاست که وقتی آن را ببینند، بدانند که private است.

اما عبارت `print(bmw.__c)` بدلیل نشانگر `c__` مشخص می‌کند که یک attribute خصوصی است که بطور عملی از سوی پایتون ، دسترسی به آن را محدود می‌کند و اگر قصد تغییر و دسترسی به آن را داشته باشیم، خطا دریافت خواهیم کرد. همانطور که در مثال بالا می‌بینید.

#### اما چگونه می‌توانیم با `private variable` ها کار کنیم؟
برای کار با چنین متغیرهایی که دسترسی به آن‌ها محدود شده می‌توانیم از توابعی که اجازه‌ی دسترسی و کار با چنین متغیرهایی که فضای خاص و محدودی دارند را تعریف کنیم؛

به چنین متد (توابع) هایی ، متد‌ (توابع) های **getter** و **setter** می‌گویند. 

مانند:
```
class Car:
	def __init__(self):
		self.color = "red"
		self.__speed = 200
	
	# setter
	def set_speed(self, new_speed):
		self.__speed = new_speed
		
	# getter
	def get_speed(self):
		return self.__speed
		
bmw = Car()
print(bmw.get_speed())
bmw.set_speed(1000)
print(bmw.get_speed())

# output:
200
1000
```

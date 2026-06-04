### تمرین:
- یک کلاس Person با ویژگی های name و age ایجاد کنید.
- یک متد ()display ایجاد کنید که name و age یک شی ایجاد‌شده از طریق کلاس Person را نمایش دهد.
- یک کلاس فرزند Student ایجاد کنید که از کلاس Person خصوصیاتش را به ارث می‌برد و علاوه بر آن یک پارامتر دیگر major را نیز به عنوان ورودی میپذیرد.
- یک متد ()displayStudent ایجاد کنید که name ،age و major یک instance ایجاد‌شده از طریق کلاس Student را نمایش‌دهد.

### پاسخ:
```
class Person:
	def __init__(self, name, age):
		self.name = name
		self.age = age

	def display(self):
		return f"{self.name} {self.age}"

class Student(Person):
	def __init__(self, name, age, major):
		super().__init__(name, age)
		self.major = major

	def display_student(self):
		return f"Name: {self.name} - Age: {self.age} - Major: {self.major}"


p1 = Student("Milad Salimi", 22, "4th year")
print(p1.display_student())

# output:
Name: Milad Salimi - Age: 22 - Major: 4th year
```

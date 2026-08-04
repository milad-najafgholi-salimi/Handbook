# Problem:

![pic-1-problem](Usefull/Linked/LeetCode/Linked/Arrays/Two%20Sum/Linked/Problem/1.png)

![pic-2-problem](Usefull/Linked/LeetCode/Linked/Arrays/Two%20Sum/Linked/Problem/2.png)

# My Solution:

![pic-1-my_solution](Usefull/Linked/LeetCode/Linked/Arrays/Two%20Sum/Linked/My_Solution/1.png)

**Time Complexity:** O(n²)  
**Space Complexity:** O(1)
# LeetCode Solutions:

![pic-1](Usefull/Linked/LeetCode/Linked/Arrays/Two%20Sum/Linked/LeetCode_Solution/1.png)

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[j] == target - nums[i]:
                    return [i, j]
        # Return an empty list if no solution is found
        return []
```

![pic-2](Usefull/Linked/LeetCode/Linked/Arrays/Two%20Sum/Linked/LeetCode_Solution/2.png)

---
توضیح خط زیر:
```
if nums[j] == target - nums[i]:
```

ریاضی ساده است. در حقیقت جبر ساده‌ی کلاس هفتم است. معادل این خط، کد زیر است که در راه حل خودم استفاده کرده‌ام:
```
if nums[i] + nums[j] == target:
```

---

![pic-3](Usefull/Linked/LeetCode/Linked/Arrays/Two%20Sum/Linked/LeetCode_Solution/3.png)

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i in range(len(nums)):
            hashmap[nums[i]] = i
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap and hashmap[complement] != i:
                return [i, hashmap[complement]]
        # If no valid pair is found, return an empty list
        return []
```

![pic-4](Usefull/Linked/LeetCode/Linked/Arrays/Two%20Sum/Linked/LeetCode_Solution/4.png)

نکته آموزشی که یاد گرفتم:
>اگر یک key-value pair در دیکشنری وجود داشته باشد، و در طول پروسه‌ی برنامه، همان key-value pair مشابه تولید شده و به دیکشنری اضافه شود، نه دیکشنری خطا خواهد داد و نه اضافه خواهد شد؛ بلکه **بازنویسی Overwrite** خواهد شد. همچنین اگر یک key-value pair وجود داشته باشد و در طول پروسه، یک key-value pair تولید شود که کلید یکسان اما value متفاوت داشته باشد، باز هم key-value pair با دیتای جدید بازنویسی Overwrite می‌شود. 

توضیح خط زیر:
```
for i in range(len(nums)):
            hashmap[nums[i]] = i
```

دیکشنری hashmap بصورت زیر خواهد بود:
```
{2: 0, 3: 1, 1: 2, 4: 3, 5: 4}
```

اما پرسش اساسی من خط زیر است:
```
for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap and hashmap[complement] != i:
```

شاید با خودت بگویی:

> چرا روی خود `nums` حلقه نزده است؟ چرا روی `range(len(nums))` حرکت کرده؟

پاسخ این است که **مسئله‌ی Two Sum خروجی را به صورت اندیس‌ها (indices) می‌خواهد، نه خود اعداد.** پس به این دلیل روی رنج حرکت کردیم تا اندیس را داشته باشیم.
برای همین hashmap را به آن صورت ذخیره کردیم که دیدی.

توضیح بیشتر خط زیر:
```
complement = target - nums[i]
```

تارگت را که می‌دانیم؛ `nums[i]` در آرایه nums به دنبال ایندکس i می‌گردد و خود عدد را از آرایه nums می‌آورد. سپس با تفاضل، متمم را حساب می‌کند؛ سپس اگر متمم در hashmap بعنوان کلید موجود بود، value آن کلید را که همان ایندکس آن است را بر می‌گرداند. همچنین این شرط هم وجود دارد که نباید آن کلید با 

---

![pic-5](Usefull/Linked/LeetCode/Linked/Arrays/Two%20Sum/Linked/LeetCode_Solution/5.png)

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap:
                return [i, hashmap[complement]]
            hashmap[nums[i]] = i
        # Return an empty list if no solution is found
        return []
```

![pic-6](Usefull/Linked/LeetCode/Linked/Arrays/Two%20Sum/Linked/LeetCode_Solution/6.png)

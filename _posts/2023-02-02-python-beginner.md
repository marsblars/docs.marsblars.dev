---
layout: post
title: "Solving Beginner Level Python Problems"
date: 2023-02-02 21:36:00 -0100
categories: [Academics]
tags: [python,beginner]
---

> Here are a few beginner-level problems in Python that you can try solving:
>1. Calculate the factorial of a number.
>2. Check if a number is prime or not.
>3. Print the first n Fibonacci numbers.
>4. Convert Celsius to Fahrenheit and vice versa.
>5. Generate a random password of a specified length.
>6. Count the number of occurrences of each character in a string.
>7. Check if a string is a palindrome or not.
>8. Reverse a string.
>9. Print the multiplication table for a given number.
>10. Check if a given year is a leap year or not.

>Remember to break down the problem into smaller parts and try to understand the steps involved before writing code. Good luck!
{: .prompt-tip }

## Breaking Problems Into Psuedocode:

1. **Calculate the factorial of a number:**
    - Take an input number from the user.
    - Create a variable `result` to store the factorial result and initialize it to 1.
    - Use a loop to iterate through all the numbers up to the input number.
    - Multiply each number with `result` in each iteration and update the value of `result`.
    - After the loop, print the value of `result`.

2. **Check if a number is prime or not:**
    - Take an input number from the user.
    - Check if the input number is equal to 2, then print "Prime".
    - If the input number is less than 2, then print "Not Prime".
    - Otherwise, use a loop to iterate through all the numbers up to the square root of the input number.
    - For each number, check if the input number is divisible by it.
    - If the input number is divisible by any of the numbers, print "Not Prime".
    - If the input number is not divisible by any of the numbers, print "Prime".

3. **Print the first n Fibonacci numbers:**
    - Take an input number from the user to determine the number of Fibonacci numbers to be printed.
    - Initialize two variables `a` and `b` to 0 and 1 respectively.
    - Use a loop to iterate `n` times.
    - In each iteration, calculate the sum of `a` and `b`, and store it in a variable `c`.
    - Update the values of `a` and `b` to `b` and `c` respectively.
    - Print the value of `a` in each iteration.

4. **Convert Celsius to Fahrenheit and vice versa:**
    - Take an input temperature and the unit (Celsius or Fahrenheit) from the user.
    - If the unit is "Celsius", then use the formula `F = (9/5)C + 32` to convert the temperature to Fahrenheit.
    - If the unit is "Fahrenheit", then use the formula `C = (F - 32) * 5/9` to convert the temperature to Celsius.
    - Print the converted temperature.

5. **Generate a random password of a specified length:**
    - Take an input length from the user to determine the length of the password.
    - Import the `random` module to generate random characters.
    - Use a loop to iterate `n` times, where `n` is the length of the password.
    - In each iteration, generate a random character using the `random.choice` method and add it to a string.
    - Repeat the previous two steps until the string is of the desired length.
    - Print the password.

6. **Count the number of occurrences of each character in a string:**
    - Take a string as input from the user.
    - Create an empty dictionary to store the count of each character.
    - Use a loop to iterate through each character in the string.
    - For each character, check if it exists in the dictionary.
    - If it exists, increment its count by `1`.
    - If it doesn't exist, add it to the dictionary with count `1`.
    - After the loop, print the character and its count for each key-value pair in the dictionary.

7. **Check if a string is a palindrome or not:**
    - Take a string as input from the user.
    - Convert the string to lowercase to make it case-insensitive.
    - Use a loop to iterate through the characters in the string.
    - In each iteration, compare the first and last characters, then the second and second-last characters, and so on.
    - If any of the characters don't match, print `Not Palindrome`.
    - If all of the characters match, print `Palindrome`.

8. **Reverse a string:**
    - Take a string as input from the user.
    - Create an empty string to store the reversed string.
    - Use a loop to iterate through the characters in the string from the end to the beginning.
    - In each iteration, add the current character to the reversed string.
    - After the loop, print the reversed string.

9. **Print the multiplication table for a given number:**
    - Take a number as input from the user.
    - Use a loop to iterate through the numbers from `1` to `10`.
    - In each iteration, multiply the input number with the current number and print the result.

10. **Check if a given year is a leap year or not:**
    - Take a year as input from the user.
    - If the year is divisible by `4`, check if it is divisible by `100`.
    - If the year is divisible by `100`, check if it is divisible by `400`.
    - If the year is divisible by `400`, print `Leap Year`.
    - If the year is divisible by `4` and not divisible by `100`, print `Leap Year`.
    - Otherwise, print `Not Leap Year`.

## Solving Each Problem:

1. **Calculate the factorial of a number:**

```python
def factorial(n):
    result = 1
    for i in range(1, n+1):
        result *= i
    return result

num = int(input("Enter a number: "))
print("The factorial of", num, "is", factorial(num))
```

1. **Check if a number is prime or not:**

```python
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5)+1):
        if n % i == 0:
            return False
    return True

num = int(input("Enter a number: "))
if is_prime(num):
    print(num, "is prime")
else:
    print(num, "is not prime")
```

3. **Print the first n Fibonacci numbers:**

```python
def fibonacci(n):
    a, b = 0, 1
    for i in range(n):
        print(a)
        a, b = b, a + b

num = int(input("Enter the number of Fibonacci numbers: "))
fibonacci(num)
```

4. **Convert Celsius to Fahrenheit and vice versa:**

```python
def convert_temperature(temp, unit):
    if unit == "Celsius":
        return (9/5)*temp + 32
    elif unit == "Fahrenheit":
        return (temp - 32) * 5/9
    else:
        return "Invalid unit"

temp = float(input("Enter the temperature: "))
unit = input("Enter the unit (Celsius or Fahrenheit): ")
converted_temp = convert_temperature(temp, unit)
print("The converted temperature is: ", converted_temp)

```

5. **Generate a random password of a specified length:**

```python
import random
import string

def generate_password(length):
    characters = string.ascii_letters + string.digits + string.punctuation
    password = ''.join(random.choice(characters) for i in range(length))
    return password

length = int(input("Enter the length of the password: "))
password = generate_password(length)
print("The generated password is: ", password)
```

6. **Count the number of occurrences of each character in a string:**

```python
string = input("Enter a string: ")
char_count = {}
for char in string:
    if char in char_count:
        char_count[char] += 1
    else:
        char_count[char] = 1

print("Character Count:")
for char, count in char_count.items():
    print(char, count)
```

7. **Check if a string is a palindrome or not:**

```python
string = input("Enter a string: ").lower()
is_palindrome = True
for i in range(len(string) // 2):
    if string[i] != string[-(i + 1)]:
        is_palindrome = False
        break

if is_palindrome:
    print("Palindrome")
else:
    print("Not Palindrome")
```

8. **Reverse a string:**

```python
string = input("Enter a string: ")
reversed_string = ""
for i in range(len(string) - 1, -1, -1):
    reversed_string += string[i]

print("Reversed String:", reversed_string)
```

9. **Print the multiplication table for a given number:**

```python
number = int(input("Enter a number: "))
for i in range(1, 11):
    print(number, "x", i, "=", number * i)
```

10. **Check if a given year is a leap year or not:**

```python
year = int(input("Enter a year: "))
if year % 400 == 0 or (year % 4 == 0 and year % 100 != 0):
    print("Leap Year")
else:
    print("Not Leap Year")
```

## Conclusion
In conclusion, the previous responses provided an explanation of ten beginner-level problems in Python and the steps involved in solving each one. 

The key takeaways from these problems are:
- Breaking a problem down into smaller parts and understanding the steps involved in solving each part.
- Using various programming constructs such as loops, conditions, and dictionaries to solve the problems.
- Getting comfortable with reading and processing user input.
- Understanding the use of mathematical operations, string manipulation, and type conversion in Python.

By solving these beginner-level problems, one can gain a solid foundation in Python programming and be well on their way to solving more complex problems in the future.

### Variables, Data Types & Arithmetic

1. Take two numbers as input and print their sum, difference, product, quotient, and remainder.
2. Swap two variables' values without using a third variable (hint: use arithmetic).
3. Convert temperature from Celsius to Fahrenheit and vice versa.
4. Calculate the simple interest given principal, rate, and time.
5. Given a 3-digit number, extract and print each digit separately (hint: use `/` and `%`).

### Conditional Branching (if/else)

1. Check if a number is even or odd.
2. Check if a year is a leap year.
3. Find the largest of three numbers.
4. Check if a triangle is valid, given three angles (they must sum to 180).
5. Build a simple grading system: take marks as input, print grade (A/B/C/F) using `else if`.

### Loops (for / while)

1. Print all even numbers from 1 to 50.

2. Find the sum of digits of a number (e.g., 123 → 1+2+3 = 6).

3. Check if a number is prime.

4. Print the multiplication table of a number entered by the user.

5. Calculate factorial of a number.

6. Reverse a number (e.g., 123 → 321).

   ```C
   #include <stdio.h>
   
   int main() {
       int number, digit, reversed = 0;
   
       printf("Enter a number: ");
       scanf("%d", &number);
   
       while (number != 0) {
           digit = number % 10;        // extract last digit
           reversed = reversed * 10 + digit;  // build reversed number
           number = number / 10;        // remove last digit from number
       }
   
       printf("Reversed number: %d\n", reversed);
   
       return 0;
   }
   
   #include <stdio.h>
   
   int main() {
       int number, digit;
   
       printf("Enter a number: ");
       scanf("%d", &number);
   
       printf("Reversed: ");
       while (number != 0) {
           digit = number % 10;   // extract last digit
           printf("%d", digit);    // print it immediately
           number = number / 10;    // remove last digit
       }
       printf("\n");
   
       return 0;
   }
   ```

7. Check if a number is a palindrome (reads same forwards and backwards, e.g., 121).

8. Generate the Fibonacci sequence up to N terms.

9. Keep asking the user for numbers and print their running total, until they type `-1` to stop.

### Arrays

1. Find the largest and smallest element in an array.
2. Calculate the sum and average of elements in an array.
3. Reverse an array in place.
4. Count how many even and odd numbers are in an array.
5. Find the second-largest element in an array.

### Char Arrays / Strings

1. Count the number of vowels in a string.
2. Check if a string is a palindrome (e.g., "madam").
3. Count the length of a string **without** using `strlen()`.
4. Reverse a string **without** using a library function.
5. Count how many times a specific character appears in a string.

### Functions

1. Write a function `isPrime(int n)` that returns 1 or 0, then use it in a loop to print all primes between 1 and 100.
2. Write a function to calculate the power of a number (`power(base, exponent)`) without using `pow()`.
3. Write separate functions for addition, subtraction, multiplication, division, and call them from `main()` based on user's menu choice.
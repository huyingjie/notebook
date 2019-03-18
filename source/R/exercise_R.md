# Excercise for R

* What is the sum of the first n positive integers?

  We can use the formula n(n+1)/2 to quickly compute this quantity.

  Instructions:

  * Define 'n=100'

  * Then use R to compute the sum of 1 through 100 using the formula n(n+1)/2. What is the sum?

  Knowledge: Using variables


  ```r
  # Here is how you compute the sum for the first 20 integers
  20*(20+1)/2

  # However, we can define a variable to use the formula for other values of n
  n <- 20
  n*(n+1)/2

  n <- 25
  n*(n+1)/2

  # Below, write code to calculate the sum of the first 100 integers

  n <- 100
  n*(n+1)/2
  ```

* What is the sum of the first 1000 positive integers?

  We can use the formula n(n+1)/2 to quickly compute this quantity.

  Knowledge: Using variables

  ```r
  # Below, write code to calculate the sum of the first 1000 integers
  n <- 1000
  n*(n+1)/2
  ```

* Use one line of code to compute the log, to the base 10, of the square root of 100.
  Make sure your code includes the `log10` and `sqrt` functions.

  knowledge: Nested function calls

  ```r
  log10(sqrt(100))
  ```
* Which of the following will always return the numeric value stored in x?

  Knowledge: Using variables


  * log(10^x)
  * log10(x^10)
  - log(exp(x))
  * exp(log(x, base = 2))

  Answer: log(exp(x))

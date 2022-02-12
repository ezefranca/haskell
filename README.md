# haskell


** Mac M1:
https://www.youtube.com/watch?v=zeZkgIrGKeY

** VSCode
https://medium.com/@dogwith1eye/setting-up-haskell-in-vs-code-with-stack-and-the-ide-engine-81d49eda3ecf

Expressions
In almost all programming languages you can create expressions such as:
```swift
 (b*b-4*a*c)/2*a
 ```
and you can assign these expressions to variables:
```haskell
v = (b*b-4*a*c)/2*a
```
In Haskell, you can do this as well, and what’s more: expressions are really all there is, there are no statements.

Functions
In Python, you can define a function such as
```python
def hello(name):
    return "Hello, "+name
```
In Haskell you can write this simply as:
```haskell
hello name = "Hello, "++name
 ```
Types
C has types, for example:
```c
int f (int x, int y) {
  return x*y+x+y;
 }
 ```
Haskell has much more powerful types than C, and we will talk a lot about types:
```haskell
    f :: Int -> Int -> Int
    f x y =  x*y+x+y
```
Lists
In many languages, e.g. Python, JavaScript, Ruby, … you can create lists such as:
```javascript
    lst = [ "A", "list", "of", "strings"]
 ```
Haskell also uses this syntax for lists.

To join lists, in Python you could write
```python
lst = [1,2] + [3,4]
```
In Haskell this would be very similar:

    lst = [1,2] ++ [3,4]
Anonymous functions
In JavaScript you can define anonymous functions (functions without a name) such as:

    var f = function(x,y){return x*y+x+y};
In Haskell, such anonymous functions are called lambda functions and they are actually the basis of the language. Again, the syntax is very compact:
```haskell
    f = \x y -> x*y+x+y
```
Higher-order functions
Finally, in many languages, functions can operate on functions. For example, in Perl you can modify the elements in a list using:
```pearl
    map sub ($x){$x*2+1}, [1..10]
```
Haskell provides many of these so-called higher-order functions, and lets you define your own.
```haskell
    map (\x -> x*2+1) [1..10]
```

## 2

Expressions
Haskell has no statements, only expressions!

In an imperative language like C or Java,
there are expressions that denote small scale computations (2*x), and
statements that handle sequencing, looping, conditionals, and all the large scale operation of the program.
Pure functional programming languages don’t have any statements — no assignments, no jumps.
Instead, all computation is performed by evaluating expressions
So, let’s start with expressions!
(We’ll still be working on expressions at the end of the course, since that’s all there is.)
Examples of integer expressions

An expression evaluates to a result (usually written 
e
⇝
r
 but we’ll use e -- > r). Haskell uses a similar notation for numbers and operators as most languages:

    2 -- > 2
    3+4 -- > 7
    3+4*5    {equivalent to 3+(4*5)} -- > 23
    (3+4)*5   {equivalent to 7*5} -- > 35
Syntax of expressions

Parentheses are used for grouping, just as in mathematics.
If you don’t need parentheses for grouping, they are optional.
Operators have precedence, e.g. 
 
∗
 
 has “tighter” precedence than 
 
+
 
, so 
2
 
+
 
3
 
∗
 
4
 means 
2
 
+
 
(
3
 
∗
 
4
)
.
Use the reference documentation for complete list of operators and their precedences, if you need them.
Function applications

Expressions can contain function calls.
A function takes argument(s), performs some computation, and produces result(s).
The function abs gives the absolute value of a number.
To use a function, you apply it to an argument. Write the function followed by the argument, separated by a space.
  abs 5 -- > 5
  abs (-6) -- > 6
Parentheses are for grouping

Good style

  2+3*5
  2+(3*5) -- might be clearer to some readers
  abs 7
You don’t need parentheses. The following are legal, but they look silly:

    (2) + ((3+(((((5)))))))
    abs (5)
    abs (((5)))
Functions with several arguments

min and max are functions that take two arguments.
The arguments are given after the function, separated by whitespace.
Write min 3 8, don’t write min(3, 8);
    min 3 8 -- > 3

    max 3  8 -- > 8
Precedence of function application

Function application binds tighter than anything else.
So f x + 3 means (f x) + 3 and not f (x+3)
If an argument to a function is an expression, you’ll need to put it in parentheses.
Equations
Equations give names to values

Equations are used to give names to values.
answer = 42
An equation in Haskell is a mathematical equation: it says that the left hand side and the right hand side denote the same value.
The left hand side should be a name that you’re giving a value to.
Correct: x = 5*y
Incorrect: 2 * x = (3*x)**2 – Reassignment is not allowed in a pure FPL
Equations are not assignments

A name can be given only one value.
Names are often called “variables”, but they do not vary.
In Haskell variables are constant!
    n = 1    -- just fine!
    x = 3*n  -- fine
    n = x    -- Wrong: can have only one definition of n
Once you give a value to a name, you can never change it!
This is part of the meaning of “pure” and “no side effects”
What about n = n+1?

In imperative languages, we frequently say n := n + 1
This is an assignment, not an equation!
It means (1) compute the right hand side, using the old value of n; then (2) discard the old value of n and overwrite it with the new value.
There are no equations in imperative languages like C and Java.
In Haskell, it is valid to write n = n + 1.
This is an equation, not an assignment!
It means: compute the value of n that has the property that n = n + 1.
Haskell will try, and it will fail.
How can you compute without assignments?

Think of an assignment statement as doing three things:
It evaluates the right hand side: computing a useful value.
It discards the value of the variable on the left hand side: destroying a value that might or might not be useful.
It saves the useful value of the RHS into the variable.
In a pure functional language
We never destroy old values.
We just compute new useful ones.
If the old value was truly useless, the garbage collector will reclaim its storage.


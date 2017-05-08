---
title: "Writing Functions"
teaching: 15
exercises: 15
questions:
- "How can I create my own functions?"
objectives:
- "Explain and identify the difference between function definition and function call."
- "Write a function that takes a small, fixed number of arguments and produces a single result."
keypoints:
- "Break programs down into functions to make them easier to understand."
- "Define a function using `def` with a name, parameters, and a block of code."
- "Defining a function does not run it."
- "Arguments in a function *call* are matched to parameters in function *definition*."
- "Functions may return a result to their caller using `return`."
---
## Break programs down into functions to make them easier to understand.

*   Human beings can only keep a few items in working memory at a time.
*   Understand larger/more complicated ideas by understanding and combining pieces.
    *   Components in a machine.
    *   Lemmas when proving theorems.
*   Functions serve the same purpose in programs.
    *   *Encapsulate* complexity so that we can treat it as a single "thing".
*   Also enables *re-use*.
    *   Write one time, use many times.

## Define a function using `def` with a name, parameters, and a block of code.

*   Begin the definition of a new function with `def`.
*   Followed by the name of the function.
    *   Must obey the same rules as variable names.
*   Then *parameters* in parentheses.
    *   Empty parentheses if the function doesn't take any inputs.
    *   We will discuss this in detail in a moment.
*   Then a colon.
*   Then an indented block of code.

~~~
def print_greeting():
    print('Hello!')
~~~
{: .python}

## Defining a function does not run it.

*   Defining a function does not run it.
    *   Like assigning a value to a variable.
*   Must call the function to execute the code it contains.

~~~
print_greeting()
~~~
{: .python}
~~~
Hello!
~~~
{: .output}

## The arguments in a function *call* are matched to the parameters in function *definition*.

*   Functions are most useful when they can operate on different data.
*   Specify *parameters* when defining a function.
    *   These become variables when the function is executed.
    *   The values of incoming arguments are assigned to these variables in order.

~~~
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(1871, 3, 19)
~~~
{: .python}
~~~
1871/3/19
~~~
{: .output}

*   A cleaver way to think about this is that the
    `()` contains the ingredients for the function
    while the body contains the recipe ([via Twitter](https://twitter.com/minisciencegirl/status/693486088963272705)).

## Functions may send back a result using the `return` statement.

*   Use `return ...` to give a value back to the caller.
*   May occur anywhere in the function, but...
*   Functions are easier to understand if `return` occurs:
    *   Near the beginning to handle special cases.
    *   At the very end, with a final result.

~~~
def average(values):
    if len(values) == 0:
        return None
    output = sum(values) / len(values)
    return output
~~~
{: .python}

~~~
a = average([1, 3, 4])
print('average of actual values:', a)
~~~
{: .python}
~~~
2.6666666666666665
~~~
{: .output}

~~~
print('average of empty list:', average([]))
~~~
{: .python}
~~~
None
~~~
{: .output}

## Remember that every function returns something, even if 'something' equals `None`
*   A function that doesn't explicitly `return` a value automatically returns `None`.

~~~
def greeting(message):
    print(message)

result = greeting("Hello World!)
print('The result of the call to greeting is:', result)
~~~
{: .python}
~~~
Hello World!
The result of the call to greeting is: None
~~~
{: .output}

> ## Definition and Use
>
> What does the following program print?
>
> ~~~
> def report(pressure):
>     print('The pressure is', pressure)
>
> report(22.5)
> ~~~
> {: .python}
{: .challenge}

> ## Order of Operations
>
> The following code is written given the function in the previous example
>
> ~~~
> result = report(22.5)
> print('result of call is:', result)
> ~~~
> {: .python}
>
> The output is:
>
> ~~~
> The pressure is 22.5
> result of call is: None
> ~~~
> {: .output}
>
> Explain why the two lines of output appeared in the order they did.
{: .challenge}

> ## Encapsulation
>
> Fill in the blanks to create a function that calculates the area
> of a circle
>
> ~~~
> import math
>
> def area_of_circ(____):
>     area = math.______ * _____ ** 2
>     return ____
> ~~~
> {: .python}
>
> > ## Hint
> >
> > The formula for area is pi * radius ^ 2
> {: .solution}
>
> > ## Solution
> >
> > ~~~
> > import math
> >
> > def area_of_circ(radius):
> >     area = math.pi * radius ** 2
> >     return area
> > ~~~
> > {: python}
> {: .solution}
{: .challenge}

> ## Calling by Name
>
> What does this short program print?
>
> ~~~
> def print_date(year, month, day):
>     joined = str(year) + '/' + str(month) + '/' + str(day)
>     print(joined)
>
> print_date(day=1, month=2, year=2003)
> ~~~
> {: .python}
>
> 1.  Why do you think it's okay to call the arguments in a different order like this?
> 2.  When and why is it useful to call functions this way?
{: .challenge}

> ## Encapsulating a for-loop
>
> Write a function that sings '99 bottles of beer on the wall', for however
> many verses the singer wishes to sing it
>
> > ## Solution
> >
> > ~~~
> >
> > def bottles_of_beer(num_bottles):
> >     for bottle in range(1, num_bottles):
> >         print(bottle, "bottles of beer on the wall")
> >         print(bottle, "bottles of beer")
> >         print("Take one down and pass it around")
> >         print(bottle - 1, "bottles of beer on the wall\n")
> >
> > bottles_of_beer(4)
> > ~~~
> > {: python}
> {: .solution}
{: .challenge}

> ## Identifying Syntax Errors
>
> 1. Read the code below and try to identify what the errors are
>    *without* running it.
> 2. Run the code and read the error message.
>    Is it a `SyntaxError` or an `IndentationError`?
> 3. Fix the error.
> 4. Repeat steps 2 and 3 until you have fixed all the errors.
>
> ~~~
> def another_function
>   print("Syntax errors are annoying.")
>    print("But at least python tells us about them!")
>   print("So they are usually not too hard to fix.")
> ~~~
> {: .python}
>
> 
> > ## Solution
> >
> > > ~~~
> > > def another_function():
> > >     print("Syntax errors are annoying.")
> > >     print("But at least python tells us about them!")
> > >     print("So they are usually not too hard to fix.")
> > > ~~~
> > {: .python}
> {: .solution}
{: .challenge}
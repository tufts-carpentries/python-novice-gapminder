---
title: "Variables and Assignment"
teaching: 15
exercises: 10
questions:
- "How can I store data in programs?"
objectives:
- "Write programs that assign scalar values to variables and perform calculations with those values."
- "Correctly trace value changes in programs that use scalar assignment."
keypoints:
- "Use variables to store values."
- "Use `print` to display values."
- "Variables persist between cells."
- "Variables must be created before they are used."
- "Variables can be used in calculations."
- "Use an index to get a single character from a string."
- "Use a slice to get a substring."
- "Use the built-in function `len` to find the length of a string."
- "Python is case-sensitive."
- "Use meaningful variable names."
- "Use comments to add documentation to programs."
---
## Use variables to store values.

*   Variables are names for values.
*   In Python the `=` symbol assigns the value on the right to the name on the left.
*   The variable is created when a value is assigned to it.
*   Here, Python assigns an age to a variable `age`
    and a name in quotation marks to a variable `first_name`.

~~~
age = 42
first_name = 'Ahmed'
~~~
{: .python}

*   Variable names:
    *   cannot start with a digit
    *   cannot contain spaces, quotation marks, or other punctuation
    *   *may* contain an underscore (typically used to separate words in long variable names)
*   Underscores at the start like `__alistairs_real_age` have a special meaning
    so we won't do that until we understand the convention.

## Use `print` to display values.

*   Python has a built-in function called `print` that prints things as text.
*   Call the function (i.e., tell Python to run it) by using its name.
*   Provide values to the function (i.e., the things to print) in parentheses.
*   The values passed to the function are called 'arguments'

~~~
print(first_name, 'is', age, 'years old')
~~~
{: .python}
~~~
Ahmed is 42 years old
~~~
{: .output}

*   `print` automatically puts a single space between items to separate them.
*   And wraps around to a new line at the end.

## Variables must be created before they are used.

*   If a variable doesn't exist yet, or if the name has been mis-spelled,
    Python reports an error.
    *   Unlike some languages, which "guess" a default value.

~~~
print(last_name)
~~~
{: .python}
~~~
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-c1fbb4e96102> in <module>()
----> 1 print(last_name)

NameError: name 'last_name' is not defined
~~~
{: .error}

*   The last line of an error message is usually the most informative.
*   We will look at error messages in detail [later]({{ page.root }}/05-error-messages/).

> ## Variables Persist Between Cells
> Variables defined in one cell exist in all other cells once executed,
> so the relative location of cells in the notebook do not matter
> (i.e., cells lower down can still affect those above).
> Remember: Notebook cells are just a way to organize a program:
> as far as Python is concerned,
> all of the source code is one long set of instructions.
{: .callout}

## Variables can be used in calculations.

*   We can use variables in calculations just as if they were values.
    *   Remember, we assigned 42 to `age` a few lines ago.

~~~
age = age + 3
print('Age in three years:', age)
~~~
{: .python}
~~~
Age in three years: 45
~~~
{: .output}

## Variables can be re-assigned
*   A variable’s value can be replaced with another value by using the assignment operator again.

~~~
first = 1
second = 5 * first
first = 2
print('first is', first, 'and second is', second)
~~~
{: .python}
~~~
first is 2 and second is 5
~~~
{: .output}

*   The computer reads the value of `first` when doing the multiplication,
    creates a new value, and assigns it to `second`.
*   After that, `second` does not remember where it came from.

## Python is case-sensitive.

*   Python thinks that upper- and lower-case letters are different,
    so `Name` and `name` are different variables.
*   There are conventions for using upper-case letters at the start of variable names
    so we will use lower-case letters for now.

## Use meaningful variable names.

*   Python doesn't care what you call variables as long as they obey the rules
    (alphanumeric characters and the underscore).

~~~
flabadab = 42
ewr_422_yY = 'Ahmed'
print(ewr_422_yY, 'is', flabadab, 'years old')
~~~
{: .python}

*   Use meaningful variable names to help other people understand what the program does.
*   The most important "other person" is your future self.

## Use comments to add documentation to programs.

~~~
# This sentence isn't executed by Python.
adjustment = 0.5   # Neither is this - anything after '#' is ignored.
print(adjustments)
~~~
{: .python}


~~~
0.5
~~~
{: .output}

> ## Swapping Values
>
> Draw a table showing the values of the variables in this program
> after each statement is executed.
> In simple terms, what do the last three lines of this program do?
>
> ~~~
> lowest = 1.0
> highest = 3.0
> temp = lowest
> lowest = highest
> highest = temp
> ~~~
> {: .python}
{: .challenge}

> ## Predicting Values
>
> What is the final value of `position` in the program below?
> (Try to predict the value without running the program,
> then check your prediction.)
>
> ~~~
> initial = "left"
> position = initial
> initial = "right"
> ~~~
> {: .python}
{: .challenge}

> ## Choosing a Name
>
> Which is a better variable name, `m`, `min`, or `minutes`?
> Why?
> Hint: think about which code you would rather inherit
> from someone who is leaving the lab:
>
> 1. `ts = m * 60 + s`
> 2. `tot_sec = min * 60 + sec`
> 3. `total_seconds = minutes * 60 + seconds`
>
> > ## Solution
> >
> > `minutes` is better because `min` might mean something like "minimum"
> > (and actually does in Python, but we haven't seen that yet).
> {: .solution}
{: .challenge}

> ## What Did You Have For Dinner Last Night?
>
> In a new notebook cell create variables that contain relevant data 
> regarding the "what, where, and when" of last night's dinner, then
> include those variables in a `print()` command as part of a full sentence.
>
> Paste the output into the EitherPad, so we can all vicariously
> enjoy your meal.
{: .challenge}

---
title: "Conditionals"
teaching: 10
exercises: 15
questions:
- "How can programs do different things for different data?"
objectives:
- "Correctly write programs that use if and else statements and simple Boolean expressions (without logical operators)."
- "Trace the execution of unnested conditionals and conditionals inside loops."
keypoints:
- "Use `if` statements to control whether or not a block of code is executed."
- "Conditionals are often used inside loops."
- "Use `else` to execute a block of code when an `if` condition is *not* true."
- "Use `elif` to specify additional tests."
- "Conditions are tested once, in order."
---
## Use `if` statements to control whether or not a block of code is executed.

*   An `if` statement (more properly called a *conditional* statement)
    controls whether some block of code is executed or not.
*   Structure is similar to a `for` statement:
    *   First line opens with `if` and ends with a colon
    *   Body containing one or more statements is indented (usually by 4 spaces)

~~~
mass = 3.54
if mass > 3.0:
    print(mass, 'is large')

mass = 2.07
if mass > 3.0:
    print (mass, 'is large')
~~~
{: .python}
~~~
3.54 is large
~~~
{: .output}

## Conditionals are often used inside loops.

*   Not much point using a conditional when we know the value (as above).
*   But useful when we have a collection to process.

~~~
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
~~~
{: .python}
~~~
3.54 is large
9.22 is large
~~~
{: .output}

## Use `else` to execute a block of code when an `if` condition is *not* true.

*   `else` can be used following an `if`.
*   Allows us to specify an alternative to execute when the `if` *branch* isn't taken.

~~~
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
~~~
{: .python}
~~~
3.54 is large
2.07 is small
9.22 is large
1.86 is small
1.71 is small
~~~
{: .output}

## Use `elif` to specify additional tests.

*   May want to provide several alternative choices, each with its own test.
*   Use `elif` (short for "else if") and a condition to specify these.
*   Always associated with an `if`.
*   Must come before the `else` (which is the "catch all").

~~~
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 9.0:
        print(m, 'is HUGE')
    elif m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
~~~
{: .python}
~~~
3.54 is large
2.07 is small
9.22 is HUGE
1.86 is small
1.71 is small
~~~
{: .output}

## Conditions are tested once, in order.

*   Python steps through the branches of the conditional in order, testing each in turn.
*   So ordering matters.

~~~
grade = 85
if grade >= 70:
    print('grade is C')
elif grade >= 80:
    print('grade is B')
elif grade >= 90:
    print('grade is A')
~~~
{: .python}
~~~
grade is C
~~~
{: .output}

*   Does *not* automatically go back and re-evaluate if values change.

~~~
velocity = 10.0
if velocity > 20.0:
    print('moving too fast')
else:
    print('adjusting velocity')
    velocity = 50.0
~~~
{: .python}
~~~
adjusting velocity
~~~
{: .output}

*   Often use conditionals in a loop to "evolve" the values of variables.

~~~
velocity = 10.0
for i in range(5): # execute the loop 5 times
    print(i, ':', velocity)
    if velocity > 20.0:
        print('moving too fast')
        velocity = velocity - 5.0
    else:
        print('moving too slow')
        velocity = velocity + 10.0
print('final velocity:', velocity)
~~~
{: .python}
~~~
0 : 10.0
moving too slow
1 : 20.0
moving too slow
2 : 30.0
moving too fast
3 : 25.0
moving too fast
4 : 20.0
moving too slow
final velocity: 30.0
~~~
{: .output}

*   The program must have a `print` statement *outside* the body of the loop
    to show the final value of `velocity`,
    since its value is updated by the last iteration of the loop.

> ## Compound Relations Using `and`, `or`, and Parentheses
>
> Often, you want some combination of things to be true.  You can combine
> relations within a conditional using `and` and `or`.  Continuing the example
> above, suppose you have
>
> ~~~
> mass     = [ 3.54,  2.07,  9.22,  1.86,  1.71]
> velocity = [10.00, 20.00, 30.00, 25.00, 20.00]
>
> i = 0
> for i in range(5):
>     if mass[i] > 5 and velocity[i] > 20:
>         print("Fast heavy object.  Duck!")
>     elif mass[i] > 2 and mass[i] <= 5 and velocity[i] <= 20:
>         print("Normal traffic")
>     elif mass[i] <= 2 and velocity <= 20:
>         print("Slow light object.  Ignore it")
>     else:
>         print("Whoa!  Something is up with the data.  Check it")
> ~~~
> {: .python}
>
> Just like with arithmetic, you can and should use parentheses whenever there
> is possible ambiguity.  A good general rule is to *always* use parentheses
> when mixing `and` and `or` in the same condition.  That is, instead of:
>
> ~~~
> if mass[i] <= 2 or mass[i] >= 5 and velocity[i] > 20:
> ~~~
> {: .python}
>
> write one of these:
>
> ~~~
> if (mass[i] <= 2 or mass[i] >= 5) and velocity[i] > 20:
> if mass[i] <= 2 or (mass[i] >= 5 and velocity[i] > 20):
> ~~~
> {: .python}
>
> so it is perfectly clear to a reader (and to Python) what you really mean.
{: .callout}

> ## Tracing Execution
>
> What does this program print?
>
> ~~~
> pressure = 71.9
> if pressure > 50.0:
>     pressure = 25.0
> elif pressure <= 50.0:
>     pressure = 0.0
> print(pressure)
> ~~~
> {: .python}
>
> > ## Hint
> > 
> > The variable '`pressure`' is being updated. Is there any logical way
> > that either the '`if`' or '`elif`' will _not_ evaluate to `True`? Do
> > you think Python would allow _both_ '`if`' and '`elif`' to evaluate 
> > to `True`?
> {: .solution}
>
> > ## Solution
> > 
> > answer: 25.0
> > 
> > 71.9 is greater than 50.0, so the '`if`' statement evaluates to `True`.
> > Once an '`if`' or '`elif`' evaluates to `True` the remaining
> > conditionals are skipped, so even though pressure is now < 50.0, it
> > is not reassigned to 0.0 in the '`elif`' statement.
> {: .solution}
{: .challenge}

> ## Trimming Values
>
> Fill in the blanks.
>
> The `result` should be a new list of 1's and 0's, where positive values 
> are converted to 1's, and negative values are converted to 0's.
>
> ~~~
> original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
> result = ____
> for value in original:
>     if ____:
>         result.append(0)
>     else:
>         ____
> print(result)
> ~~~
> {: .python}
>
> ~~~
> # Predicted output
> [0, 1, 1, 1, 0, 1]
> ~~~
> {: .output}
>
> > ## Solution
> > 
> > ~~~
> > original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
> > result = []
> > for value in original:
> >     if value < 0:
> >         result.append(0)
> >     else:
> >         result.append(1)
> > print(result)
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}

> ## Initializing
>
> Fill in the blanks.
>
> This function should find the largest and smallest values in a list.
>
> ~~~
> def min_max(values):
>     smallest, largest = None, None
>     for v in values:
>         if ____:
>             smallest, largest = v, v
>         ____:
>             smallest = min(____, v)
>             largest = max(____, v)
>     return ____
> 
> print(min_max([...some test data...]))
> ~~~
> {: .python}
>
> > ## Hint
> > 
> > What does '`None`' resolve to if evaluated in a conditional?
> >
> > The '`if`' statement should only execute on the first iteration of the for-loop
> >
> > Don't forget to add some actual numbers to the list passed to min_max()!
> {: .solution}
> 
> > ## Solution
> > 
> > ~~~
> > def min_max(values):
> >     smallest, largest = None, None  # Initialize some variables but don't set any actual values (you don't know what the `values` list will contain a priori)
> >     for v in values:
> >         if not smallest:  # `None` evaluates to `False`, so the 'double negative' evalutes to `True` on the first pass through the for-loop
> >             smallest, largest = v, v  # Now it's time to set actual values to `smallest` and `largest`
> >         else:
> >             # After the first pass through the loop, every `v` will be checked against the current min and max
> >             smallest = min(smallest, v)
> >             largest = max(largest, v)
> >     return smallest, largest
> > 
> > print(min_max([...some test data...]))
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}


> ## Bring it all together by processing a FASTA file
>
> The FASTA format specification consists of a header, prefixed with a 
> greater-than symbol (&gt;), that contains the sequence IDs and 
> space-separated metadata, followed by the sequence data on one or more
> subsequent lines.
>
> Use nano to open up the FASTA file in the 'sequences' directory.
>
> ~~~
> $: nano swc-data/sequences/pannexins.fa
> ~~~
> {: .bash}
>
> ~~~
>  GNU nano 2.2.6          File: swc-data/sequence/pannexins.fa
> 
> >Dme-Panx1 FBgn0004646 dmInx1.
> MYKLLGSLKSYLKWQDIQTDNAVFRLHNSFTTVLLLTCSLIITATQYVGQPISCIVNGVP
> PHVVNTFCWIHSTFTMPDAFRRQVGREVAHPGVANDFGDEDAKKYYTYYQWVCFVLFFQA
> MACYTPKFLWNKFEGGLMRMIVMGLNITICTREEKEAKRDALLDYLIKHVKRHKLYAIRY
> WACEFLCCINIIVQMYLMNRFFDGEFLSYGTNIMKLSDVPQEQRVDPMVYVFPRVTKCTF
> HKYGPSGSLQKHDSLCILPLNIVNEKTYVFIWFWFWILLVLLIGLIVFRGCIIFMPKFRP
> RLLNASNRMIPMEICRSLSRKLDIGDWWLIYMLGRNLDPVIYKDVMSEFAKQVEPSKHDR
> AK
> >Dme-Panx2 FBgn0027108 dmInx2.
> MFDVFGSVKGLLKIDQVCIDNNVFRMHYKATVIILIAFSLLVTSRQYIGDPIDCIVDEIP
> LGVMDTYCWIYSTFTVPERLTGITGRDVVQPGVGSHVEGEDEVKYHKYYQWVCFVLFFQA
> ILFYVPRYLWKSWEGGRLKMLVMDLNSPIVNDECKNDRKKILVDYFIGNLNRHNFYAFRF
> FVCEALNFVNVIGQIYFVDFFLDGEFSTYGSDVLKFTELEPDERIDPMARVFPKVTKCTF
> HKYGPSGSVQTHDGLCVLPLNIVNEKIYVFLWFWFIILSIMSGISLIYRIAVVAGPKLRH
> 
> ^G Get Help    ^O WriteOut    ^R Read File   ^Y Prev Page   ^K Cut Text    ^C Cur Pos
> ^X Exit        ^J Justify     ^W Where Is    ^V Next Page   ^U UnCut Text  ^T To Spell
> ~~~
> {: .txt}
>
> <br />
> For the following exercise write a program that will print only the
> IDs from the Drosophila melanogaster (Dme) sequences, like this:
>
> ~~~
> Dme-Panx1
> Dme-Panx2
> Dme-Panx3
> Dme-Panx4
> Dme-Panx5
> Dme-Panx6
> Dme-Panx7
> Dme-Panx8
> ~~~
> {: .txt}
>
> <br />
> To read the file into your program, use the following code snippet:
>
> ~~~
> with open("pannexins.fa", "r") as ifile:
>    lines = ifile.readlines()
> ~~~
> {: .python}
>
> <br />
> The 'readlines()' function will create a new list and then append 
> each line in the file to that list.
>
> NOTE: This is *NOT* the recommended solution for very large
> files, because readlines() stores everything in the file in memory.
> 
> > ## Solution
> > 
> > ~~~
> > # Read the file into a list
> > with open("pannexins.fa", "r") as ifile:
> >     lines = ifile.readlines()
> > 
> > # Loop over every line, searching for the header lines
> > for line in lines:
> >     # Confirm that the line is a header, not sequence
> >     if line[0] == ">":
> >         # 'split' the string into a list on the space (" ") character
> >         line_split = line.split(" ")
> > 
> >         # The sequence ID is the first index of the header list
> >         seq_id = line_split[0]
> > 
> >         # Remove the leading > symbol from the ID
> >         seq_id = seq_id[1:]
> > 
> >         # Test if the first three characters of the ID are "Dme"
> >         if seq_id[:3] == "Dme":
> >             print(seq_id)
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}
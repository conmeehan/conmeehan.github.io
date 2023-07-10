---
layout: article
titles:
  en      : &EN       Concepts in computer programming
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Concepts
---


This tutorial outlines the basics concepts in computer science such as variables, operators, selecting/iteration, pseudo code and regular expressions.<br />

## Learning outcomes
* Recognise data types and variables
* Describe arithmetic, relational and logic operators
* Execute selection and iteration workflows
* Express algorithms in pseudocode
* Implement regular expressions

## Prerequisites
It is recommended that you have [Notepad++ (Windows)](https://notepad-plus-plus.org/downloads/) or [BBEdit (Mac)](https://www.barebones.com/support/bbedit/updates.html) for the regular expressions tasks; most default Linux editors can do these.

## Order of tutorial

Please do the pre-learning quiz, then watch the presentation. <br />
During the presentation there are points to stop and do exercises, which are linked below. The answers to the questions in the exercises are linked within each one.<br />
Once finished the tutorial, take the post-learing quiz.<br />

### <a href="https://ntusurvey.onlinesurveys.ac.uk/concepts-in-computer-programming-pre-tutorial-survey" target="_blank">Concepts in Computer Programming Pre-tutorial Survey</a>

### [Presentation slides](https://conmeehan.github.io/PathogenDataCourse/SlideSets/ConceptsInComputerProgramming.pptx)

### <a href="https://ntusurvey.onlinesurveys.ac.uk/concepts-in-computer-programming-post-tutorial-survey" target="_blank">Concepts in Computer Programming Post-tutorial Survey</a>

## Tasks from slides with sample answers
### Sequence and iteration
{:start="1"}
1. Initialise a variable with a certain real value. Write a statement that will add 10 to the variable if it is less than 10 and divide the variable by 10 if it is greater than or equal to 10

<details> <summary>Click here for answer</summary>

{% highlight console %}
real var1 = 11.0
if var1 < 10
  var1 = var1+10
else
  var1 = var1/10 
{% endhighlight %}

</details><br />

{:start="2"}
2. Write a for loop that will iterate from 1 to 10 and at each stage get the modulus 2 of the variable

<details>

<summary>Click here for answer</summary>

{% highlight console %}
for variable between 1 and 10
print variable%2 
{% endhighlight %}

</details><br />

{:start="3"}
3. Initialise a variable to be value 1. Write a while loop that continues until that variable is 100. Inside the loop, if the number is less than 10, get the number to the power of itself. If it is between 10 and 50, take away 5 from the number. If it is above 50, add 1 to the number

<details>

<summary>Click here for answer</summary>

{% highlight console %}
int var1 = 1
while var1 <=100
  if var1 < 10
    var1= var1^var1
  else if var1 >= 10 && var1 <=50
    var1 = var1 - 5
  else if var1 > 50
    var1 = var1 + 1 
{% endhighlight %}

* Note: the algorithm is worded ambiguously where it states 'between 10 and 50' and should be more specific saying "between 10 and 50 included" or similar. 
 * This is specifically like this to make you think about ambiguity
* Note 2: This loop will actually never finish because the first step of the loop is 1^1 which is 1, so it will never increase and thus run forever.
  * This is specifically done to make you think about covering all scenarios. Probably best to start at 2 or add a clause to capture such cases

</details>

### Pseudocode
{:start="1"}
1. Ask the user for 2 numbers and print out their product (i.e. multiply them together)
<details><summary>Click here for answer</summary>

{% highlight console %}
Prompt user to enter a number
  Store number in variable1
 Prompt user for a second number
  Store number in variable2
 Multiply variable1 and variable2
  Store answer in variable3
 Print variable3 to screen 
{% endhighlight %}

</details><br />

{:start="2"}
2. Read in a string of letters and check if it is a valid DNA string
<details><summary>Click here for answer</summary>

{% highlight console %}
Read in a string from the user or file
  Store in variable1
Loop through by going letter by letter through the string
  Check if the letter is an A, C, G or T (case insensitive)
  If not, stop
 If the loop  finishes without stopping early, it is a valid DNA string 
{% endhighlight %}

</details><br />

{:start="3"}
3. Check if a string conforms to the pattern “patient_000000” where the 6 digits can be any numbers between 0-9
  - Hint: use phrases like ‘starts with’, ‘ends with’, ‘followed by’
<details><summary>Click here for answer</summary>

{% highlight console %}
Store string in a variable
Check if variable starts with "patient_" and is followed by six digits
Check that the string ends after these 6 digits
{% endhighlight %}

</details><br />

{:start="4"}
4. Do the following steps
  - Read in 5 separate numbers
  - Calculate the average of the five numbers
  - Find the smallest (minimum) and largest (maximum) of the five entered numbers.
  - Write out the three results found with a message describing what they are
<details><summary>Click here for answer</summary>

{% highlight console %}
Create 5 real type variables and store numbers in each
Add all five numbers to each other and divide that answer by 5 to get the average
  print to screen "This is the average of the five numbers" followed by the answer
Starting with the first number, store it in a variable called minimum
Now go number by number through the other 4 and at each number check if it is smaller than the number stored in minimum
  If so, replace the number stored in minimum by that number
Once finished, print to screen "The minimum of the 5 numbers is" followed by the number stored in the minimum variable
Starting with the first number, store it in a variable called mamimum
Now go number by number through the other 4 and at each number check if it is larger than the number stored in maximum
  If so, replace the number stored in maximum by that number
Once finished, print to screen "The maximum of the 5 numbers is" followed by the number stored in the maximum variable
{% endhighlight %}

</details><br />

### Regular expressions
These should be done in Notepad++ or BBEdit
Create a file with the following content:
```
>seq1
ACTGC
>seq2
AACTG
>seq3
TTTCC
>seq4
AACCC
```
{:start="1"}
1. Find all sequence names (i.e. seq followed by a number)
  - Sequence names are lines that begin with >

<details><summary>Click here for answer</summary>

{% highlight console %}
Find:
^>.*
{% endhighlight %}

</details><br />

{:start="2"}
2. Find the first nucleotide of each sequence
<details><summary>Click here for answer</summary>

{% highlight console %}
Find:
^[^>]
{% endhighlight %}

</details><br />

{:start="3"}
3. Replace all ‘seq’ in sequence names with ‘sample’
  - Sequence names are lines that begin with >
<details><summary>Click here for answer</summary>

{% highlight console %}
Find:
^>seq
Replace:
>sample
{% endhighlight %}

</details><br />

{:start="4"}
4. Add a tab character followed by ‘function’ to the end of each sequence name
<details><summary>Click here for answer</summary>

{% highlight console %}
Find:
^(>.*)
Replace:
\1\tfunction
{% endhighlight %}

</details><br />

{:start="5"}
5. Find an AA at the start of a line and move it to the end of the line
<details><summary>Click here for answer</summary>

{% highlight console %}
Find:
^(AA)(.*)$
Replace:
\2\1
{% endhighlight %}

</details><br />


## Additional (advanced) tasks
* Write pseudocode that will check if a year is a leap year
* Write pseudocode to search a fasta file for every occurrence of a specific DNA motif
* In a file of bacterial species names, change the full name (e.g. Mycobacterium tuberculosis) to the shortened name (e.g. M. tuberculosis), no matter what the species name is

## Useful websites with additonal resources
* [The first step to learning bioinformatics is to not jump to bioinformatics](https://towardsdatascience.com/the-first-step-to-learning-bioinformatics-is-to-not-jump-to-bioinformatics-2e958f7b811a)
* [Programming concepts (Isaac computer science)](https://isaaccomputerscience.org/topics/programming_concepts?examBoard=all&stage=all)
* [What is pseudocode (Future learn)](https://www.futurelearn.com/info/courses/block-to-text-based-programming/0/steps/39492)
* [Regular Expressions for Biologists](https://carpentries-incubator.github.io/regex-novice-biology/)
* [Abstraction in computer science](https://www.happykhan.com/posts/abstraction-in-computer-science/)

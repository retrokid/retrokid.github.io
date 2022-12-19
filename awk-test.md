# 1 AN AWK TUTORIAL

Awk is a convenient and expressive programming language that can be applied to a wide variety of computing and data-manipulation tasks. This chapter is a tutorial, designed to let you start writing your own programs as quickly as possible. Chapter 2 describes the whole language, and the remaining chapters show how awk can be used to solve problems from many different areas. Throughout the book, we have tried to pick examples that you should find useful, interesting, and instructive.

## 1.1 Getting Started

Useful awk programs are often short, just a line or two. Suppose you have a file called __emp.data__ that contains the name, pay rate in dollars per hour, and number of hours worked for your employees, one employee record per line, like this:

```
Beth	4.00	0
Dan 	3.75	0
Kathy	4.00	10
Mark 	5.00	20
Mary 	5.50	22
Susie 	4.25	18
``` 

Now you want to print the name and pay (rate times hours) for everyone who worked more than zero hours. This is the kind of job that awk is meant for, so it's easy. Just type this command line:

```
awk '$3 > 0 { print $1, $2 * $3 }' emp.data
```

You should get this output:

```
Kathy 40
Mark 100
Mary 121
Susie 76.5
```

This command line tells the system to run awk, using the program inside the quote characters, taking its data from the input file __emp.data__. The part inside the quotes is the complete awk program. It consists of a single pattern-action statement. The pattern, `$3 > 0`, matches every input line in which the third column, or field, is greater than zero, and the action

```
{ print $1, $2 * $3 }
```

prints the first field and the product of the second and third fields of each matched line.

> __!IMPORTANT!__
> Awk programs runs seperately for every single line. 
> If there are 4 lines in a file the program will run 4 times. 
> Every line treated as another input. 
> And every input is causing the program run again.

If you want to print the names of those employees who did not work, type this command line:

```
awk '$3 == 0 { print $1 }' emp.data
```

Here the pattern, `$3 == 0`, matches each line in which the third field is equal
to zero, and the action `{ print $1 }` prints its first field.

As you read this book, try running and modifying the programs that are
presented. Since most of the programs are short, you'll quickly get an understanding of how awk works. On a Unix system, the two transactions above would look like this on the terminal:

```
$ awk '$3 > 0 { print $1, $2 * $3 }' emp.data 
Kathy 40
Mark 100
Mary 121
Susie 76.5
$ awk '$3 == 0 { print $1 }' emp.data 
Beth
Dan
$
```

The `$` at the beginning of a line is the prompt from the system; it may be different on your machine.


#### The Structure of an AWK Program

Let's step back a moment and look at what is going on. In the command lines above, the parts between the quote characters are programs written in the awk programming language. Each awk program in this chapter is a sequence of one or more pattern-action statements:

```
pattern { action } 
pattern { action }
...
```

The basic operation of awk is to scan a sequence of input lines one after another, searching for lines that are matched by any of the patterns in the program. The precise meaning of the word "match" depends on the pattern in question; for patterns like `$3 > 0`, it means "the condition is true."
Every input line is tested against each of the patterns in turn. For each pattern that matches, the corresponding action (which may involve multiple steps) is performed. Then the next line is read and the matching starts over. This continues until all the input (file) has been read.
The programs above are typical examples of patterns and actions.

```
$3 == 0 { print $1 }
```

is a single pattern-action statement; for every line in which the third field is zero, the first field is printed.

Either the pattern or the action (but not both) in a pattern-action statement may be omitted. If a pattern has no action, for example,

```
$3 == 0
```
then each line that the pattern matches (that is, each line for which the condition is true) is printed. This program prints the two lines from the __emp.data__ file where the third field is zero:

```
Beth 4.00 0 
Dan 3.75 0
```

If there is an action with no pattern, for example,

```
{ print $1 }
```

then the action, in this case printing the first field, is performed for every input line.
Since patterns and actions are both optional, actions are enclosed in braces to distinguish them from patterns.

#### Running an AWK Program

There are several ways to run an awk program. You can type a command line of the form

```
awk 'program' input files
```
to run the program on each of the specified input files. 

For example, you could type

```
awk '$3 == 0 { print $1 }' file1 file2
```

to print the first field of every line of __file 1__ and __file2__ in which the third field is zero.


You can omit the input files from the command line and just type

```
awk 'program '
```

In this case awk will apply the program to whatever you type next on your terminal until you type an end-of-file signal (control-d on Unix systems). Here is a sample of a session on Unix:

```
$ awk '$3 == 0 { print $1 }'
Beth 4.00 0
Beth
Dan 3.75 0
Dan
Kathy 3.75 10 
Kathy 3.75 0 
Kathy
```

The lines 3, 5, 8 are what the computer printed.

This behavior makes it easy to experiment with awk: type your program,
then type data at it and see what happens. We again encourage you to try the examples and variations on them.

Notice that the program is enclosed in single quotes on the command line. This protects characters like `$` in the program from being interpreted by the shell and also allows the program to be longer than one line.

This arrangement is convenient when the program is short (a few lines). If the program is long, however, it is more convenient to put it into a separate file, say __progfile__, and type the command line

```
awk -f progfile optional list of input files
```

#### Errors

If you make an error in an awk program, awk will give you a diagnostic message. For example, if you mistype a brace, like this:

```
awk '$3 == 0 [ print $1 }' emp.data
```

you will get a message like this:

```
awk: syntax error at source line 1 
context is
	$3 == 0 >>> [ <<< 
	extra }
	missing ]
awk: bailing out at source line 1
```

"Syntax error" means that you have made a grammatical error that was detected at the place marked by `>>> <<<`. "Bailing out" means that no recovery was attempted. Sometimes you get a little more help about what the error was, such as a report of mismatched braces or parentheses.
Because of the syntax error, awk did not try to execute this program. Some errors, however, may not be detected until your program is running. For example, if you attempt to divide a number by zero, awk will stop its processing and report the input line number and the line number in the program at which the division was attempted.

## 1.2 Simple Output

The rest of this chapter contains a collection of short, typical awk programs based on manipulation of the __emp.data__ file above. We'll explain briefly what's going on, but these examples are meant mainly to suggest useful operations that are easy to do with awk - printing fields, selecting input, and transforming data. We are not showing everything that awk can do by any means, nor are we going into many details about the specific things presented here. But by the end of this chapter, you will be able to accomplish quite a bit, and you'll find it much easier to read the later chapters.
We will usually show just the program, not the whole command line. In every case, the program can be run either by enclosing it in quotes as the first argument of the awk command, as shown above, or by putting it in a file and invoking awk on that file with the `-f` option.
There are only two types of data in awk: numbers and strings of characters. The `emp.data` file is typical of this kind of information - a mixture of words and numbers separated by blanks and/or tabs.
Awk reads its input one line at a time and splits each line into fields, where, by default, a field is a sequence of characters that doesn't contain any blanks or tabs. The first field in the current input line is called $1, the second $2, and so forth. The entire line is called $0. The number of fields can vary from line to line.
Often, all we need to do is print some or all of the fields of each line, perhaps performing some calculations. The programs in this section are all of that form.

##### Printing Every Line

More than one item can be printed on the same output line with a single __print__ statement. The program to print the first and third fields of each input line is

```
{ print $1, $3 }
```

With __emp.data__ as input, it produces

```
Beth 0 
Dan 0 
Kathy 10 
Mark 20 
Mary 22 
Susie 18
```

Expressions separated by a comma in a print statement are, by default, separated by a single blank when they are printed. Each line produced by __print__ ends with a __newline__ character. Both of these defaults can be changed; we'll show how in "Chapter 2".

##### NF, the Number of Fields

It might appear you must always refer to fields as $1, $2, and so on, but any expression can be used after $ to denote a field number; the expression is evaluated and its numeric value is used as the field number. Awk counts the number of fields in the current input line and stores the count in a built-in vari- able called NF. Thus, the program

```
{ print NF, $1, $NF }
```

prints the number of fields and the first and last fields of each input line.

##### Computing and Printing


You can also do computations on the field values and include the results in what is printed. The program

```
{ print $1, $2 * $3 }
```

is a typical example. It prints the name and total pay (rate times hours) for
each employee:

```
Beth 0
Dan 0 
Kathy 40 
Mark 100 
Mary 121 
Susie 76.5
```

We'll show in a moment how to make this output look better.

##### Printing Line Numbers

Awk provides another built-variable, called __NR__, that counts the number of lines read so far. We can use __NR__ and __$0__ to prefix each line of __emp.data__ with its line number:

```
{ print NR, $0 }
```

The output looks like this:

```
1 Beth 4.00 0 
2 Dan 3.75 0 
3 Kathy 4.00 10 
4 Mark 5.00 20 
5 Mary 5.50 22 
6 Susie 4.25 18
```

##### Putting Text in the Output

You can also print words in the midst of fields and computed values:

```awk
{ print "total pay for", $1, "is", $2 * $3 }
```

prints

```
total pay for Beth is 0 
total pay for Dan is 0 
total pay for Kathy is 40 
total pay for Mark is 100 
total pay for Mary is 121 
total pay for Susie is 76.5
```

In the print statement, the text inside the double quotes is printed along with the fields and computed values.

## 1.3 Fancier Output

The print statement is meant for quick and easy output. To format the output exactly the way you want it, you may have to use the __printf__ statement. As we shall see in Section 2.4, __printf__ can produce almost any kind of output, but in this section we'll only show a few of its capabilities.

#### Lining Up Fields

The __printf__ statement has the form

```
printf(format, value_1, value_2, ... , value_N)
```

where __format__ is a string that contains text to be printed verbatim, interspersed with specifications of how each of the values is to be printed. A specification is a "%" followed by a few characters that control the format of a value. The first specification tells how value_1 is to be printed, the second how value_2 is to be printed, and so on. Thus, there must be as many "%" specifications in format as values to be printed.

Here's a program that uses __printf__ to print the total pay for every employee:

```
{ printf("total pay for %s is $%.2f\n", $1, $2 * $3) }
```

The specification string in the __printf__ statement contains two "%" specifications.
The first, __%s__, says to print the first value, __$1__, as a string of characters; the second, __%.2f__, says to print the second value, __"$2 * $3"__, as a number with 2 digits after the decimal point. Everything else in the specification string, including the dollar sign, is printed verbatim; the "\n" at the end of the string stands for a "newline", which causes subsequent output to begin on the next line. With __emp.data__ as input, this program yields:

```
total pay for Beth is $0.00 
total pay for Dan is $0.00 
total pay for Kathy is $40.00 
total pay for Mark is $100.00 
total pay for Mary is $121.00 
total pay for Susie is $76.50
```

With __printf__, no blanks or newlines are produced automatically; you must create them yourself. Don't forget the "\n".

Here's another program that prints each employee's name and pay:

```
{ printf("%-8s $%6.2f\n", $1, $2 * $3) }
```


The first specification, "%-8s", prints a name as a string of characters left-justified in a field 8 characters wide. The second specification, "%6.2f", prints the pay as a number with two digits after the decimal point, in a field 6 characters wide:

We'll show lots more examples of __printf__ as we go along; the full story is in Section 2.4.

#### Sorting the Output

Suppose you want to print all the data for each employee, along with his or her pay, sorted in order of increasing pay. The easiest way is to use awk to prefix the total pay to each employee record, and run that output through a sorting program. On Unix, the command line

```
awk '{ printf("%6.2f %s\n", $2 * $3, $0) }' emp.data | sort
```

pipes the output of awk into the `sort` command, and produces:

```
  0.00	Beth	4.00 0
  0.00	Dan		3.75 0
 40.00	Kathy	4.00 10 
 76.50	Susie	4.25 18
100.00	Mark	5.00 20 
121.00	Mary	5.50 22
```

## 1.4 Selection

Awk patterns are good for selecting interesting lines from the input for further processing. Since a pattern without an action prints all lines matching the pattern, many awk programs consist of nothing more than a single pattern. This section gives some examples of useful patterns. 

#### Selection by Comparison

This program uses a comparison pattern to select the records of employees who earn $5.00 or more per hour, that is, lines in which the second field is greater than or equal to 5:

```
$2 >= 5
```

It selects these lines from __emp.data__:

```
Mark 5.00 20 
Mary 5.50 22
```

#### Selection by Computation

The program

```
$2 * $3 > 50 { printf("$%.2f for %s\n", $2 * $3, $1) }
```

prints the pay of those employees whose total pay exceeds $50:

```
$100.00 for Mark 
$121.00 for Mary 
$76.50 for Susie
```

#### Selection by Text Content

Besides numeric tests, you can select input lines that contain specific words
or phrases. This program prints all lines in which the first field is Susie:

```
$1 == "Susie"
```

The operator "=="" tests for equality. You can also look for text containing any of a set of letters, words, and phrases by using patterns called "regular expressions". This program prints all lines that contain __Susie__ anywhere:

```
/Susie/
```

The output is this line:

```
Susie 4.25 18
```

Regular expressions can be used to specify much more elaborate patterns; Section 2.1 contains a full discussion.

#### Combinations of Patterns

Patterns can be combined with parentheses and the logical operators `&&`, `||` ,
and `!`, which stand for AND, OR, and NOT. The program

```
$2 >= 4 || $3 >= 20
```

prints those lines where $2 is at least 4 or $3 is at least 20:

```
Beth 	4.00 	0 
Kathy 	4.00 	10 
Mark 	5.00 	20 
Mary 	5.50 	22 
Susie 	4.25 	18
```

Lines that satisfy both conditions are printed only once. Contrast this with the following program, which consists of two patterns:

```
$2 >= 4 
$3 >= 20
```

This program prints an input line twice if it satisfies both conditions:

```
Beth	 4.00 	0 
Kathy	 4.00 	10 
Mark	 5.00 	20 
Mark 	 5.00 	20 
Mary 	 5.50 	22 
Mary 	 5.50 	22 
Susie 	 4.25 	18
```

Note that the program

```
!($2 < 4 && $3 < 20)
```

prints lines where it is not true that $2 is less than 4 and $3 is less than 20; this condition is equivalent to the first one above, though perhaps less readable.

#### Data Validation
page 22




























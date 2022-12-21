# 2 THE AWK LANGUAGE

This chapter explains, mostly with examples, the constructs that make up awk programs. Because it's a description of the complete language, the material is detailed, so we recommend that you skim it, then come back as necessary to check up on details.

The simplest awk program is a sequence of pattern-action statements: 

```
pattern { action }
pattern { action }
...
```

In some statements, the pattern may be missing; in others, the action and its enclosing braces may be missing. After awk has checked your program to make sure there are no syntactic errors, it reads the input a line at a time, and for each line, evaluates the patterns in order. For each pattern that matches the current input line, it executes the associated action. A missing pattern matches every input line, so every action with no pattern is performed at each line. A pattern-action statement consisting only of a pattern prints each input line matched by the pattern. Throughout most of this chapter, the terms "input line" and "record" are used synonymously. In Section 2.5, we will discuss multiline records, where a record may contain several lines.
The first section of this chapter describes patterns in detail. The second section begins the description of actions by describing expressions, assignments, and control-flow statements. The remaining sections cover function definitions, output, input, and how awk programs can call other programs. Most sections contain summaries of major features.

### The Input File "countries"

As input for many of the awk programs in this chapter, we will use a file called __countries__. Each line contains the name of a country, its area in thousands of square miles, its population in millions, and the continent it is in. The data is from 1984; the __USSR__ has been arbitrarily placed in Asia. In the file, the four columns are separated by tabs; a single blank separates __North__ and __South__ from __America__.

The file countries contains the following lines:

```
USSR	8649	275		Asia
Canada	3852	25		North America
China	3705	1032	Asia
USA		3615	237		North America
Brazil	3286	134		South America
India	1267	746		Asia
Mexico	762		78		North America
France	211		55		Europe
Japan	144		120		Asia
Germany	96		61		Europe
England	94		56		Europe
```

For the rest of this chapter, the countries file is used when no input file is mentioned explicitly.

### Program Format

Pattern-action statements and the statements within an action are usually separated by newlines, but several statements may appear on one line if they are separated by semicolons. A semicolon may be put at the end of any statement.
The opening brace of an action must be on the same line as the pattern it accompanies; the remainder of the action, including the closing brace, may appear on the following lines.
Blank lines are ignored; they may be inserted before or after any statement to improve the readability of a program. Blanks and tabs may be inserted around operators and operands, again to enhance readability.
Comments may be inserted at the end of any line. A comment starts with the character # and finishes at the end of the line, as in

```awk
{ print $1, $3 } # print country name and population
```

A long statement may be spread over several lines by inserting a backslash
and newline at each break:

```awk
{ print \ 
		$1,  # country name
		$2,  # area in thousands of square miles
		$3 } # population in millions
```

As this example shows, statements may also be broken after commas, and a comment may be inserted at the end of each broken line.
In this book we have used several formatting styles, partly to illustrate different ones, and partly to keep programs from occupying too many lines. For short programs like those in this chapter, format doesn't much matter, but consistency and readability will help to keep longer programs manageable.

## 2.1 Patterns

Patterns control the execution of actions: when a pattern matches, its associated action is executed. This section describes the six types of patterns and the conditions under which they match.


----------------------------------------------------------------

### Summary of Patterns

1. `BEGIN { statements }`
	- The __statements__ are executed once before any input has been read.
2. `END { statements }`
	- The __statements__ are executed once after all input has been read.
3. `expression { statements }`
	- The __statements__ are executed at each input line where the __expression__ is true, that is, nonzero or nonnull.
4. `/regular expression/ { statements }`
	- The __statements__ are executed at each input line that contains a string matched by the __regular expression__.
5. `compound pattern { statements }`
	- A compound pattern combines expressions with `&& (AND), || (OR), ! (NOT)`, and parentheses; the __statements__ are executed at each input line where the __compound pattern__ is true.
6. `pattern_1 , pattern_2 { statements }`
	- A range pattern matches each input line from a line matched by pattern_1 to the next line matched by pattern_2, inclusive; the statements are executed at each matching line.

`BEGIN` and `END` do not combine with other patterns. A range pattern cannot be part of any other pattern. `BEGIN` and `END` are the only patterns that require an action.

-----------------------------------------------------------------


### BEGIN and END

The `BEGIN` and `END` patterns do not match any input lines. Rather, the statements in the `BEGIN` action are executed before awk reads any input; the statements in the `END` action are executed after all input has been read. `BEGIN` and `END` thus provide a way to gain control for initialization and wrapup. `BEGIN` and `END` do not combine with other patterns. If there is more than one `BEGIN`, the associated actions are executed in the order in which they appear in the program, and similarly for multiple `END`'s. Although it's not mandatory, we put `BEGIN` first and `END` last.
One common use of a `BEGIN` action is to change the default way that input lines are split into fields. The field separator is controlled by a built-in variable called `FS`. By default, fields are separated by blanks and/or tabs; this behavior occurs when `FS` is set to a blank. Setting `FS` to any character other than a blank makes that character the field separator.

The following program uses the `BEGIN` action to set the field separator to a tab character (\t) and to put column headings on the output. The second `printf` statement, which is executed at each input line, formats the output into a table, neatly aligned under the column headings. The `END` action prints the
totals. (Variables and expressions are discussed in Section 2.2)

```awk
# print countries with column headers and totals

BEGIN { FS = "\t" # make tab the field separator 
		printf("%10s %6s %5s	%s\n\n",
		"COUNTRY", "AREA", "POP", "CONTINENT")
	  }
	  { printf("%10s %6d %5d	%s\n", $1, $2, $3, $4)
	    area = area + $2
	  	pop = pop + $3
	  }
END   { printf( "\n%10s %6d %5d\n", "TOTAL", area, pop) }
```

With the countries file as input, this program produces

```
COUNTRY   AREA   POP	CONTINENT

      USSR   8649   275	Asia
    Canada   3852    25	North America
     China   3705  1032	Asia
       USA   3615   237	North America
    Brazil   3286   134	South America
     India   1267   746	Asia
    Mexico    762    78	North America
    France    211    55	Europe
     Japan    144   120	Asia
   Germany     96    61	Europe
   England     94    56	Europe

     TOTAL  25681  2819
```

### Expressions as Patterns

Like most programming languages, awk is rich in expressions for describing numeric computations. Unlike many languages, awk also has expressions for describing operations on strings. Throughout this book, the term __string__ means a sequence of zero or more characters. These may be stored in variables, or appear literally as string constants like `""` or `"Asia"`. The string `""`, which contains no characters, is called the __null string__. The term substring means a contiguous sequence of zero or more characters within a string. In every string, the __null string__ appears as a substring of length zero before the first character, between every pair of adjacent characters, and after the last character.
Any expression can be used as an operand of any operator. If an expression has a numeric value but an operator requires a string value, the numeric value is automatically transformed into a string; similarly, a string is converted into a number when an operator demands a numeric value.
Any expression can be used as a pattern. If an expression used as a pattern has a nonzero or nonnull value at the current input line, then the pattern matches that line. The typical expression patterns are those involving comparisons between numbers or strings. A comparison expression contains one of the six relational operators, or one of the two string-matching operators `~` (tilde) and `!~` that will be discussed in the next section. These operators are listed in table below.

| Operator | Meaning                  | 
| -------- | ------------------------ |
| <        | less than                |
| <=       | less than or equal to    |
| ==       | equal to                 |
| !=       | not equal to             |
| >=       | greater than or equal to |
| >        | greater than             |
| ~        | matched by               |
| !~       | not matched by           |






















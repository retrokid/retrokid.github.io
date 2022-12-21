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
































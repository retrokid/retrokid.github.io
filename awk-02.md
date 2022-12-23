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


If the pattern is a comparison expression like `NF > 10`, then it matches the current input line when the condition is satisfied, that is, when the number of fields in the line is greater than ten. If the pattern is an arithmetic expression like `NF`, it matches the current input line when its numeric value is nonzero. If the pattern is a string expression, it matches the current input line when the string value of the expression is nonnull.
In a relational comparison, if both operands are numeric, a numeric comparison is made; otherwise, any numeric operand is converted to a string, and then the operands are compared as strings. The strings are compared character by character using the ordering provided by the machine, most often the ASCII character set. One string is said to be "less than" another if it would appear before the other according to this ordering, e.g., "Canada" < "China" and "Asia"< "Asian".

The pattern

```awk
$3 / $2 >= 0.5
```

selects lines where the value of the third field divided by the second is numerically greater than or equal to 0.5, while

```awk
$0 >= "M"
```

selects lines that begin with an M, N, o, etc.:

```
USSR	8649	275		Asia
USA		3615	237		North America
Mexico	762		78		North America
```

Sometimes the type of a comparison operator cannot be determined solely by the syntax of the expression in which it appears. The program

```awk
$1 < $4
```

could compare the first and fourth fields of each input line either as numbers or as strings. Here, the type of the comparison depends on the values of the fields, and it may vary from line to line. In the ___countries___ file, the first and fourth fields are always strings, so string comparisons are always made; the output is

```
Canada	3852	25		North America
Brazil	3286	134		South America
Mexico	762		78		North America
England	94		56		Europe
```

Only if both fields are numbers is the comparison done numerically; this would be the case with

```awk
$2 < $3
```

on the same data.
Section 2.2 contains a more complete discussion of strings, numbers, and expressions.

### String-Matching Patterns

Awk provides a notation called __regular expressions__ for specifying and matching strings of characters. Regular expressions are widely used in Unix programs, including its text editors and shell. Restricted forms of regular expressions also occur in systems like MS-DOS as "wild-card characters" for specifying sets of filenames.
A string-matching pattern tests whether a string contains a substring matched by a regular expression.
The simplest regular expression is a string of letters and numbers, like Asia, that matches itself. To turn a regular expression into a string-matching pattern, just enclose it in slashes:

```awk
/Asia/
```

This pattern matches when the current input line contains the substring __Asia__, either as __Asia__ by itself or as some part of a larger word like __Asian__ or __Pan-Asiatic__. Note that blanks are significant within regular expressions: the string-matching pattern

-------------------------------------------------------

### String-Matching Patterns

1. /regexpr/
	- Matches when the current input line contains a substring matched by __regexpr__.
2. expression ~ /regexpr/
	- Matches if the string value of __expression__ contains a substring matched by __regexpr__.
3. expression !~ /regexpr/
	- Matches if the string value of expression does not contain a substring matched by __regexpr__.

Any expression may be used in place of /regexpr/ in the context of `~` and `!~`.

-------------------------------------------------------

```awk
/ Asia /
```

matches only when Asia is surrounded by blanks.

The pattern above is one of three types of string-matching patterns. Its form is a regular expression /r/ enclosed in slashes:

```awk
/r/
```

This pattern matches an input line if the line contains a substring matched by __r__.

The other two types of string-matching patterns use an explicit matching
operator:

```
expression ~ /r/
expression !~ /r/
```

The matching operator `~` means "is matched by" and `!~` means "is not matched by." The first pattern matches when the string value of expression contains a substring matched by the regular expression __r__; the second pattern matches if there is no such substring.

The left operand of a matching operator is often a field: the pattern

```awk
$4 ~ /Asia/
```

matches all input lines in which the fourth field contains __Asia__ as a substring, while

```awk
$4 !~ /Asia/
```

matches if the fourth field does not contain __Asia__ anywhere.

Note that the string-matching pattern

```awk
/Asia/
```

is a shorthand for

```awk
$O ~ /Asia/
```

### Regular Expressions

A regular expression is a notation for specifying and matching strings. Like an arithmetic expression, a regular expression is a basic expression or one created by applying operators to component expressions. To understand the strings matched by a regular expression, we need to understand the strings matched by its components.

---------------------------------------------------------
### Regular Expressions

1. The regular expression metacharacters are:
	- `\ ^ $ . [ ] | ( ) * + ?`
2. A basic regular expression is one of the following:
	- a nonmetacharacter, such as __A__. that matches itself.
	- an escape sequence that matches a special symbol: `\t` matches a tab
	- a quoted metacharacter, such as `\*`,that matches the metacharacter literally.
	- `^`, which matches the beginning of a string.
	- `$`, which matches the end of a string.
	- `.`, which matches any single character.
	- a character class: `[ABC]` matches any of the characters A, B, or C.
	- character classes may include abbreviations: `[A-Za-z]` matches any single letter.
	- a complemented character class: `[^0-9]` matches any character except a digit.
3. These operators combine regular expressions into larger ones:
	- alternation: `A|B` matches A or B.
	- concatenation: `AB` matches A immediately followed by B.
	- closure: `A*` matches zero or more A's.
	- positive closure: `A+` matches one or more A's.
	- zero or one: `A?` matches the null string or A.
	- parentheses: `(r)` matches the same strings as r does.

--------------------------------------------------------------


The basic regular expressions are summarized in the table above. The characters

`\ ^ $ . [ ] | ( ) * + ?`

are called metacharacters because they have special meanings. A regular expression consisting of a single nonmetacharacter matches itself. Thus, a single letter or digit is a basic regular expression that matches itself. To preserve the literal meaning of a metacharacter in a regular expression, precede it by a backslash. Thus, the regular expression `\$` matches the character __$__. If a character is preceded by a single `\`, we'll say that character is __quoted__.

In a regular expression, an unquoted caret `^` matches the beginning of a string, an unquoted dollar-sign `$` matches the end of a string, and an unquoted period `.` matches any single character. Thus,

- `^C` matches a C at the beginning of a string
- `C$` matches a C at the end of a string
- `^C$` matches the string consisting of the single character c
- `^.$` matches any string containing exactly one character
- `^...$` matches any string containing exactly three characters
- `...` matches any three consecutive characters
- `\.$` matches a period at the end of a string

A regular expression consisting of a group of characters enclosed in brackets is called a __character class__; it matches any one of the enclosed characters. For example, `[AEIOU]` matches any of the characters __A__, __E__, __I__, __O__ or __U__.

Ranges of characters can be abbreviated in a character class by using a hyphen `-`. The character immediately to the left of the hyphen defines the beginning of the range; the character immediately to the right defines the end. Thus, `[0-9]` matches any digit, and `[a-zA-Z][0-9]` matches a letter followed by a digit. Without both a left and right operand, a hyphen in a character class denotes itself, so the character classes `[+-]` and `[-+]` match either a `+` or a `-`. The character class `[A-Za-z-]+` matches words that include hyphens.
A __complemented__ character class is one in which the first character after the `[` is a `^`. Such a class matches any character __not__ in the group following the caret. Thus, `[^0-9]` matches any character except a digit; `[^a-zA-Z]` matches any character except an upper or lower-case letter.

- `^[ABC]` matches an A, B or C at the beginning of a string
- `^[^ABC]` matches any character at the beginning of a string. except A, B or C
- `[^ABC]` matches any character other than an A, B or C
- `^[^a-z]$` matches any single-character string. except a lower-case letter

Inside a character class, all characters have their literal meaning, except for the quoting character `\`, `^` at the beginning, and `-` between two characters. Thus, `[.]` matches a period and `^[^^]` matches any character except a caret at the beginning of a string.

Parentheses are used in regular expressions to specify how components are grouped. There are two binary regular expression operators: alternation and concatenation. The alternation operator `|` is used to specify alternatives: if `r_1` and `r_2` are regular expressions, then `r_1 | r_2` matches any string matched by `r_1` or by `r_2`.

There is no explicit concatenation operator. If `r_1` and `r_2` are regular expressions, then `(r_1)(r_2)` (with no blank between (r_1) and (r_2)) matches any string of the form `xy` where `r_1` matches `x` and `r_2` matches `y`. The parentheses around `r_1` or `r_2` can be omitted, if the contained regular expression does not contain the alternation operator. The regular expression

```awk
(Asian|European|North American) (male|female) (black|blue)bird
```

matches twelve strings ranging from

```
Asian male blackbird
```

to

```
North American female bluebird
```

The symbols `*`, `+` and `?` are unary operators used to specify repetitions in regular expressions. If `r` is a regular expression, then `(r)*` matches any string consisting of zero or more consecutive substrings matched by `r`, `(r)+` matches any string consisting of one or more consecutive substrings matched by `r`, and `(r)?` matches the null string or any string matched by `r`. If `r` is a basic regular expression, then the parentheses can be omitted.

- `B*` matches the null string or B or BB, and so on
- `AB*C` matches AC or ABC or ABBC, and so on
- `AB+C` matches ABC or ABBC or ABBBC, and so on
- `ABB*C` also matches ABC or ABBC or ABBBC, and so on
- `AB?C` matches AC or ABC
- `[A-Z]+` matches any string of one or more upper-case letters
- `(AB)+C` matches ABC, ABABC, ABABABC, and so on

In regular expressions, the alternation operator | has the lowest precedence, then concatenation, and finally the repetition operators `*`, `+`, and `?`. As in arithmetic expressions, operators of higher precedence are done before lower ones. These conventions often allow parentheses to be omitted: `ab|cd` is the same as `(ab)|(cd)`, and `^ab|cd*e$` is the same as `(^ab)|(c(d*)e$)`.


To finish our discussion of regular expressions, here are some examples of useful string-matching patterns containing regular expressions with unary and binary operators, along with a description of the kinds of input lines they match. Recall that a string-matching pattern `/r/` matches the current input line if the line contains at least one substring matched by `r`.

```awk
/^[0-9]+$/ 
	# matches any input line that consists of only digits
```

```awk
/^[0-9][0-9][0-9]$/ 
	# matches any input line that exactly three digits
```

```awk
/^(\+|-)?[0-9]+\.?[0-9]*$/ 
	# matches a decimal number with an optional sign and optional fraction
```

```awk
/^[+-]?[0-9]+[.]?[0-9]*$/
	# also a decimal number with an optional sign and optional fraction
```

```awk
/^[+-]?([0-9]+[.]?[0-9]*|[.][0-9]+)([eE][+-]?[0-9]+)?$/
	# a floating point number with optional sign and optional exponent
```

```awk
/^[A-Za-z][A-Za-z0-9]*$/
	# a letter followed by any letters or digits (e.g., awk variable name)
```

```awk
/^[A-Za-z]$|^[A-Za-z][0-9]$/
	# a letter or a letter followed by a digit (e.g., variable name in Basic)
```

```awk
/^[A-Za-z][0-9]?$/
	# also a letter or a letter followed by a digit
```

Since `+` and `.` are metacharacters, they have to be preceded by backslashes in the third example to match literal occurrences. These backslashes are not needed within character classes, so the fourth example shows an alternate way to describe the same numbers.

Any regular expression enclosed in slashes can be used as the right-hand operand of a matching operator: the program

```awk
$2 !~ /^[0-9]+$/
```

prints all lines in which the second field is not a string of digits.

Within regular expressions and strings, awk uses certain character sequences, called __escape sequences__, to specify characters for which there may be no other notation. For example, `\n` stands for a newline character, which cannot otherwise appear in a string or regular expression; `\b` stands for backspace; `\t` stands for tab; `\007` represents the ASCII bell character; and `\/` represents a slash. Escape sequences have special meaning only within an awk program; they are just characters in data. The complete list of escape sequences is shown in table below:

| Sequence   | Meaning |
| ---------- | ------- |
| `\b`       | backspace |
| `\f`       | formfeed |
| `\n`       | newline (line feed) |
| `\r`       | carriage return |
| `\t`       | tab |
| `\ddd`     | octal value __ddd__, where __ddd__ is 1 to 3 digits between 0 and 7 |
| `\c` | any other character __c__ literally (e.g., `\\` for backslash, `\"` for `"`) |


Table below summarizes regular expressions and the strings they match. The operators are listed in order of increasing precedence.

| EXPRESSION | MATCHES |
| ---------- | ------- |
| `c` | the nonmetacharacter c |
| `\c` | escape sequence or literal character c |
| `^` | beginning of string |
| `$` | end of string |
| `.` | any character |
| `[c1c2...]` | any character in c1 c2... |
| `[^c1c2...]` | any character not in c1 c2... |
| `[c1-c2]` | any character in the range beginning with c1 and ending with c2 |
| `[^c1-c2]` | any character not in the range c1 to c2 |
| `r1|r2` | any string matched by r1 or r2 |
| `(r1)(r2)` | any string xy where r1 matches x and r2 matches y; parentheses not needed around arguments with no alternations |
| `(r)*` | zero or more consecutive strings matched by r |
| `(r)+` | one or more consecutive strings matched by r |
| `(r)?` | zero or one string matched by r; parentheses not needed around basic regular expressions |
| `(r)` | any string matched by r |

### Compound Patterns

A compound pattern is an expression that combines other patterns, using parentheses and the logical operators `||` (OR), `&&` (AND) and `!` (NOT). A compound pattern matches the current input line if the expression evaluates to true. The following program uses the AND operator to select all lines in which the fourth field is __Asia__ and the third field exceeds 500:

```awk
$4 == "Asia" && $3 > 500
```

The program

```awk
$4 == "Asia" || $4 == "Europe"
```

uses the OR operator to select lines with either Asia or Europe as the fourth field. Because the latter query is a test on string values, another way to write it is to use a regular expression with the alternation operator `|`:






























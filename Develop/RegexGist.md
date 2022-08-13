# Regex Overview and Email Tutorial

Regex is a tool used to search for particular sets of characters.  It could be numbers, letters words, special characters, or any combination of them. Through accurate programming and syntax, Regex expressions can be used to find any pattern of characters within a document from phone numbers to email addresses.

## Summary

Regular expressions are tools that search for specific patterns - it's how the "find" function works on computers (ctrl/cmd + f). 
Using Regular Expressions, or Regex for short, searches can be made for literal and/or meta characters, with literal characters being specific characters ("a", "F", "1" or "!"), and meta being more broad categories - any uppercase letter, any lowercase letter, any number, or any character. Finally, regex expressions will look for any individual case of the characters it searches for, without repeating them in another match. For example, a search for the letters "the" in that order, will match the word "the" as well as the "the" in "these", and the "the" in "gather". 

Consider the following Regex:

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

<br>
With the above code, a user can search a document for any kind of email address. Below, you'll find out how it works.



## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Conclusion](#conclusion)

## Regex Components
There are several components involved in Regex.

- "." will match with any character 
    -  for example: A, 2, or % 
- "\\" will prevent special characters commonly used in Regex expressions from being part of the code.
    - Could be used for \. \\ \$ and more  

Within the following code: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>
you see various backslashes and periods. Within the square brackets, they're considered normal puntuation, however when you see the backslash between the parentheses, it is making the period, " . " be seen as an actual period, and not a match for any character.


### Anchors

Anchors will match the characters in the search based around where they are with an individual word. They can be used for finding specific word groupings, or letter/number sequences.

- $ matches a pattern when it occurs at the end of a string
    - for example, "hel$" will search for the "h-e-l" "bushel" and not "hello" or "shell"
- ^ matches a pattern when it occurs at the beginning of a string
    - this time, "^hel" will match the "h-e-l" in "hello" and not "bushel" or "shell"

Within the following code: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>
You can see the the carrot " ^ " at the beginning of the expression, and a $ at the end, noting that the phrases contained on either side of the expression must be at the beginning and the end of the regex, so there won't be excess spaces or characters on either side - you won't get @test@email.com or test@email.com.more as a match.

### Quantifiers

Quantifiers determine how many of a character type you'd like to match. 

- \* will match any amount of zero or more
    - For example, " o\*t\* " would match any number of "o" including in the words "lot", "boot", "knott" and even "oooh" and "belt".

- \+ will match one or more of a character. 
    - For example with " o\+t\+ ", it will match "lot", "boot" and "knott", but not "oooh" or "belt"

- ? will match with 0 or 1 of a character only.
    - For example, " o?t? " will match "lot", "oh" and "belt". 
    - It's commonly used for plurals in the form of "cards?" to match with "card and "cards" 

- {n} will match a character a specific amount of times. It must be a number in the curly brackets.
    - For example, " \w{4} " will look for any 4 letter word.
- {min, max} can be used to match a value within a range.
    - For example, " \d{4, 6} " will search for any sequence of numbers with 4 to 6 digits, whether is 1234 or 100000
- {min,} will match any number of characters starting with the specific digit or greater.    
    - For example, " \w{9,} " will search for words/alphabetical sequences with 9 characters or more, resulting in finding words like "tangerine" as well as "biologically"


Within the following code: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>
There are several quantifiers in this expression: 
<br>
With `[a-z0-9_\.-]+` a plus sign + is used to signify any of the characters inside the brackets could be matched, and there could be 1 or more of them.<br>
The second bracket expression is:
`[\da-z\.-]+` which is the same quantifier as above. <br>
<br>
Finally, there's `([a-z\.]{2,6})`, in which the {2,6} ensures that no matches will have a domain less than 2 and more than 6 within the email address, so .com, .edu, and .in could all work within the confines of the regex search.


### OR Operator
The " | " or OR operator, can be used to search for different items. For example, it can 

- | can be used as an "or" expression - it will search for two different items.
    - For example, John|Jon would search for both "John" and "Jon", 

Within the following code, there are no "or" operators.<br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>

### Character Classes
Character Classes can be considered anything within the square brackets. These are the literal or meta characters that are searched for with a regex.

- \w mean "word" - any characters A-Z, a-z or 0-9
- \W (capital 'w') means anything that is NOT A-Z, a-z, or 0-9

- \d means digit (any digit 0-9)
- \D (capital 'd') - any NON-digits

- " . " any character whatsoever.
- " .* " is a set of characters. just means, there's something there, but could be anything

- \s - white space (a space or a tab, or soooooometimes a line break)
- \S (capital 's') means anything that is NOT white space


Within the following code: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>
With the above code, there is 1 character class used - do you see it?: <br>
It's the \d in 
`[\da-z\.-]`<br>

While lowercase a-z and several special characters are also mentioned, the backslach and lowercase d says any number can be place in the domain name.

<br>

### Flags
Flags are letters that can be used to adjust searches by allowing for alterations or other circumstances. <br> 
There are four commonly used flags - i, s, m, and x, thought many languages have their own additional flags.

- "i" removes case-sensitivity, meaning a search will look for uppercase and lowercase letters

- "s" treats the match as a single line. This cannot be used with Javascript.
    - In Javscript, [\D\d] can be used instead

- "m" modifies the match by search for match over multiple lines. Commonly used with the " ^ " and " $ " anchors, it can search over the course of several lines.

- "x" is used at the end of a regex noting that there are access spaces in the regular expression that should be condensed. It's largely for the benefit of the programmer.

Within the following code, there are no flags
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>

### Grouping and Capturing
At times, a search may be created to search for specific characters as a grouping, which can be done using parentheses and/or backslashes. These groups are then entered into a numbered group to be reused with a backreference. We'll get to backreferences later on.

- " (hello) " would specifically return "hello" and add it to a backreferencing group.
- " (?:hello) " would group the regular expression allowing the user to apply operators, but a group isn't capture.
- " \1 " through " \99 " is for backreferencing the captured groups. (in Javscript  - see below for more)

Within the following code: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>
There are 3 groupings captured here - before and after the "@" sign and again after the " \. ".

These are largely used for keeping the expressions separated from one another.

### Bracket Expressions
- [] are used to match any individual or set of characters within the brackets.
    - for example, [a-z] will match all lowercase letters, and [xyz] will search for only the letters x, y, and z.

Within the following code:<br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>
There are 3 bracket expressions.
The first is: <br>
`[a-z0-9_\.-]` <br>
This says it could look for lowercase letters a-z, digits 0-9, underscore _, period or dot ., and a hyphen -. 
<br>
The second bracket expression is:
`[\da-z\.-]` <br>
which says, as previously mentioned, any digit can be matched, an a-z, and the punctuations period, and hyphen ( . - ).
<br> Finally, the last bracket expression is:
`[a-z\.]`<br>
This says the letters a-z can be used, as well as a period or dot ..

- Please note that the backslash next to the period . is considered an escaping character, allowing the . to act as itself, and not "any character" from the character class.


### Greedy and Lazy Match
It is important not to use "greedy" and "lazy" matches.  That is to say, matches that match the maximum number of quantifiers vs. matches that match the minimum number of quantifiers.

Consider the following "greedy" expression:
[b.+d]
One might think this would match any words that start with b and end with d, but due to the quantifier in between, it will find the first letter b in the sentence, then *every character in between*, before realizing it's hit the end of the sentence, at which point it will backtrack to find the last "d" in the sentence.
- If the sentence searched was "I'm eating bread and going to bed by dawn", it will match "bread and going to bed by d".

That error can be fixed with a lazy expression:
[b.+?d]
Here, the "?" changes the .+ quantifier to a lazy expression, by forcing it to always look for the next item in the search and moving on if it doesn't match.
- This time, the regex search would match with "bread" and "bed"

Within the following code there are no greedy or lazy matches: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>

### Boundaries
Boundaries, or word boundaries, can be used to place barriers around matches.
- " \b " is the syntax for the boundaries or beginning and end of a word. 
    - For example, a regex expression like " \b[dog]\b " will match every single word "dog", without matching pieces of words, such as the "dog" in "hotdog" or the "dog" in "dogma".

Within the following code: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>

while no specific boundaries are used, the forward slash typically donates a beginning and end.

### Back-references
Back-referencing is a way to recall previous groupings withing that expression. Remember grouping and capturing with parentheses? When a regular expression, or part of a regular expression is captured, it's given a number, starting with 1 and increasing with each group. That number works like a shortcut for the grouping. 
- \1 (up to \99 ) is how to call for a previously define grouping within that expression
    - For example, consider " ([1-5])\1\1 " will look for a sequence of 3 numbers, with each number being between 1 and 5. It could match 111 or 523, but not 501 or 126. That's because with both \1 back-references, it's repeating the call for numbers 1-5.

    Within the following code: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>
While there are parentheses being used, no backreferences are being used, although, one could claim ([a-z\.]) could be referenced in each of the 3 bracket expression, and thus a \1 could be used.

### Look-ahead and Look-behind
Lookahead and lookbehind, or lookarounds are similar to the start and ending anchors, although rather than returning the match, it only returns whether or not there was a match.

Positive and negative lookaheads look for items that are or are not followed by anything else (positive and negative, respectively).

Meanwhile, positive and negative lookbehinds do the opposite - respectively, they look for characters that do or do not preceed another.

Within the following code: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>
a greedy expression begins twice, signified by the two + signs. The first part adds all the characters within the confines of the bracket, but once it hits the at symbol, @, it ends. <br>
The second time, the greedy expression begins and continues through the end of the boundary, at which point, it backtracks to look for a period or dot .

### Conclusion
In concluscion, the following expression means this: <br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
<br>

The regex is looking to match a string that first contains either letters a-z, digits 0-9, an _, ., or and -, and as many characters as necessary, but they must follow an @.

Following the @, there must be another string of characters containing any digit, any lowercase a-z, ., or -, and as many of them as neccessary. Once find it, it will go to the end of the boundary and backtrack to find a period.

Finally, there must be final string following the period - the last section, which can contain lowercase letters a-z, or a period ..

There are 3 groupings (parentheses) in this, expression, and an anchor on each side, signifying the beginning of the expression (^) must not have anything before the first bracket expression, nor after the final bracket expression's contents ($).

The following will return as a match:

- jesse@email.com
- jj1134@haha456.wawawa
- te.st@te.st.te.st (remember how this is a greedy expression?)

The following will NOT return as matches.
- Jesse@Gmail.COM (because of uppercase letters)
- test!@te#st.5com (incorrect characters in each grouping)

## Author

Jesse is an HTML5 game producer in Brooklyn, NY, and an aspiring game developer. He's been coding for a short time, but has a background in screenwriting and experience in animation that he hopes to bring to his game design projects in the future.
[Jesse's Github](https://github.com/sweetfreak)

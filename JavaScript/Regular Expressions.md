## Modifiers

| Modifier | Description                       |
| -------- | --------------------------------- |
| /g       | Perform a global match (find all) |
| /i       | Perform case-insensitive matching |
| /m       | Perform multiline matching        |

## Brackets

| Bracket | Description                                                 |
| ------- | ----------------------------------------------------------- |
| \[abc]  | Find any character between the brackets                     |
| \[^abc] | Find any character NOT between the brackets                 |
| \[0-9]  | Find any character between the brackets (any digit)         |
| \[^0-9] | Find any character NOT between the brackets (any non-digit) |
| (x\|y)  | Find any of the alternatives specified                      |

## Metacharacters

| Character | Description                                                       |
| --------- | ----------------------------------------------------------------- |
| .         | Find a single character, except newline or line terminator        |
| \w        | Find a word character                                             |
| \W        | Find a non-word character                                         |
| \d        | Find a digit                                                      |
| \D        | Find a non-digit character                                        |
| \s        | Find a whitespace character                                       |
| \S        | Find a non-whitespace character                                   |
| \b        | Matches any string that contains zero or more occurrences of _n_  |
| n?        | Matches any string that contains zero or one occurrences of _n_   |
| n{X}      | Matches any string that contains a sequence of _X_ _n_'s          |
| n{X,Y}    | Matches any string that contains a sequence of X to Y _n_'s       |
| n{X,}     | Matches any string that contains a sequence of at least X _n_'s   |
| n$        | Matches any string with _n_ at the end of it                      |
| ^n        | Matches any string with _n_ at the beginning of it                |
| ?=n       | Matches any string that is followed by a specific string _n_      |
| ?!n       | Matches any string that is not followed by a specific string _n_  |
| \xxx      | Find the character specified by an octal number xxx               |
| \xdd      | Find the character specified by a hexadecimal number dd           |
| \udddd    | Find the Unicode character specified by a hexadecimal number dddd |

## Quantifiers

| Quantifier | Description                                                      |
| ---------- | ---------------------------------------------------------------- |
| n+         | Matches any string that contains at least one _n_                |
| n\*        | Matches any string that contains zero or more occurrences of _n_ |
| n?         | Matches any string that contains zero or one occurrences of _n_  |
| n{X}       | Matches any string that contains a sequence of _X_ _n_'s         |
| n{X,Y}     | Matches any string that contains a sequence of X to Y _n_'s      |
| n{X,}      | Matches any string that contains a sequence of at least X _n_'s  |
| n$         | Matches any string with _n_ at the end of it                     |
| ^n         | Matches any string with _n_ at the beginning of it               |
| ?=n        | Matches any string that is followed by a specific string _n_     |
| ?!n        | Matches any string that is not followed by a specific string _n_ |

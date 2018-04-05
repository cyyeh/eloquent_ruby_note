## Chapter 5: Find the Right String with Regular Expressions

### Matching One Character at a Time

- letters and numbers match themseleve (By default, case is important)
	- The regular expression aaa will match three a’s all in a row
	- The regular expression 123 will match the first three numbers
	- The regular expression R2D2 will not match r2d2
- punctuation characters have special meanings
	- period or dot character
		- `.`: match any single-character string including r and % and ~
		- two periods ( `..` ) will match any two characters, perhaps xx or 4F or even {!, but won’t match Q since it’s one, not two, characters long.
	- backslash
		- `\`: turn off the special meanings of the punctuation charac- ters
		- The regular expression `\.` will match a literal dot.
		- `Mr\. Olsen` will match exactly one thing: Mr. Olsen
- you can combine the different kinds of expressions to build up more complex patterns
	- The regular expression `A.` will match any two-character string that starts with a capital A, including AM, An, At, and even A=.
	- Theregularexpression`.r\.Smith` will match both Dr.Smith as well as Mr.Smith but not Mrs. Smith.

### Sets, Ranges, and Alternatives

- set
	- `[]`: match any one of a bunch of characters
		- The regular expression `[0123456789]` will match any single digit
		- `[aApP][mM]` to match am or PM and anything in between, like aM or Pm
- range
	- `[0-9]`: match any decimal digit
	- `[0-9a-zA-Z_]` will match any letter, number, or the underscore character
- some shorter shortcuts for common sets
	- `\d`: match any digit
	- `\w`: match any letter, number or the underscore (w stands for "word character")
	- `\s`: match any white space character including the vanilla space, the tab, and the newline
- alternatives
	- `|`: the expression will match either the thing before the bar or the thing after it
		- `A|B`: match either A or B
		- surround your alternatives in parentheses to set them off from the rest of the pattern, so that
			- `The (car|boat) is red`: match both The car is red as well as The boat is red.

### The Regular Expression Star

- asterisk `(*)`
	- matches zero or more of the thing that came just before it
	- `AB*` matches AB, ABB, A
	- `[aeiou]*` matches any number of vowels
	- `Rub*y` matches Ruy, Ruby, Rubbbbbby
- `.*`: one of the most widely used of all regular expressions
	- match anything, since `.*` is the same as `.`, `..` and `...` and so on.
	- `George.*`: match the full name of anyone whose first name is George

### Regular Expressions in Ruby

- encase your pattern between forward slashes
	- `/\d\d:\d\d (AM|PM)/`
- use the `=~` operator to test whether a regular expression matches a string
	- you can use regular expression matches as booleans
	- `/\d\d:\d\d (AM|PM)/ =~ '10:24 PM' # output: 0` 
		- the regular expression matched, starting at index zero
		- Ruby scans along the string, searching for a match anywhere in the string
	- `/May/ =~ 'Sometime in June' # output: nil`
	- `puts "It's morning!" if '10:24 AM' =~ /AM/`
- turn that case sensitivity off (`i` on the end of your expression)
	- `puts "It matches!" if /AM/i =~ 'am'`
- regular expressions also come into play in the string methods that involve searching
	- `@content.gsub!( /\d\d:\d\d (AM|PM)/, '**:** **' )`

### Beginnings and Endings

- match at the beginning of the string (`\A`)
	- `/\AOnce upon a time/`
- match at the end of the string (`\z`)
	- `/and they all lived happily ever after\z/` 
- match the beginning of the string or the beginning of any line within the string (`^`)
	- `puts "Found it" if content =~ /^Once upon a time/`
- matches the end of the string or the end of any line within the string (`$`)
	- `puts "Found it" if content =~ /happily ever after\.$/`
- match across the lines (adding an `m` to end of expression)
	- `/^Once upon a time.*happily ever after\.$/m`

### Staying Out of Trouble

- `=~` for regular expression match operator, not `==`
- regular expression matches return `nil` when there is not match, not `0`
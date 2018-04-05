## Chapter 4: Take Advantage of Ruby's Smart Strings
	
### String Literals
	
- single-quoted
	- the only fancy things you can do in a single-quoted string are to embed a literal quote in it, escaped by a backslash
	```
	a_string_with_a_quote = 'Say it ain\'t so!'
	a_string_with_a_backslash = 'This is a backslash: \\'
	```
- doubled-quoted
	- You can put characters like tabs and newlines in a double-quoted string with the appropriate character after a backslash
	```
	double_quoted = "I have a tab: \t and a newline: \n"
	```
	- embed arbitrary expressions in a double-quoted string by enclosing the expression between `#{` and `}`
	```
	author = "Ben Bova"
	title = "Mars"
	puts "#{title} is written by #{author}"
	```
- arbitrary quote mechanism
	- escape from the backslash Hell
	```
	# The character after the q is the actual string delimiter
	# Alternatively, you can use any of the other special characters 
	# as your delimiter, ending the string with the same character.
	
	# lowercase q => single-quote treatment
	str = %q{"Stop", she said, "I can't live without 's and "s."}
	# uppercase q -> doubled-quote treatment
	str = %Q<The time in now #{Time.now}>
	```
- span multi-line
	```
	a_multiline_string = "a multi-line
	string"
	another_one = %q{another multi-line
	string}
	heres_one = <<EOF
	This is the beginning of my here document.
	And this is the end.
	EOF
	
	# cancel multi-line string with a trailing backslash
	yet_another = %Q{another multi-line string with \ 
	no newline}
	```

### Another API to Master

- Like the collection classes, many of the string methods have counterparts whose names end with a !, which modify the original string instead of returning a modified copy.

```
# lstrip: return a copy of the string with all of the 
# leading whitespace clipped off
' hello'.lstrip # 'hello'
# rstrip: peel the white space off of the end of your string
'hello '.rstrip # 'hello'
# strip: take the white space off of both ends
' hello '.strip # 'hello'

# chomp: return a copy of the string with at most one newline character lopped from the end
"It was a dark and stormy night\n".chomp # "It was a dark and stormy night
# chop: simply knock off the last character of the string, no matter what it is
"hello".chop # "hell"

# upcase: get a copy of your string with all of the lowercase letters made uppercase
'hello'.upcase # 'HELLO'
# downcase: opposite from upcase
'HELLO'.upcase # 'hello'
# swapcase: 
'Hello'.swapcase # 'hELLO'

# sub: name is short for "substitute", search for some substring and 
# replace it with another (at most once)
'yes yes'.sub( 'yes', 'no' ) # 'no yes'
# gsub: replace as many substrings as it possibly can
'yes yes'.gsub( 'yes', 'no' ) # 'no no'

# split: break your strings into smaller strings
# Call split with no arguments and it will return an array containing 
# all the bits of your string that were separated by white space
'It was a dark night'.split # ["It", "was", "a", "dark", "night"]
# Pass a string argument to split and it will break things up 
# using that string as a delimiter
'Bill:Shakespeare:Globe'.split( ':' ) # ["Bill", "Shakespeare", "Globe"]

# index: searching for things than changing them
"It was a dark and stormy night".index( "dark" ) # Returns 9
```

### The String: A Place for Your Lines, Characters, and Bytes
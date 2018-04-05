## Chapter 2: Choose the Right Control Structure

### If, Unless, While, Until

```
if @writable
  @title = new_title
end
```

```
unless @readable
  @title = new_title
end
```

```
while ! document.is_printed?
  document.print_next_page
end
```

```
until document.is_printed
  document.print_next_page
end
```

- use `unless|until` instead of `if not|while not`
  - shorter
  - takes less mental energy(once you get used to it)

### Use the Modifier Forms

original
```
if @writable
  @title = new_title
end

unless @readable
  @title = new_title
end

...

```

better
```
@title = new_title if @writable

@title = new_title unless @readable

document.print_next_page while document.pages_available?

document.print_next_page until document.printed?
```

### Use each, Not for

- We tend not to use `for` loop, we use `each` method instead
  - Reason: Eliminating one level of indirection, since Ruby actually defines the `for` loop in terms of the `each` method

```
fruits = [ 'apple', 'banana', 'papaya' ]

fruits.each { |fruit| puts fruit }
```

### Case statement

- A multi-way decision statement similar to the `switch` statement

variant 1
```
case title
when 'War And Peace'
  puts 'Tolstoy'
when 'Romeo And Juliet'
  puts 'Shakespeare'
else
  puts "Don't know"
end
```

variant 2
```
author = case title
         when 'War And Peace'
           'Tolstoy'
         when 'Romeo And Juliet'
           'Shakespeare'
         else
           "Don't know"
         end
```

variant 3 (when no clause matches, value of author is `Don't know`)
```
author = case title
         when 'War And Peace' then 'Tolstoy'
         when 'Romeo And Juliet' then 'Shakespeare'
         else "Don't know"
         end
```

variant 4 (when no clause matches, value of author is `nil`)
```
author = case title
         when 'War And Peace' then 'Tolstoy'
         when 'Romeo And Juliet' then 'Shakespeare'
         end
```

- since `case` statement uses the `===` operator to do the comparisons(more on Chapter 12), we can use a `case` statement to do these things:
	- switch on the class of an object
	- detect a regular expression match

```
case doc
when Document
  puts "It's a document!"
when String
  puts "It's a string!"
else
  puts "Don't know what it is!"
end

case title
when /War And .*/
  puts 'Maybe Tolstoy?'
when /Romeo And .*/
  puts 'Maybe Shakespeare?'
else
  puts 'Absolutely no idea...'
end
```

### Staying Out of Trouble

- One of the best ways to lose control of your programming logic is to forget the fundamentals of the Ruby's boolean logic
	- only `false` and `nil` are treated as false
		- thus you should avoid testing for truth by testing for specfic values
	- If you are looking for `nil` and there is any possibility of `false` turning up, then look for `nil` explicitly 
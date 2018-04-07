## Chapter 3: Take Advantage of Ruby's Smart Collections

### Literal Shortcuts

array initialization
```
poem_words = [ 'twinkle', 'little', 'star', 'how', 'I', 'wonder' ]
# initialize an array of strings, where none of the strings have embedded spaces
poem_words = %w{ twinkle little star how I wonder } 
```

hash initialization
```
freq = { "I" => 1, "don't" => 1, "like" => 1, "spam" => 963 }
# If you happen to be using symbols as your keys(you don't care about the types of the hash keys)
# original
book_info = { :first_name => 'Russ', :last_name => 'Olsen' }
# shorten version
book_info = { first_name: 'Russ', last_name: 'Olsen' }
```

### Instant Arrays and Hashes from Method Calls

array
```
# The value of the stared parameter will be an array containg arbitrary set of arguments
def echo_all( *args )
	args.each { |arg| puts arg }
end

# You can only have on starred parameter, but it can be pretty much anywhere in your parameter list
def echo_at_least_two( first_arg, *middle_args, last_arg )
  puts "The first argument is #{first_arg}"
  middle_args.each { |arg|puts "A middle argument is #{arg}" }
  puts "The last argument is #{last_arg}"
end
```

hash
```
def load_font( specification_hash )
  # Load a font according to specification_hash[:name] etc.
end

load_font( { :name => 'times roman', :size => 12 })
load_font( :name => 'times roman', :size => 12 ) # if the hash is at the end of the argument list
load_font :name => 'times roman', :size => 12 # leave the parentheses off
```

### Running Through Your Collection

- Use `each` method
- Both hashes and arrays are equipped very extensive APIs
	- Array instances caryy around an even 100 public methods
	- Hashes include more than 80 public methods

**A key part of knowing how to program in Ruby is getting to know this extensive toolkit.**

array
```
words.each { |word| puts word }

# find_index
def index_for( word )
  words.find_index { |this_word| word == this_word }
end

# map
doc.words.map { |word| word.size }
lower_case_words = doc.words.map { |word| word.downcase }

# inject
# 0.0 in the example—is the initial value of the result. 
# If you don’t supply an initial value, 
# inject will skip calling the block for the first element of the array 
# and simply use that element as the initial result.
def average_word_length
  total = words.inject(0.0){ |result, word| word.size + result}
  total / word_count
end
```

hash
```
movie = { title: '2001', genre: 'sci fi', rating: 10 }
movie.each { |entry| pp entry }

# return a series of two element arrays
# [:title, "2001"]
# [:genre, "sci fi"]
# [:rating, 10]

movie.each { |name, value| puts "#{name} => #{value}"}
```

### Beware to !

- One thing you really want to know is which methods will actually change your col- lection and which will leave it be.

	```
	a = [1, 2, 3]
	a.reverse # a is still [1, 2, 3]
	a.reverse! # now a is [3, 2, 1]
	```

**Don't, however, get the idea that only methods with names ending in ! will change your collection.Remember, the Ruby convention is that an exclamation point at the end of a method name indicates that the method is the dangerous or surprising version of a pair of methods.**

- Be sure you know what a method is going to do to your collection before you call it.

### Rely on the Order of Your Hashes

- Ruby arrays and hashes have one thing in common that takes many programmers by surprise: They are both ordered.

### Staying Out of Trouble

- Several conditions to avoid
	- change the collection out from iterating methods
	```
	array = [ 0, -10, -9, 5, 9 ]
	array.each_index {|i| array.delete_at(i) if array[i] < 0}
	pp array # [0, -9, 5, 9]
	```
	- add element to array in wrong way
	```
	# Although you can plug new values anywhere you want,
	# Since arrays are continuous, the second line above instantly 
	# created 24,602 new ele- ments of array, most of them set to nil.
	array = []
	array[24601] = "Jean Valjean"
	```
	- use array or hash when there is better solution (**In coding, as in carpentry, you need the right tool for the job.**)
	```
	# scenario:
	# we are interested in knowing whether a specific word appears in a document
	
	# hash version
	word_is_there = {}
	words.each { |word| word_is_there[ word ] = true }
	
	# array version
	unique = []
	words.each { |word| unique << word unless unique.include?(word) }
	
	# better solution, using set
	require 'set'
	word_set = Set.new( words )
	```
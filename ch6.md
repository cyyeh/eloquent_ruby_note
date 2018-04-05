## Chapter 6: Use Symbols to Stand for Something

### The Two Faces of Strings

- Sometimes a good way to explain a troublesome topic is to engage in a little creative fiction. You start out with an oversimplified explanation and, once that has sunk in a bit, you work your way from there back to the real world.
	- In this spirit, let’s start our exploration of symbols with a slight simplification: Symbols are really just strings. 

```
# example of some ActiveRecord code
book = Book.find(:all) # pass in symbol(a flag)

# we can also rewrite code so that we could use a string 
# to signal that we wanted all the books
book = Book.find('all')
```

### Not Quite a String

- We tend to use strings of characters in our code for two different purposes
	- use for strings is to hold some data that we are processing (regular data processing tasks)
		- want to have the whole range of string manipulation tools
		- String class
	- represent things in our programs (for internal, symbolic, marker-type jobs)
		- using some characters to stand for something in your code, you probably are not very interested in messing with the actual characters
		- Symbol class

### Optimized to Stand for Something

- There can only ever be one instance of any given symbol
	- If I mention `:all` twice in my code, it is always exactly the same `:all`
	- figuring out whether this symbol is the same as that symbol is not only foolproof, it also happens at lightning speeds
- Symbols are immutable
- make ideal hash keys since symbol comparison runs at NASCAR speeds and symbols never change

### Staying Out of Trouble

- The best way to screw up with a symbol is to use it when you wanted a string, and vice versa
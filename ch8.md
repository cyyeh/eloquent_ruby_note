## Chapter 8: Embrace Dynamic Typing

### Shorter Programs, But Not the Way You Think

- Advantages of dynamic typing
	- (oft-repeated) write more compact code, since less declaration to variables
	- (much more significant) classes, modules and methods you never write at all
		- duck typing: Instead of looking at an object’s type to decide whether it is the correct object, Ruby simply assumes that if an object has the right methods, then it is the right kind of object

### Extreme Decoupling

- Ruby’s dynamic typing means that you don’t declare the classes of variables and parameters. That means that your classes are not frozen together in a rigid network of type relationships. In Ruby, any two classes that can work together will work together. Flexibility is a huge advantage when it comes to constructing programs.
- When you are coding, anything that reduces the number of revolving mental plates is a win. From this perspective, a typing system that you can sum up in a short phrase, “The method is either there or it is not,” has some definite appeal. If the problem is complexity, the solution might just be simplicity.

### Required Ceremony Versus Programmer-Driven Clarity

- Required type declarations inevitably become a ceremonial part of your code, motions you need to go through just to get your program to work
- With dynamic typing, it’s the programmer who gets to pick the right level of documentation, not the rules of the language
	- If you are writing simple, obvious code, you can be very minimalistic
	- if you are building something complex, you can be more elaborate. Dynamic typing allows you to document your code to exactly the level you think is best

### Staying Out of Trouble

- Engineering is all about trade-offs. Just about every engineering decision involves get- ting something, but at a price, and there is a price to be paid for dynamic typing
- Fewer mistakes, but not zero mistakes. Inevitably you are going to experience a type-related bug now and then. Unsurprisingly, you are also going to have non-type- related bugs as well. The Ruby answer to both kinds of bugs is to write automated tests, lots and lots of automated tests

- Ruby is a language for grown-ups; it gives you the tools for writing clear and concise code. It’s up to you to use them
	```
	# bad code example
	class Doc
	  attr_accessor :ttl, :au, :c

	  def initialize(ttl, au, c)
	    @ttl = ttl; @au = au; @c = c
	  end

	  def wds;  @c.split; end
  end
	```
	
- To take advantage of dynamic typing
	- Don’t create more infrastructure than you really need. Keep in mind that Ruby classes don’t need to be related by inheritance to share a common interface; they only need to support the same methods. Don’t obscure your code with pointless checks to see whether this really is an instance of that.
	- Do take advantage of the terseness provided by dynamic typing to write code that simply gets the job done with as little fuss as possible—but also keep in mind that someone (possibly you!) will need to read and understand the code in the future
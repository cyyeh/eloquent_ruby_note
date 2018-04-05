## Chapter 1: Write Code That Looks Like Ruby

### Basic Ruby style of programming
- Ruby style of programming is built on a couple of very simple ideas
  - Code should be crystal clear: good code tells the reader exactly what it is trying to do; great code shouts its intent
  - Code should be concise: it's much easier to understand what a method or a class is doing if you can take it all in at a glance
  
- Indent code with two spaces per level

### Comments

- Comments: anything following a `#` in the code is a comment
  - Ruby also supports multiline comments(`=begin` and `=end`), but Ruby programmers tend to stick with the `#` style of comments most of the time
- When is it a good idea to insert a comment into your code? And how much commenting is enough?
  - If it's obvious how someone would use your method, if the class or program needs no explanation, then don't explain it
  - Never put in a comment simply because you always put a comment there
  - Good reasons for adding comments to your code:
    - The best being to explain how to use your software masterpiece: Focus on exactly on "how to use the thing". 
    - Don't explain why you wrote it, the algorithm that it uses, or how you got it to run faster than fast
    - Examples are always welcome
- Other types of comments
  - background of the code: keep it separate from the instructions
  - "how it works" explanation(sometimes it's wise): keep it separate from the instructions
  - in-line comments
- Worst reason for adding comments: to make a badly written program somewhat comprehensible: that voice you hear in your head, the one whispering that you need to add some comments, may just be your program crying out to be rewritten
- Good code is like a good joke: It need no explanation
  
```
# Class that models a plain text document, complete with title, author
# and content:
#
# doc = Document.new( 'Hamlet', 'Shakespeare', 'To be or...' )
# puts doc.title
# puts doc.author
# puts doc.content
#
# Document instances know how to parse their content into words
#
# puts doc.words
# puts doc.word_count
#

class Document
  attr_accessor :title, :author, :content

  def initialize(title, author, content)
    @title = title
    @author = author
    @content = content
  end

  def words
    @content.split
  end

  def word_count
    words.size
  end
end
```
### Naming

- lowercase_words_separated_by_underscores
  - methods, arguments, variables, instance variables
- camel case
  - class, (constant)
- ALL_UPPERCASE_SEPARATED_BY_UNDERSCORES
  - constant

### Parentheses (are optional but are occasionally forbidden)

- conditions when forbidden
  - `puts "Look Ma, no parentheses!"`
  - method with no argument
  - conditions in control statements don't require parentheses

### Foding Up
  
- statements
  - Usually Ruby code sticks to the "one statement per line" format
  - How to fold: insert `;` between statements
  - exceptions
    - very, very simple class or method
      - `class DocumentException < Exception; end`
- blocks
  - `{ ... }` or `do ... end` (Ruby doesn't really care which you use)
  - Use `{ ... }` when
    - your block consists of a single and not too long statement
  - Use `do ... end` when
    - your block consists multiple statements
  
### Staying Out of Trouble

**folding code blocks**

[ x ]: single statement
```
doc.words.each do |word|
  puts word
end
```

[ v ]
```
doc.words.each { |word| puts word }
```

[ x ]: single statement but too long
```
doc.words.each { |word| some_really_really_long_expression( ... with
    lots of args ... ) }
```

---

**parentheses**

[ v ]
```
puts doc.author
doc.instance_of? Document
```

[ x ]: assemble two or more methods into a more complex expression
```
puts doc.instance_of? self.class.superclass.class
```

[ v ]
```
puts doc.instance_of?( self.class.superclass.class )
```

**The final code formatting rule is to always mix in a pinch of pragmatism.**

---
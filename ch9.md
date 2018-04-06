## Chapter 9: Write Specs!

- A key part of the Ruby style of programming is that no class, and certainly no program, is ever done if it lacks automated tests

### Test::Unit: When Your Documents Just Have to Work

- Test::Unit comes packaged with Ruby itself and is a member of the so called XUnit family of testing frameworks, so called because there is a similar one for virtually every programming language out there
- The very simple idea behind Test::Unit is to exercise your code in a series of individual tests, where each test tries out one aspect of the program
- In Test::Unit, each test is packaged in a method whose name needs to begin with test_

```
def test_document_holds_onto_contents
  text = 'A bunch of words'
  doc = Document.new('test', 'nobody', text)
  assert_equal text, doc.content
end
```

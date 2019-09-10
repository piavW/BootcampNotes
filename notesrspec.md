# demo advanced Rspec 4/9 with Faraz Naeem
(beginners guides are in the repository: ITPcourse/notes/TDDnotes)

R = ruby
Spec = specification
spec = example = text

**Spec definition:** executable example that tests the code in controlled context. testing a portion of the code rather than all of the things connected to the code. 

*simplified: Given some context, When some events occurs, Then I expect some outcome.*

Why test?
- helps to find bugs
- stimulates critical thinking
- cover edge cases (sad paths, different languages, timeszones, integers instead of letters)
- exposes poorly written code (smelly code)
- increases confidence when: refactoring/improving code, adding new features, updrading related software, during code deployments. 

We want to test:
- happy path
- sad path
- edge cases
- bug fixes

What not to test: 
- basic ruby / ruby on rails
- third party API
- behaviours that are already tested.

## Heart of RSpec
Write an expectation, see if it is met or not. expect().to ()
expect().not_to ()

**Matchers**
- Truthiness matchers (compare true/false values)
- Numeric-comparison matchers (compare numberic values)
- Collection matchers (compare arrays)
- Observation matchers (evaluate changes)
- predicate/dynamic matchers (used for methods that return tru/false). Gives better errormessages. 
    built in ruby methods:
        some_value.odd? #uneven?
        some_value.nil? #0/empty/nothing
        some_value.integer?
    In rspec: adding dynamic matches with build-in-ruby methods - only work with build-in rubymethods that end in a questionmark
    expect(some_value).to be_odd
    expect(some_value).to be_nil
    expect(some_value).to be_integer

    ex. 
    Custom method
        def voldemort?(name)
        name == 'Tom Riddle' ? true : false
        end
    with dynamic matchers
        expect(name).to be_voldemort
    without dynamic matchers
        expect(name.voldemort?).to be true

Example of matchers:
*expect().to eq() // eq is a matcher.*
- eq, be, raise_error, 

## Hooks
When writing unit test, it is often convenient to run steup and teardown code before and after you run your tests. Setup code is the code that configures or "sets up" conditions for a test. 
- Before - runs before the code
- After - runs after the code
- Around - runs during the code

## Test doubles -
allows you to test your code even when it relies on a calss that is undefiend or unavailable. they are stand-ins for objects. 
Different terms with slightly different usage. (ex. instance_double)
- Mocks
- Fakes
- Spies
- Stubs
    Why use test doubles? 
    - Easier to test
    - doesn't need to use expensive(data-heavy/slow) objects
    - when dealing with unpredictable responses
        - sending emails
        - different timezones
        - APIs

ex. 
book = double("book") #Creates a test double
account = instance_double("Account", name: "Pablo")

---

# demo about Debugging with Thomas Ochman, 5/9

## Debugging with RSpec 
Pry is one of the best Ruby debuggers. If you have it installed, you have to require it in the place you want to use it. 

By using a debugger you can get a sense of the current state of the object/application, which methods you can use, get answers to questions and bugs in your application. 

A simple example:
Create folder, create file Gemfile, add source https://rubygems.org/ add gem 'ruby'. 
You can also install a gem by in terminal write $ gem install rspec.
$ rspec -- init
#In .rspec add --format documentation
create spec/file_spec.rb 
require './lib/file.rb' in ur specfile

```rb
describe Person do
    it {expect(described_class).to respond_to :new} #is a oneliner
    it {expect(subject).to respond_to :name}
    it {expect(subject).to respond_to :name=}

    it 'has a name on instatiation' do
    expect(subject.name).to eq 'Thomas'
    end
end
```
#test it 
#create the required src/file.rb.
#test it
#create the 

```rb
class Person
    attr_accessor :name, 
end 
```
It can be onelined: class Person; end
#test again. 

In the `do .. end` block, if we have an object we use { }, 
When execute commands we can use { }. 

the `before { commands here}`
means we issue commands within {}
It's the same as: 
```rb 
before do 
command
end
```
FYI, attr_accessor is a built in method with getters and setters?
:name is a getter
:name= is a settermethod

### To install pry (a debugger) 
write gem 'pry' in Gemfile
then write bundle in terminal
require 'pry' in your spec_helper
in person.rb we also require 'pry'
then in your implementation code you add the below: 

```rb
def initialize
 binding.pry
end
```
The command "binding.pry" stops the program at that specific place in the code. 

### Self
Self is a keyword which return the object itself that we have creates. Through self.class we can see which person it is. Through self.methods we can see the possible methods to use with that class. On the top of the method-list we usually see the methods we've created ourself. 

self.class.respond_to?(:new) -> true
self.respond_to?(:new) -> false
self.respond_to?(:name) -> true

self.name= "Thomas" -> Thomas, if we put this under initialize the test goes green. 

self.name = "Thomas" we usually do @name = "Thomas" were we set the instancevariable of name to "thomas" 

If we, in pry, write next we see what's next... 

[WIP] <h2>Debugging with JavaScript </h2>
In JS the command `debugger`is put inside a javascript program. 

In browser, use inspect. 
Thomas will get back to us. 

---

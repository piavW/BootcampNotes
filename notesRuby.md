<h1> Notes for basic Ruby</h1>

TL;RL:
- string = "string"
- hashes = {}
- arrays = [] *can contain many - objects*
- symbols = !symbol
- integers = 123
- floats = 123.456

*Try to always use single quotes '' cause it saves processing power, use doublequotes "" if there's a need like string interprolation or you wrap a string in somethingelse*


Ruby/ irb - use https://www.codecademy.com/courses/learn-ruby/lessons/loops-iterators/exercises/the-until-loop?action=resume_content_item to learn more ruby! 
Especially hashes and arrays. 

Ctlr + C to quit Irb! 
För att testa koden: ruby nameofprogram.rb 
Börja koda ruby genom att skriva irb i terminal.

## DATATYPES
to know what class something is, type `objectname.class`

- **String**= a class, object type, for letters/characters, anything inside “ “  or ‘ ‘ is a string. 
- **Floats** =  numbers (and decimal numbers)
- **Integer** = whole numbers (a Fixnum class)
- **Booleans** = yes and no, true or false types,  no quotations! 
- **Arrays** = list/collection of objects (can have strings, floats, integers, booleans etc within) 
	- Create by: `Collection = Array.new` or `collection = [ ]`  objects in arrays are indexed/numbered starting with 0 collection[0] . 
	- PUSH/<< (also called the shovel method) 
    To add to an Array, use `objectname.push [the new thing]`. Or use `objectname << newthing`. 
	- POP to remove the last added variable from an Array use `collection.pop`.  
  Examples:  
	`my_array.first`  
	`my_array.laster`  
	`my_array[1]`  
	`my_array.push('horse')`  
	To delete by it’s index use `objectname.delete_at(indexnr exvis. 0)`  
- **Hashes** are collection of key-value pairs. 
	- To create a hash where :name is the key and “pia” is the value.   
  `Person = {name: “pia”, age: 27, weight: 59.5}`   
	`my_hash = {}`  
	`my_hash = Hash.new`
	- Hash[:key] tells irb to look in the hash for the :key and display the info.  
	`my_hash[:another_key]`

To return a key from a hash:
	```rb
	my_hash = {familykey: 'value', petskey: 'pets')
	my_hash.keys 
	#returns the following => [:family, :pets].
	``` 

To extract a hash from an array that contains a hash:
```rb
person1 = {name: 'Faraz'}  ((is a hash))
person2 = {name: 'Thomas'} ((is a hash))
people = [person1, person2]
people[0][:name]
```

## String interprelation
First write your method.
Arguments are the raw material that you pass in to a method. 
Parameters are placeholernames for an argument.
```rb
def my_method(parameter)
puts "my name is: #{parameter}"
end
```

## .each do 
.each do is an itterator which repets what is inside what is called on(on the left of the .)
.to_i makes the string digit into an integer
```rb
numbers = [1, 2, 3, 4, 5]
numbers.each do [digit]
	digit.to_i
	puts digit + digit
end
```

## To check even or uneven
```rb
if digit.even?
puts digit + 1
end
if digit.odd?
puts "uneven digit"
end
```

## To find methods
`numbers = [1, 2, 3, 4, 5]`
`puts numbers.methods` shows the methods available for the created object

```rb
def random_method(name = 'pia')
puts name
end
#returns pia when called
random_method('Becca')
# returns Becca when called
```


To print the strings inside an array as a greetings messge 
```rb
names = ['Thomas', 'Kalle', 'Anders']
names.each do |name|
  puts "Hello #{name}"
end
```
### FYI about hashrockets 
**`=>`** also called a Hashrocket 
This is no longer acceptable usage! But it separates the keys from the values in a hashmap literal. When used as the last parameter of a function the `{ }` aren’t needed for that hash. `f(:a => 1, :b => 2)`, f is called with one argument, which is a hashmap that has the keys :a and :b and the values 1 and 2.

```rb
# So instead of 
my_hash = {key => 'value'}
#write
my_hash ? {key: 'value'}
```


`x: “something”` means that the thing on the left has the same value as the thing on the right of the =>.      

---

# From the 11/8 lecture about Ruby:
Ruby is an object-oriented programming language. 
A high-level code-language, high-level code-language is written for humans, slower than low-level but more creative and can write more code in fewer lines. 
Low-level code-language is closer to the computer, like when you give a machine commands, executes faster. 

Everything in Ruby is an object - every object belong (is an instance of) a class. Being a part of a class gives it methods/power/functions.

Exampels:  
`x.nil?` Asks is there something in this? Answer will be true/false. 

`x is_a?` Nilclass/Fixnum/Integer etc asks about the `x.methods` shows the built in methods we can use for  that object. 

We can add our own methods to a class. The below code creates a method called say.hi. 
```rb
Def nil.say_hi
‘Hello World’
End
```

### Keywords
**Inheritance** - you can have a child/sub-class & a parent-class. The basic attributes are inherent from the parents. ¨

**`Super`** keyword - used to override a method that comes from a parent class to a subclass. 

**`Initialize`** - creates an instance of a class with their initial values. 

- attr_accessor : color (kan se koden och ändra koden
- attr_reader - Kan läsa koden
- attr_writer - Kan ändra koden?

`Nameofobject.color = ‘newcolor’` changes color.  

Code to create a new class and object. 
```rb
Class name
Def initialize 
@color = red
@doors = 5
End
end
```
Terminal input: `$ my_car = name.new`

`.methodname` används för att “tillkalla”/använda en metod. 
Man kan oxå använda flera metoder efter varandra/Chain methods.

`%w (x y)` är genväg för `[“x”, “y”]`, listar det som skrivs in 

### If-statement
```rb
If … = ..
Puts “Correct”
End
```
If-statement with multiple possibilities. 
```rb
If ...
  puts
elsif ..
  puts
else
  puts
end
```

### Unless-statement
```rb
Unless … = …
Puts “sometimes”
End
```
The opposite of if-statements, såvida inte det som kommer efter unless är True, så kommer det stå “sometimes”. 

```rb
my_array = ["cat", "dog", "world"]
my_array.each do |item|
  puts "hello " + item
end
```
Output will be: Hello cat, ny rad, Hello dog, ny rad, Hello world.

Hashes uses curlybrakets { }
Array uses hardbrakets: [ ]

Att hämta från en hash som är i en array `my_group[1][:age]`  om du skapat `hash = {name: “noel”, age: 34, gender: “male”}`, och skapat `hash2 = {name: “faraz”, age: 34, gender: “male”}`, sen `my:group [hash, hash2]` och därefter skapar din array `my_group = [hash, harsh2]`. 

String interprelation = när du ser en hashtag med curlybrackets vilket är när går in i en hash och tar information/upprepar information från en hash eller hashens key till en string. 

`.each do` is a helper method which is finished with the keyword `end`. We use pipes `| |`
```rb
my_group.each do |person|
Puts `#{person[:name]} is a #{person[:age]} year old #{person[:gender]}`
```
We use “” because we get data from a string usin string-interpolation. 

Method:
```rb
Def hello(name)
	“Hello”+” “+ name +” “+”how are you?”
End 
```
The space between `“ “` creates a space.. 
To call the method we write: `hello(“Pia”)`


You can also use logical or boolean operators. Ruby has three: and `&&`, or `||`, and not `!`. 
Ruby has the boolean operator not (!). !makes true values false, and vice-versa.
  - With `&&` both comparisons on the left and right must evaluate to true for the entire statement to return true. If the left side does not return true it will not bother trying the right side
- With `||` either the right or left side must evaluate to true. If the left side evaluates to true, the right side will not be tried because it has met the condition of one side being true.
- With `!` you reverse the result. If you’re false you’re now true. if you’re true you’re now false! Just think of it as opposite day!


## To change datatype or remove line
`.to_s` makes it into a string
`.to_i` makes it into a integral etc
`.chomp` removes the new line

### Arrays

`.product = `returns an array of all combinations of elements from all arrays.
```rb 
Arr = [15, 7, 18, 5, 8, 5, 1]
arr.index(5) visar att det finns tre stycken 5 i arr.
arr.index[5] visar error
arr[5] visar vad för information som finns på arr nummer 5
```

### Select
`select {|key, value| block} → a_hash`
`select → an_enumerator`
Returns a new hash consisting of entries for which the block returns true.
If no block is given, an enumerator is returned instead.
```rb
h = { "a" => 100, "b" => 200, "c" => 300 }
h.select {|k,v| k > "a"}  #=> {"b" => 200, "c" => 300}
h.select {|k,v| v < 200}  #=> {"a" => 100}
select! {| key, value | block } → hsh or nil
select! → an_enumerator
Equivalent to Hash #keep_if, but returns nil if no changes were made.
````


So if I want to get info from family
```rb
family = { brothers: [“Svante”, “Gustav”], parents: [“Thomas”, “ulrika”], cousins: [“louise”, “carl”] }
```
I write `brothers = family.select {|x| x[“brothers”]}`and then I get values withing brothers. 

---

# More advanced Ruby

# LAMBDA, blockers and Proc
source:
- https://www.rubyguides.com/2016/02/ruby-procs-and-lambdas/ 
- https://www.honeybadger.io/blog/using-lambdas-in-ruby/

## Blocks
Blocks är enclosed in a do / end statement or between { }, they can have multiple arguments. 
The argument names är defined between pipes ||.
For example, in single line blocks. 

```rb
[1,2,3].each { |num| puts num}
```
The |num| is a block with the arguments, the puts num is a block with the body. 

```rb In multi-line blocks:
[1,2,3].each do |num|
puts num
end
``` 
## Lambda
Lambda is a special Proc object. Lambdas are a way to define a block and it's parameters. the syntax is: `->` as in: `say_something ? -> { puts 'this is a lambda'}`. Alternative syntax: `lambda` instead of ->. 

You use the .call method to run the code inside the lambda. Other ways to run it:

```rb
ex_lambda = -> {puts 'lambda called'}
ex_lambda.call 
ex_lambda.()
ex_lambda[] #perfect to use instead of arrays
ex_lambda.===
```
Lambdas can take argumens as so `times_two = ->(x) {x*2}`. Upon `times_two.call(10)` we get #20.

## Proc
A Proc will return from the current context, a lambda will return normally, like a regular method. Procs don't really care about the number of arguments. 

Procs are defined with Proc.new {}

Procs and lambdas have the **closures** attribute:

This concept, which is sometimes called closure, means that a proc will carry with it values like local variables and methods from the context where it was defined.

They don’t carry the actual values, but a reference to them, so if the variables change after the proc is created, the proc will always have the latest version.

---

## Difference between Class method and instance method.
ex. 

```rb
class SayHello
  def self.from_the_class
    "Hello, from a class method"
  end

  def from_an_instance
    "Hello, from an instance method"
  end
end
```
>> SayHello.from_the_class
=> "Hello, from a class method"

>> SayHello.from_an_instance
=> undefined method `from_an_instance' for SayHello:Class


>> hello = SayHello.new
>> hello.from_the_class
=> undefined method `from_the_class' for #<SayHello:0x0000557920dac930>

>> hello.from_an_instance
=> "Hello, from an instance method"
We can't call an instance method on the class itsel, and we can't directly call a class mathod on an instance. 
To call an instance method we first have to create a new instance. 

## Index

index - is a built-in method in ruby to find the index of an array. 
So if we in library-challenge ask for 
`collection.detec{|b| b[:item][:title] == b}` we ask it to find the exact input using the detec method. 
`collecion.index {|b| b[:iteam][:title] == b}`it can find the index matching the title of previously inputted search.  

---

## Remove all instances of n from array
ruby
arr = [1, 3, 1, 3, 5]
arr.delete(3)
# now arr contains: [1, 1, 5]
## Remove item by index
ruby
arr = [1, 3, 1, 3, 5]
arr.delete_at(3)
# now arr contains: [1, 3, 1, 5]
## Conditional deletion with if
ruby
arr = [1, 3, 1, 3, 5]
arr.delete_if { |i| i < 2 }
# now arr contains: [3, 3, 5]

.
---
---

# WEEKEND-CHALLENGE: Library challenge
See the course material for Object Oriented Programming Fundamentals. 

Everything we need to complete this is in the ATM-challenge, find inspiration and bring your knowledge into a new domain. 
Be submitted by Monday morning! Use google, stackoverflow, notes etc to complete the challenge. Reference it in the readme! 

No codesupport on this one ;) 
  if lost - go through our atm-challenge-code. 

Thoughts:
Returndate - like expiredate! 
simple is better than complicated! 

## Reading and writing YAML-files (YAML Ain't Markup Language)
YAML-files are textfiles in which which we can store data in a orderly manner.

YAML is a human friendly data serialization stanard for all programming languages. 

Data serialization is a way to organise any thing of content. YAML is a kind of version of the same concept as Jason. It takes a piece of data and organises, stores it and structures it in a specific way. 


## Separation of concerns -
In the libararychallenge we use YAML to store the data in a data layer instead of storing it in a hash inside the logic layer. 

Even methods should be separated in the logic layer. 

## The YAML properties:

- syntax matters a lot
- whitespace indentation (indentation  & whitespace sensistive)
- used for storing information ( a set up file, list of books, list of customers)
- needs to follow a structure

### YAML format 

- :property:
    :title: 'Pippi'
    :author: 'Astrid Lindgren'
  :available: true
  :return_date: 
- :nextProperty:
    :title: 'Lotr'
    :author: 'Tolkein'
  :available: false
  :return_date: 2019_10_22
- :nextNextProperty: 
etc...

Takes the info from a file and returns it in a ruby array with hashs with key value pairs. Means that we can use the hash-methods on it to manipulate data, add data, delete data, amend data.

### Reading and writing YAML

`File.open('some_file_name.txt', 'w')` the w tells us we want to write to files with ruby
`File.open('some_file_name.txt', 'r')` the r tell us we want to read files with ruby 
`File.open('./lib/data.yml', 'w') { |f| f.write colletion.to_yaml}` using a codeblock to add information to yaml

VERY CASE SENSITIVE
IN IRB - not the same as open and writing a YAML file. File-suffix is .yml
```
open irb
  require 'yaml' => true
create a variable:

```
collection = YAML.load_file('.lib/data.yml)
collection => gives us the array with hashes inside
`collection.select {|book<is the iteration variable>| book[:item][:title].include? 'Pippi'<can also use "">}`

To modify the first object in the YAML file, which is currently set to :true 
`collection[0][:available] = false => false` 
Now we need to store/write the information in the YAML file
`File.open('.lib/data.yml', 'w') {|book| book.write collection.to_yaml}`
First we tell it to open and that we want to write, then within the curlybrackets we make the item book accessible for us to manipulate, by the book.write colletion.to_yaml we're saving it. 
then you want to find the book again to show ruby it's changed.
`collection.select {|book| book[:item][:title].include? 'Pippi'>}`

To check out:
we need to change a specific books:
- availability : true/false
- return date : set_return_Date and nil

We know how to access the first books availability
We don't know how to access any other books availability.... 

visitor searches for book by title or author $
sees if it is available (shown when u've searched) $
if available - visitor checks out 
searched book changes availability,
searched book gets return date
visitor gets a list of checked out books and their return date (or just the entire info of the book with availability and all?)  as in statusmessage for withdraw case when. 

We don't have a userstory or need to create a check back in for book....! 
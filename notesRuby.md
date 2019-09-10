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
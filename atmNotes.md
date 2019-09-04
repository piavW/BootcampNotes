<h2> First week, ATM-challenge demo</h2>
ATM - prints out an amount of money to the right person. 
Pieces: Person - ATM - Account (could have a debit card aswell)
- The person Class needs: card, pin code, name, money. (class is an entity that creates or contains something. It has built in methods to use). A class has different things/methods/functions that do particular things. The class holds it together. 
- Account Class needs: money, account number. 
- ATM Class has: money.

How to organize your code, the three layers of code: visual layer, logical layer, data layer. Spagetticode is the opposite, when it's hullerombuller. 
- Visual layer - the interface/what the user sees/the HTML-page
- Logial layer - the computations, confirmation that it's the right person, that it needs to pay this amount, conditions
- Data layer: the code storage, where data is kept: user name, account number etc. The logical layer goes to the data layer to access information. 

In this challenge the visual layer will be the irb. Your data will also be stored here in this challenge. 
the logical layer will be touched upon this weekend. 
the data layer we won't do anything with in this challenge. 

<i>Demo demo - this is all in the coursematerial as well</i>
Create ur mkdir in terminal, click the link in course material (get u to github), fork the repository, clone the url for my own repository, check git st, will see initial commit and updated readme. 
Good idea to paste in the user story from the design sprint in the README. 
Unitest ur code - means set up rspec: 
touch Gemfile
open it & add:  
source 'http://rubygems.org'
gem 'rspec'
in terminal do git st
do a git add & commit & push (in present time, explain what I'm doing - adds a user story to readme, greates gemfile, adds rspec)
in terminal
bundle install
rspec --init
in the .rspec file (open it through code . in terminal) add 
-- require spec_helper 
-- color 
-- format documentation

The other programmers you're codeing with will during the course of the pairprogramming do Git pull, work a bit, make a commit and push it up. 

Also add a .gitignore file - se course documentation. 

Then intialize the ATM and add a method to withdraw funds, create a file spec/atm_spec.rb 
In atm_spec.rb
```rb
require './lib/atm.rb'
describe ATM do
it 'has .....' do 
atm = ATM.new
expect(atm.funds).to eq 1000
end
end
```
Because we have ATM up in describe we can write subject inside the expect(subject.funds) and then don't need atm = ATM.new
test ur code through rspec
git add & commit
push it to pairingpartner who will create the next folder & file we need, i.e. the /lib/atm.rb
In atm.rb create class 
class ATM 
end
run rspec
create method funds
in class:
attr_accessor :funds
run rspec
in class to initialize the method:
def initialize
@funds = 1000
end 
run rspec
git add & commit

Create a new spec and it-block in atm_spec

Add subject.withdraw(50) to it-block
run rspec
add withdraw method to atm.rb ATM class 
def withdraw(amount)
end
run rspec
In def withdraw
@funds -= amount 
git add & commit





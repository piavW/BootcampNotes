# Notes about JavaScript starting with week 2

For beginners JS notes go to my github repository ITPnotes. 

---

## Introduction to JavaScript ES6 with Faraz Naeem

ECMAScript organisation - created to standardise the JavaScript language.

Features added (more about this on es6-features.org):
- classes & modules (previously had prototypes)
- constants (previously had var)
- iterators and for/of loops 
- arrow functions
- binary data
- typed arrrays (can declare the array only contains strings, or intergers)
- collections (maps, sets, weak maps)
- promises 

The ES5 version (aka ECMAScript 5 version) can be handled by all browsers. 
The ES6 version (also called ES2015) is supported by chrome, firefox, opera, safari, explorer edge(?). 
We need to make sure our code is supported by the browsers. 
We use the transpilation tool BABEL to change our code to function with the right broswers.

### var .vs let/constant
The old way to declare a variable: 

```js
var myVariable = 12
console.log(myVariable)
```
We use *var* for special cases, like when we're dealing with a global scope. 

**Var is a global variable!**

The new and optimal way to declare a variable:
**let is a local variable!**

```js
let myNewVariable = 'Faraz'
myNewVariable = 'Thomas'
console.log(myNewVariable)
```
We use let when we know we'll reassign the value of the variable. 

```js
const myArray = [1,2,3]
console.log(myArray)
```

the *const* is used then the variable value isn't supposed to be reassigned. We can't reassign by coding `myArray = [4,5,6]` if we do we'll get an errormessage since we're not allowed to reassign the variable value of the const. 
**However** we can manipulate the data like add something to the const by myArray.push(4) or delete things myArray.pop(4) for example.

### Template string/string templating (called string interpolation in Ruby) 

```js
let faraz = 'Faraz'
console.log('Hello ' + faraz + '!')
```

The new prefered way (because it looks nicer) to do this using backticks and curly-brackets.

```js
let sverrir = 'Sverrir'
myGreeting = `Hello ${sverrir}!, how are you?`
console.log(myGreeting)
```

### Arrow functions
Old-fashioned way to write anonymous functions (anonymous functions are basicly callbacks)

```js
let sverrir = 'Sverrir'
myGreeting = `Hello ${sverrir}!, how are you?`

function greeting() {
    console.log(myGreeting)
}

greeting()
```

When we use anonymous functions we don't want to give them names cause we're only gonna use it once inside a certain scope. It's annoying to write function(){} over and over again. We use the rocket/arrow (hash-rocket in Ruby-speak). 
We can use let, const etc. 

```js
let sverrir = 'Sverrir'
myGreeting = `Hello ${sverrir}!, how are you?`

//this is a function called greeting with arguments
let greeting = (arguments, argument1) => {
    console.log(myGreeting)
}
greeting()
```

In the course-documentation:
classes, array helpers, destructing assignment. 

### Callback
Call-back is a function that will run after another function is completeted. In that case we don't need to specify or delare the function in a certain way. We don't need to give it a name. Can just put 

```js
(arguments, argument1) => {
    console.log(myGreeting)
}
```

If we put the let myGreeting inside the greeting-function only the greeting-function can read the let myGreeting. 

```js
let sverrir = 'Sverrir'

let greeting = (arguments, argument1) => {
let myGreeting = `Hello ${sverrir}!, how are you?`
    console.log(myGreeting)
}
greeting() //greeting can be found
console.log(myGreeting) //this can't be found since myGreeting is hidden within the greeting function.
```

--- 

# More about JavaScript

## REPL (Read-Eval-Print-Loop)
also called: interactive top-level or language shell. Is simple, interatice computer programming environment that takes single user inputs, evaluates them and returns the result to the user. 

REPLs facilitate exploratory programming and debugging because the programmer can inspec the printed result before deciding what expressions to provide for the next read. It gives us immediate feedback if we have any errors in our code.
Using a tool called repl.it <https://repl.it/> we can add code directly to the section, press run, and will get an output directly in the section. 

### Defining an arrow function:
(param1, param2) => { statements }
When we don't use curly bracket the arrow function has an implicit return meaning it will return the value

(param1, param2) => expression
This way of writing arrow functions is the same as the one above, but when we write an arrow function with curly brackets then we need to have the return keyword.

(param1, param2) => { return expression; }
If we are writing arrow functions without parameters then we need to have brackets to define the function.

() => { statments }  
() => expression  
() => { return expression; }

You cannot use `return` outside of a function. 

Example: 
Non-working
```js
function greet(value, callback) {
  callback(value)
}
// Create a callback function
function cb(val) {
  console.log('Sup ' + name)
}
// Pass that as an argument to the `greet` function
greet('Ryan', cb) //gives us Sup but no Ryan.
```

Working 
```js
function greet(value, callback) {
  callback(value)
}
// Create a callback function
function cb(val) {
  console.log('Sup ' + val)
}
// Pass that as an argument to the `greet` function
greet('Ryan', cb) //Gives us Sup Ryan, since we told the funciton cb to add the val after the sup in console.log()
```

However, we can ommit the creating of the callback function completely, if we instead use the arrow function and write the following in **ES6!**

```js
function greet(value, callback) {
  callback(value)
}
// Using an Arrow function
greet('Clarissa', (val) => console.log(`Bonjour ${val}`))
//this prints Bonjour Clarissa
``` 

## Destructuring
gives us the ability to extract data from objects and arrays and set them with new variables.

example:

```js
// Array Matching
let persons = ['Jane', 'raoul', 'bob']
// Before es6
console.log(persons[0])
console.log(persons[1])
console.log(persons[2])
//gives Jane, raoul, bob on new lines
// With es6+
let [ jane, tom, name3 ] = persons
console.log(jane)
console.log(tom)
console.log(name3)
//gives Jane /newline/ raoul /newline/ bob 
let [name1, ...rest] = persons
console.log(name1)
console.log(rest)
//gives Jane /newline/ ['raoul, 'bob]
```
So it's easier to call the array[indexnr] by a string-variable instead of array[indexnr].


New example:
```js
// Object Matching
let people = [
  {name: 'Raoul', gender: 'male', age: '40'}, 
  {name: 'Jane', gender: 'female', age: '20'}
]
// Before destructuring
people.forEach((parameter) => {
  console.log(`Hi, my name is ${parameter.name}, I am a ${parameter.age} year old`)
})

// With destructuring
people.forEach(( {name, age} ) => {
  console.log(`Hi, my name is ${name}, I am a ${age} year old`)
}) 
```

When we put the parameters inside curly-brackets we change them from parameters to variables of the specified key value pairs created in the people array with hashes with key:value-pairs. We then don't need to specify the parameter before calling the key-name. 

We can also rename the :keys to something else:
```js
// Rename with destructing
people.forEach(({ name: n, age: a }) => {
  console.log(`Hi, my name is ${n}, I am a ${a} year old`)
})
```
## For Loop vs. Array.forEach()
The for-loop

```js
let people = [
  {name: 'Raoul', gender: 'male', age: '40'}, 
  {name: 'John', gender: 'male', age: '20'}
]

for (var i = 0; i < people.length; i++) {
  console.log(`Hello, ${people[i].name}`)
}
```

// in Ruby
// people.each do |person|
//   puts "Hello, #{person.name}"
// end

**Here are 2 ways to write the Array.forEach() loop**

```js
people.forEach(function(person) {
  console.log(`Hello, ${person.name}`)
})
//this is one way to write it
people.forEach((person) => {
  console.log(`Hello, ${person.name}`)
})
 //this is another way to write it
 people.forEach(person => console.log(`Hello, ${person.name}`))
 // Can also be writen as follow
```

### map() method
The map() method creates a new array with the results of calling a provided function on every element in the calling array.

---

# demo Asynchronous programming with JavaScript with Faraz Naeem
Source with good information: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous

The problem is that the Processor - CPU - processes one thing at the time, it won't do the next thing before it's done with the thing it's doing, this creates a que and your program waits until it's finished, - this is **synchronous programming**.

With **asynchronous programming** we execute more than one action/function at the same time. We have no stopping-actions. 

This allows multiple things to happen at the same time, when you start a blocking action, the program will carry on. When the action is finished, the program will be notified and will get access to the results.

Asynchronous code is much faster than synchronous code (we're talking miliseconds), your code is cleaner, the user experience is better. 

Solutions for async-code
- callbacks (outdated now)
- promises (comes with ES6)
- async/Await (now the prefered way)

### Callbacks
We pass in another function as an argument. 
//Arguments are the raw material that we pass into a function. If I want a function to write my name, I'll pass in my name as an argument. 

callback tell the program to wait until the next function completes. 
Once we start calling callbacks, we need to call them on and on and on which leads to a huge callback que aka callback hell. 

### Promises
syntax: 
```js
new Promise(
    function (resolve, reject){
        //here we create our resolve function {
        };
        resolve(//functionname);
        }else {
            //here we create our reject function{
            reject(reason);
            }
   }
);
```

### Async/Await
By placing async infront of a function that makes it asynchronous with a built in promise. 
by putting await before the promise is resolved.
myFunction()
.then
.catch


## [WIP]more stuff 
Javascript (ES5) doesn’t have a formal class notation, but you can create a “constructor” function and add methods to it. Examples from here.

```js
function Person(first, last) { 
    // create "constructor"
    this.first = first;        
    // public variables -- reference current object
    this.last = last;

    this.setName = function(first, last){ 
        // public function
        this.first = first;
        this.last = last;
    }
}

Person.prototype.fullName = function() { 
    // extend prototype
    return this.first + ' ' + this.last; 
    // even at runtime!
}

var bob = new Person("Thomas", "Ochman"); 
// "new" creates an object
bob.fullName();               
// "Thomas Ochman"
```

## Exercises:
### Excercises #1

- 1. Create an array and add three numbers to it.
```js
let myArray = [1, 2, 3]
```

- 2. Use your array to return the second number.
```js
myArray[1]
```
- 3. What data type is 123/12? 
the result of 123/12 is a Float, however the entire 123/12 is a NAN(Not-A-Number)

"Things in quotes!"? 
String

undefined?
is undefined, it represents the primitive value undefined which is one of JS's primitive types.

- 4. Write an if statement that returns true.
```js
 if (myArray.length == 3) {
console.log("True bitch");}
else {
console.log("Wrong bitch");
}
```
- 5. Consider these two arrays: myArray = ['Thomas', 'Amber', 'Raoul'] and emptyArray = []. Use a for loop to add our names to emptyArray. (Hint: n needs to be the length of the array. Google a helper method for finding the length of an array in Javascript. Is it the same as Ruby?)
```js
myArray = ['Thomas', 'Amber', 'Raoul'] 

emptyArray = []

for (i = 0; i < myArray.length; i++) {
emptyArray += (myArray[i] + " ")
}
console.log(emptyArray)
```


### Excercises #2
1. What is this? Does it have an equivalent in Ruby?

This is an object, kind of like the self in Ruby, it refers to the current calling context. 

In a function, this, refers to the global object but can be something else depending on how the function is called.
In a method, this, refers to  the owner object.

2. The previous Person class is written with ES5, now that we've learned about ES2015, convert the above code class to an ES2015 version using the new class syntax
```js
function Person(first, last) { 
    this.first = first;        
    this.last = last;
 { return `${this.first + " " + this.last}`}   
}
Person("Thomas", "Ochman")    
```

As a class:
```js
Person = class { 
  constructor(first, last) {
    this.first = first;        
    this.last = last;
  }

get fullName() { 
  return this.extraMethod()
  }   
  extraMethod() {
    return `${this.first + " " + this.last}`
  }
}

const bob = new Person("Thomas", "Ochman")
bob.fullName
``` 

---


## PROTOTYPE
So when adding a prototype to a constructor function like Person, we add a parameter to that constor function ((like in Ruby when we add a attribute to a Person Class)).

---------- ES5 ----------  
```js
function getObj() {
  return { a: 1, b: 2, c: 3 };
}  
```
---------- ES6 ----------  
Note the () to differentiate with actual code block  
```js
const getObj = () => ({ a: 1, b: 2, c: 3 });
```

### explaination of THIS
https://www.reddit.com/r/javascript/comments/7yki4d/explain_like_im_5_this/
ELI5 would be:

All functions in JS are methods on objects, called liked this: myObject.myFunction(). this is the object before the . when you're in myFunction (in this case, it's myObject).

Special case 1: if you call a "naked" function (in the global context), this is simply the global object (because myGlobalFunction === window.myGlobalFunction)

Special case 2: If you don't like that rule, you can always bind a function, to explicitely set its this once and for all.

Special case 3: If you don't like that rule, you can apply or call a function, to explicitely set its this just this one time.
 
#### In my own words: asynchronous code, Async and Await 
source: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await
[HOMEWORK] - by own words explain what asynchronous code is, explain what async and await it. Slack Faraz with it before tomorrow morning! DONE.

**Asynchronous code** is when we want our code to execute more than one thing at the same time. In synchronous code, our code executes one statement after the other, like in a que, before the code continutes the current statement needs to have been loaded and/or executed and/or finished. With asynchronous code the program doesn't have to wait for a specific (often data/time-demanding) statement/piece of code to execute, the (sometimes called) heavy-code can be executed/computed by another instance/processor-core/API whilst the program continues to run. The other instance lets the program know when the heavy-code has finished it's execution. 

**Async**
When one puts the async-keyword ``async```before a function declaration it turns the function declaration into an asynchronous function declaration automaticly. An async function knows how to interprate the possibly added await-keyword, Most importantly, an async function also turn any function into a promise. 

You can put async-keywords before class/object methods to make them return promises and await promises inside the codeblock. 

You can also put the async-keyword in like the following examples:

```js
let hello = async function() { return "Hello" };
hello(); 
```
And you can use arrow functions: 

```js
let hello = async () => { return "Hello" };
```
To actually consume the value returned when the promise fulfills, since it is returning a promise, we could use a .then() block:

```js
hello().then((value) => console.log(value))
```
or even just shorthand such as 

```js
hello().then(console.log)
```

**Await**
The await-keyword is put in front of any promise-function (must be an async function!) where you want the code to stop and wait until the promise fulfills. During this waiting-time other code/tasks that may be in que to be exectued can execute, when the promise returns it's result the code continues with the next line. However, the await-keyword blocks all your code following the await-keyword until the promise is fulfilled and the result returned. ex.

```js
async function hello() {
  return greeting = await Promise.resolve("Hello");
};

hello().then(alert);
```

---

# 10/9 Intro to the adressbook challenge (week 2)

Build an address book, with: name, adress, mobile number, image or avatar (later twitterfeed etc). On a website that is deployed for anyone to go in and add their details, or we can add their details. 

- Testdriven development approach - unittest in Mocha & Chai (unittesting zooms in on small portions of the application)
- Behaviourdriven development approach - using Cucumber 
- Branches!
- Local storage
- DOM (document object model - js interactino to the html-page) manipulation usin vanilla JavaScript API
- deploy to GitHub or Netify
- Difference between running code on the server vs. browser

## BDD (behaviour driven development)
**Using Cucumber**

- reduce common wasteful activities
- the Behaviour is the larger features of the application
- We are testing and creating the application in the same way the user would interact with the application. 

Using Cucumber to write featuretest/scenario, run the test in terminal, gives us output with failing tests, add that too code, makes so each of the steps pass. 

## LocalStorage
a type of webstorage that allows JS website/apps to store and access data right in the broswer - with no expiration date (the data stored in browser will persist even after the browser window has been closed).

This means that if we deploy the site the info I have will not exist in Clarissas browser. 

In your browsers inspec window under Application you can see what info is stored. 

Cookies are also stored in your browser - it's not direct LocalStorage though.

Before every new feature you can to create a new branch! Then you merge the branch in - through a pullrequest, then create a new branch from the master branch for the next feature. 

## Whiteboard session about BDD
*Feature/acceptance testing*
Cucumber fills out the information in ex. a login page and clicks the 'login' button. 
One can of course do this manually, but it's timeconsuming and stupid. Better to do automated testing like with cucumber. 

Add a unique scenario, in the step definition file you have your expect-blocks. 
Creates scenarios for all types of users of the application, pagevisistor, admins etc. 

When should you just between BDD and TDD: 
1. start with the BDD (cucumber) featuretest and scenario
2. work on the featuretest going green
3. when error occurs which we can't handle/fix with featuretest, then we go to TDD(rspec) and change the backend/data/unittesting code. 
4. Work on it through testing and passing the test in TDD.
5. Jump back to BDD until that goes green, go back to TDD when necessary. 

When writing features/scenario we think like a user of the application. 
Create a feature file, add scenario, write implementation code. We can mock up objects etc in our BDD code. 

---

# demo Styling the addressbook with Faraz Naeem 11/9
Using a semantic-UI: http://semantic-ui.com
install through node or manual install through download.

CDN (content delivery network), you need an internetconnection, the CDN needs to be up and running. Good for smaller projects, when we do larger projects where we want control we download a pakage. 

googlesearch for: semantic-iu cdn, go to page, chose one called semantic.min.css copy the link. Go to your code, in the html, under Head tag, add <link rel="stylesheet" href="post the link here">

The font should change - that's how you know the stylesheet is working.

To change the button we go to semantic-ui webpage, chose a stylesheet for a button in the tab on the left. 
CLick on link and you can see the sourcecode, copy the code which will be for a class. 
In html you replace the button class="" with the new code. 
If we change the class to an id, we can in app.js change the '.new-contact-form' to a '#new-contact-form' then it knows to look for an id instead of a class. Since we use document.querySelector...

**read up on querySelector, classes and id in JS. 

containers affect the elements, they're mobile friendly.

when u change index.html or add styling, always run cucumber again because you'll be changing stuff and information.

They work by replacing the classes. Semantic-ui is the most react-friendly one out there. 

No need to add Jquery, to add animations - use vanilla JS. 

Go banans with styling.
remember to run cucumber on a regular basis to make sure ur not breaking code.
style when you've completed the implementation code!

styling is tough cause it's easy to get into a rabbit hole - make sure u commit on a regular basis!


In the app.js we add the styling inbetween the backticks ``. 

--- 


## JS functions in own words:
A function with an object as a parameter. 
```js
const functionname = objectparameter => {
  objectparameter.propetyname = propertyvalue;}
```
Another function with a object as a parameter which has key:value pairs. 
```js
let spaceship = {
  'Fuel Type' : 'Turbo Fuel',
  homePlanet : 'Earth'
};
```

# Reminders for myself

Remember that **if-statement syntax**: `if (jklfds==true) {} else {}`

**Function declaration syntax:**
`function functionName () => {}` 
`const functionName () => {}` 
**Unnamed methods syntax:** 
`functionName = () => {}`


---

# Lessons learned from HTML and JS
In html you need to define the class before you add the action. example: `<form class="new-contact-form" action="#"> ` if you have the action before the class, html doesn't know what it is. 
the Css and Js knows that we refer to a class when we put a dot before the class name `('.new-contact-form')`

Some CSS to try to get things centered:
#body{
margin-left: 50%;
    margin-top: 50%;
    transform: translate(-50%, -50%);
}

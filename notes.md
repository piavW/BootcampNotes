# Notes from the Bootcamp 

## HTML: span, div, script basics
The `<span> </span>` tag is used for grouping and applying styles to inline elements. 
Which is different from the `<div> </div>` tag which is used for grouping and applying styles to block-level content. 

To use Javascript inside the html dokument without creating a new .js file the javascript code can be wrapped within `<script type="text/javascript">code here</script>`.

---

## Communication within the bootcamp
STAY HUMBLE! Like a humblebumblebee 
 Communicate too much - don't asume the other person understands you. 
- Ask questions! All of them! Be precise: 
    - what doesn't work? 
    - why do you think it doesn't work?
    - what and how did you try to do?

**Don't**: bulldoze, keep things to yourself, be intimidated, be passive aggressive/sarcastic, have a negative outlook - it is hard by design to challenge us.

Daily tools: 
- Slack (important messages save on computer, it deleted history after a few weeks). 
All codeing questions in the main channel! 

**Format your code** before you send it into slack! *`shift + enter for new line, write your code, end codeblock with`* Or add a `backtick` infront and at the end of the word or phrase for just a word/phrase. 

- morning Scrums at 9 o'clock. Be precise! 
    1. What have you been working on? (technical things)
    2. Any blockers? 
    3. What's the plan for today?

- Google Meet and Google Hangout (open hangout by typing /hangout )

- Restrospective: Everyotherweek, talk about personal struggles, positives, broad discussions.  
- SALPS: personal reflections. 

- **Working hours**: Mon-Fri 8:30 - 17:00 (19:00-21.30 sometimes)
Coaches not avaliable Tues 10-11, Thurs 10-11, Sat and Sun. 
Office Hours (coach is available) Mon, Wed, Thurs 19-20.30. Primarily debugging. 

- **Support Flow**
    - Check syntax & naming
    - Use Pry for debugging
    - Make sure you're in the right folder
    - Go through the scenario/feature/unitspecs
    - cross check it with the story, are you within scope?
    - Google the error message
    - Ask fellow student in the cohort in slack
    - Read the course documentation
    - Read official documentation for gem/framework
    - Rephrase the question and google, check StackOverflow
    - Post question on Slack
    - Write a CraftOverflow issue using the template
    - Ask a Coach 

No help if: didn't go throuch support flow, developed solo, if no tests - unless in a spike - branching out and just trying things out. 

ALWAYS HAVE SPECS BEFORE YOU WRITE YOUR IMPLEMENTATION CODE! this is your sellingpoint that we work in a testing development. 

If you've done all the steps, and still stuck, only allow 20 min before you ask a coach. 

Concept questions - try to understand it, then ask. 

---

# Git tips
To change the git origin master URL use the following:

`git remote set-url origin new.git.url/here`

Add `git config core.autocrlf true` to your git to avoid *warning: LF will be replaced by CRLF in lib/atm.rb.* warnings that can occur since I'm using a Mac/unix. 

`git reset --hard HEAD` throws away any uncomitted changes
`git stash` stashes untracked files so that you call git pull from someone else. 
To discard changes in working directory `git checkout <file>`.

To deleted stashed files `git stash drop`

To remove cruft files or clean your working directory run `git clean`. 

To remove all the untracked files in your working directory, run `git clean -f -d`, which removes any files and also any subdirectories that become empty as a result.

`git remote set-url origin URLoforiginrepo`

To check what contributors/origins: `$ git remote -v`

### To create a new branch in Git and pull from your pairprogrammer when using yarn

`$ git branch`shows your branches  
To abort/stop a git merge: `$ git merge --abort` this is preferred over  `$ git reset --hard HEAD`

To add branch:
`$ git checkout -b adding_contacts <this is the name of our branch>`
`$ git remote add clarissa GitHubRepoUrl`
`$ git pull clarissa adding_contacts`   

Go to VSC and click accept incomming or accept other thing if merge is prompted.  
`$ yarn install`  
`§ yarn run cucumber`  
`§ yarn run build`  
All done, now write your code
`$ git push origin adding_contacts`


To check differences between branches:
`$ git diff master..otherBranchName`

---

To install a version of ruby: $rvm install ruby 2.3.1 

---

# GIT PONG 
First opens a repository and commits, second forks that repository, does git clone repo/url and starts coding and commits. The first then:
Head over to your Terminal and add User 2’s GitHub repo as a second remote

$ git remote add (User 2's GitHub name) (the url you copied) For the rest of this walkthrough we’ll assume that User 2’s GitHub name is user_2

Tell git to get the information about User 2’s repository that is stored on GitHub with this command.

$ git fetch user_2

$ git pull beccaburns master

To checkout a previous commit message so you can test things but they won't be saved in master/Head:
$ git checkout idofcommit
To go back to your master branch:
$ git checkout master 

---

# 3/9 Thomas Ochman demo about understanding the problem statement

We need to know what problems we need to solve and why to understand why our program is relevant. 

By working agile and have incemential delivery of working solutions we help the team to step back and identify the true nature of the problem. And the user needs are kept front and center.
http://agilemanifesto.org/principles.html

### The problem statement:
- explicit written statement of the problem, 
- a fundamental step to set the direction of the project,
- working without it leads to waste of time and effort. 
The statements needs to be well scoped, shared and understood by all teammembers. Nees to have a defined current state and desired state, needs to measureable, short and not too complex. 

### User stories:
User stories capture the requirements needed to deliver a soulution to the problem definition. Helps you understand WHAT to do. Has compoments: stakeholder (the problem owner who benefits from having the problem solved), the thing that needs/wants to be done.  
We can extract info from the user stories, like Class names, Method names, objects, states of objects, roles & their authorisations,  etc. 

When naming it needs to be relevant, naming is a process and the chosen names might need to be changed due to irrelevance or becoming illogical. Choose the level of absraction wise 'food, drinks coffe' = product. 
Normalize terminology among team members. 

**Acceptance criteria** (or an agile definition of done) is when we've checked off all the boxes/needs from the user story. 

---

# Day 3:

**Mathlog.10**
Returns the base 10 logarithm of x.
examples: 
Math.log10(100)
Math.log10(1)       #=> 0.0
Math.log10(10)      #=> 1.0
Math.log10(100) #=> 2.0
Math.log10(150) #=> 2.1760...
Math.log10(500) #=> 2.6989...
Math.log10(1000) #=> 3.0
Math.log10(10000) #=> 4.0 

The output is a Float, use .to_i to make it an integer, and add +1 to make it the right number since it starts counting at 0. 

Math.log2(2) => 1.0
Math.log2(4) => 2.0

**.strftime() vs. .strptime() or Time vs Date vs DateTime**

Always use `require 'time' or 'date' or 'DateTime'`
Syntax ex.: strftime '27/04/2018'("%d-%m-%Y")
%Y - year with century, %y - year in 2 digits.

- Strptime is a method in the DateTime class. Like a calendar-based system, can tell you the end of the moenth. .strptime is short for "parse time". It is rarely used since DateTime.parse is usually good at picking up on what's going on
- Strftime is a method in the Time class. Is timezone agnostic, good for measuring elapsed time. strftime is for "formatting time". 
- Date class is a calendar date with no associated times. 

**Magic numbers/ refactoring technique: introduce constant/extract constant/replace magic numbers with symbolic constant**
Magic numbers are hardcoded numbers which can't be changed. To remove a magic number we use constants which are given SCREAMING_SNAKE_CASE names.

```rb example: 
class User < ActiveRecord::Base
  # Constants introduced to replace the
  # magic numbers in allow_to_comment?
  COMMENTER_MINIMUM_AGE_IN_YEARS = 13
  MAXIMUM_COMMENTS_PER_HOUR = 20
```

```rb
  def allow_to_comment?
    age_in_years >= COMMENTER_MINIMUM_AGE_IN_YEARS &&
      comments_in_last_hour.size <= MAXIMUM_COMMENTS_PER_HOUR
  end
end
```

## Demo Learning Strategies with Faraz
### Using flash cards
Good for learning small facts, syndtax, methods, functions. There's apps: brainscape.com, monki. 
- Rehearse on a daily basis. 
- You don't add anything to a flashcard unless you've tried it out. So u get a question, try it out, on the back is the answer.

### Solve daily problems
- start with solving small problems like create a small application for daily-use like grocery or to-do list. 
- or scale it down into an array and push and pop things in/from it.

### Coding diary
- write down the coding-related problems and solutions you found on a day-to-day-basis. 
- simpler in the beginning, more conceptual later. 
- only worthwhile if you do read it often, like 15 min a day like before u go to sleep.

### Feynman technique
*For conseptual things like concepts and components*

- explain a topic in plaing and simple language as if to a child
- go over and find gaps in your understanding or explanation
- repeat
** Write down the concept on the top of a page, then write your explanation step by step. When u hit a issue/gap, go back to your reference material. 

### Teaching others
- explain basics to someone with no knowledge. 
- increases your confidence, helps you to explain things in a way others understand. 
- Huge part of working as a developer. 

### Metaphors
<i>Good for remembering complecated concept. </i>
- a simplified way of explaining a concept, by translating it into a realworld scenario or story. 

### Pre-questioning
Inner dialogue of questioning what's happening each step of the way.
- what will he say next?
- why is he doing that?
- why didn't he do what I though?
- what will he do next?

### Other ways
- Mentorship (copy how another person is doing)
- Rewrite notes after you've written them and make sure you understand.
- Pragmatic reading (only the essentials).
- experimentation/trail and error. 


## How to use the internet to find your answers demo with Faraz Naeem

You can google the errormessages but start with official documentation. 


 Tip: Read the official documentation often & little by little, find a method and read about it.


### For Ruby 
First check offical documentation: rubygems.org, ruby-doc.org

- Rubygems.org
resource for sourcecode and debugging/if code isn't working. 

- Ruby-lang.org

- Ruby-doc.org
 

### For JavaScript
First check: https://developer.mozilla.org

*TO DO: read offical js documentation during weekend: asynchronous js.

npmjs.com
- search here for whatever package you're building. This is official documentation for javascript packages. 

## Other ways
Do copy the entire errormessage. 
(When working with deepwest? etc - do google it.)

- http://stackoverflow.com
  When asking - be very specific. 
  
  Be cautious of the date of the ask, was it active recently?.

  Do read more than the first answers.

- http://github.com/CraftAcademy/CraftOverflow/issues
  practice to write questions here!
  Look through the issues here to find your answer!

- Google for Cheatsheet! 
  Make sure it's still relevant!

- google: what are ?? ELI5 
- google: WTF are ??

---

# Demo about AGILE with Thomas Ochman 10/9
source the http://agilemanifesto.org
Since I've read projectplanning and agile before, my notes here are sparse. 

Kanban boards, LEAN are other methods concerning project-planning. 

## Scrum
timeboxes:
- sprint planning meeting, 8hr max
- sprint commitment meeting, 4 hrs max
- sprint review meeting, 4 hr max
- sprint retrospective meeting, 3 hr max
- Daily Scrum meeting, 15 min max, standing UP!

## Artifacts
- Product Backlog (to-do list for the entire project)
- Spring Backlog (to-do list for this specific sprint)
- Brundown Chart (indicates how much work has been done and is remaining - updates daily)

### Popular choice = Scrump + XP
XP = extreme programming. 
- Behaviour Driven Development
- Test Driven Development
- Pair-programming/collective code ownership
- automated testing
- refactoring
- code review
- continous integration
- continous deployment

 *working software is the primary measure of progress*

---

# weekend challenge week 2: JavaScript FizzBuzz! with Faraz Naeem 13/9
Individual challenge!

Fizzbuzz kata, feature & unit tests, debug and find errors - there are errors in the code. Use the console for this. 
- Find and remove unneccessary code and files!
- Deploy to GitHubPages. 
- Use branches!
- answer the questions in the README!
- Now we create our own repo and create a pullrequest towards our own masterbranch. The link to a pullrequests towards the masterbranch is the submission. Create masterbranch and development branch, from the developmentbranch you merge in all the code. 
- gold star If we can deploy the project without merging to masterbranch. 

---

# demo about debugging with the chrome console, with Faraz Naeem 13/9
Open inspect (through right-click in browser) When u refresh the page it's all gone back to the original code.

- Elements-tab contains all the HTML we can see on the page
  You can choose an element and change the elements html-code, styling
- Console-tab displays alers, messages, console.log(), use it just like irb. 
- sources-tab shows the sources like app.js

To debug: go into inspect, in sources we can add breakpoints (by pressing the line-numbers on the left) to the source-code. This pauses the code next time we run it. 

We can install the extension Debugger for Chrome. It adds the words: debugger; into the code. 

By using pry or debugger-tool I'll learn to understand how data flows. 

Suggests that we have this open continuously and use it whenever we're surprised. 

---

# Codewars pair-programming
work with different ppl each time
take a screenshot of the kata when done.

### IQ-test Ruby:
```ruby
def iq_test(numbers)
 a = numbers.split(' ')
 odds = 0
 evens = 0
 
 a.each do |n|
   if n.to_i.odd? 
   odds += 1
   else
   evens += 1
   end
  end
  
  if odds < evens
    a.each do |n|
      if n.to_i.odd?
      numbeven = a.index(n).to_i
      return numbeven +1
      end
    end
  end
  
  if odds > evens 
    a.each do |n|
      if n.to_i.even?
      numbodd = a.index(n).to_i
      return numbodd +1
      end
     end
    end
end
```

### Format a string o fnames like 'Bart, Lisa & Maggie' 
```ruby
def list names
  if names.empty?
    return ''
  elsif names.length > 1
    names.map! { |n| n.values }
    a = names.pop
      return names.join(', ') + ' & ' + a[0]
  end
    return names[0][:name]
end
```
This is trying to be shorter but doens't remove first name and will add & even if it's only one name
```ruby 
def list names
a = names.map{ |n| n[:name] }
b = a.join(', ')
b + ' & ' + a[0]

end
```

..
---




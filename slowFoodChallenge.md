# Slow Food Challenge intro, 30/9.

Build an online food-ordering system. 
Building a SaaS-application (software as a service).

Using:
Rails, heroku, ruby, semaphore (makes sure everything we merge into our codeplace actually works, for automatic push to heroku). Coveralls(coverage metrics - how many lines of our code are tested), sendGrid(send emails), codacy(makes sure our code-quality is high).

Deployment: Heroku

Challenge time: week 5 + weekend!
Focus on code quality (little repetition, clear syntax, functionality, originality of design).

**ALL code has to have been reviewed by all teammembers before a PR is sent for review.**

Set up continous depoylment today!

## coursedoc.
Focus on getting 1 restaurant to work!

See prepared PT-board with userstories and chores. 
*All the chores should be completed today!*

We also get a boiler-plate/empty application - set up main applicationstructure is already done. 

Using gem **Cartify** - has the payment & add to cart-flow. Need to test it but functionality is provided by set-up! - demo will be released Tuesday. Dont' skip steps!!!

## HAML
another way of writing HTML.
If we have .erb we should use haml instead. 
There are online translators that do this for us - but there are older versions.
=> are old syntax!

HAML is super case-sensitive! Be wary of spaces and intendations - everyone needs the same spaces settings in VSC.

Styling - semantic UI is ok!
If there is a Gem then use the [gem](https://rubygems.org/gems/semantic-rails-ui/versions/1.0.5).
.
---

## Design Sprint
5 phase process that uses design thinking - the main objective is to:
- create a back-log (found in PivotalTracker) of feature requests that are described in a structured way
- to discuss each feature
- assess the complexity of the features so everyone know what to build and how
- define the definition of done
- and assess the complexity of the implementation. 

Purpose is to create user stories to build a MVP (minimum viable product). Always try to have a functioning product at each step. By iteratively add complexity.

### Lo-Fi's
An image you draw on a whiteboard/paper - low-fidelity proptype. 

A quick and tangible representation of a concept. 

Wireframe - a tool to provide a visual understanding of the page - a bit overkill for this week. 

Design Sprint checklist:
- **create lo-fis with the idea and the pages** 
  - do different pages for different type of users (un-autheticated user, authenticated user, admin, restaurant owner etc)
- **check if they meet the reqiurements**
- **create acceptance criteria** (tasks to each user story (max 4-5 tasks per story)
- **create ERD**(entity relatable diagram)(optional for this week)
- **prioritize stories** (ex. does it make sense to add a login at this point?)
- **do a dry-run with the team members** (go thorugh the stories step-by-step -> to make sure that everyone understand what we should do and how the application should be - placements of buttons, navbar, functionality etc)
- **add chores**
- **add a few stories to the backlog and vote on these** then start working on them (voteing is overkill this week)

TO-DO: Go over userstories, create lo-fis, do a dry run, add tasks & lo-fi to userstories. 

By the end of today we should have the application set up & testing framework setup (all chores should be done). Adding features should be done this evening or tomorrow. 

Each story in the PT should have a Lo-fi attached to it - take a picture and add it to the user story. 

#### To the PR:
Add the lo-fi to the PR!!
And add a screenshot of the actual implementation!

#### Agreement within the team:
Intendation with tab and 2 spaces. 

Priorities: 
1. set-up
2. menu-page
3. 

---

## continuous integration (CI)
To make sure everything we add to main codebase is working.

Practices:
- maintain a single source repo (our upstream)
- automate the build
- make the build self-testing
- every commit has to build of an integration machine
- test in a clone of the production environment
- make it easy for anyone to get the laster executable version

## continuous deployment
To make sure everything we add to main codebase it actually gets deployed. 

## Test coverage matrix
check how many % of the code that has been tested.
.
---

# HAML
**filenam.html.haml**
No closing brackets
**%body** <body> how we refrence brackets %
**#wrapper** (div with id="wrapper") how we reference id #
**.stuff** (div with class ="stuff") how we reference class . (multipleclasses can be chained: %div.wrapper.container.row#my-id)
**%a{href: ".."} Top** (<a href="-..">Top </a>)

If you leave out the `%` but this has `#my-id.my-class` haml understands that you mean to but it in a tag.

Nesting is important!
No closing tags so we use intendation
```haml
#my-id
  .container
    .row
      %p Hello World
```
Text can go at the end of the line, but can also be nested. 
Can call html.safe after a textsnippet if we include a html-syntax within text.

Can also input {style:...} for css - bad practice but do-able. 



the VSC extesion "better haml" is good. 


### Tips for product categories
Create category model, create assossiation between product and categry-models
Hints: category has many products 
hints: products belong to one category

# Cartify 
Go to new branch, Write your feature file (given the following producs, and i click on add to cart on pasta.) Add step-definitions, factories. 
- Now add Cartify gem in the top of Gemfile! (as on the off.doc)
- $ bundle install
- $ rails generate cartify.....
- if error - install --sopce assets, routes initializer one by one 
- Now w need to be able to test Java SCript: on top off feature.feature-file ass @javascript at top of page
- Have a look in routes.rb, remove duplicated resources. => [:index, :show]
- Clone necessary migrations $ rails cartify... 
- modify model class User, add piece of code from off.doc (has many...)
- configure cartify initializer: in config: cartify.rb: 
- make sure you have controllers
- add helpers $ rails g controller products... in ApplicationController. 

*now do the testing.*
And I click on string on string |string string2| - change the parameters to element and product_name.
```rb
product = Product.find_by_name(product_name)
within("#product_#(product.id)") do
click_on element
```

- Fix headless in features:support:env.rb: Capybara.register_driver :slemnium do .. remove "headless" from args.

- In view: index.html.haml add a `%table` at the top. add `id= dom_id(product)` withing the %tr. 

- make sure we have link/button `add to cart` - use the Add to cart link helper from off.doc. Within views:index add another `%td add_to_cart(product, 1, 'Add to cart')` for the button/link

- test: and I should see 1 item
- helpermethod Shop icon helper `= shop_icon_quantity` add this to nav-bar

- new scenario step: When I click on "proceed to checkout", `click_on checkout_link` Add the checkout_link to navbar through: `= checkout_link``

*here we will be prompted to log in next*
So we need to have a db-table of following user exist to feature-scenario background. and a user factory.
- add scenario- and i fill in "Enter Email" with "", fill in "password" with ""., and i click on "login"
We can also just use background: and the loggin user is logged in. 

- If issue with filling in the form - look at demo nr 2 at 27:00
change Chromedriver.set_vrsion in features: env maybe?

- `Then I should be on the "addresses" step of the checkout |expected_path| do`, `expect(current_path). to eq cartify.checkout_path(expected_path)`



**To debugg within the cucumbertest**, add scenariostep `Then stop`, inside basic_steps - `Then ("stop") do binding.pry end`if you wanna look at the featuretest and debugg. 

# Weekend challenge
Prepare for monday mornings Sprint Review

- Finish off as much functinality as possible
- Add styling & make it presentable
- Prepare for a demonstration of the app and it's functionality for monday morning (no need to slide-deck)
- deploy your app - maybe.

## Sprint review
- is held at the end of a sprint
 - inspect the increment and adapt the product backlog if needed
- This is an informal meeting, intended to elicit feedback and foster collaboration. 

#### Feeback from sprint review
Lessons: 
- focus on core-fuctionality first and foremost!

- styling - style a little on every PR
Which means we add the styling setup early and as soon as we work with the view, we add a little bit of styling. 

- Make sure we adapt our language for a non-technical person.

- at next review: show the actual application, why certain things are/aren't in place. 

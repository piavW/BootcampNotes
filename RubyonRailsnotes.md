# Notes about Ruby and Ruby on Rails
week 4
---

## demo Web Application Development with Rails, with Faraz Naeem 23/9
Fullstack web application framework, opinionated framework (best practices etc), based on MVC pattern (model - view - contoller), in ruby language. 
It was created to rapidly develop web apps.

*React vs Rails*
- React - library with tools you can use if you want, mainly the view.
- Rails - framework with tools that you need to use, it has the logic, the view etc.

**Core parts of Rails**
- Model - handles business logic/database management - handeled by Active Record & Active Model
- View - what the user sees - handled by the framework Action View
- Controller - where our logic is, what our different parts, buttons etc are doing- handled by framework Action Controller
- Action Pack = Action View + Action Controller
- Action Mailer - framework for sending plain text html och emails
- Action Cable - framework for live updates to pages, push notifications, chatfunctionality
- Active Support - framework for Ruby language extensions

Rails...
- gives your generators
- fixed folder structure
- easy routing (traffic between?)
- database access through Terminal
- manages database tables
- gives you helpermethods
- allows you to use gems (functionalities, rspec)
- makes testing easy
- helpful error messages & recommendations

Downside - not that poppular, complex to handle view compared to React, many ways to do things. 
--- 

**methods are called actions in Rails**

### Folder structure
-App-folder: where we write our main code.
- Controllers - where the logic resides.
- Models - where our businesslogic is, if they want to create articles, blogposts, buy pizzas etc. 
- Views - what ppl see - index.html.erb(embeddedruby) which means we can ass ruby code inside our html. 
- Layouts - basic html structure, <body> and within body-tag `<%=yield%>` (instead of render with divid="root/app"). If you add someting in the body and outside the yield it will be shows throughout the application. 
-db (database) - schema.rb here we can see all our models etc. NEVER TOUCH THIS FILE MANUALLY - this will be generated automaticly once we run our migration.
- features - where we write our features code and step_definitions. 
- spec - where we have our specs for unittests. Uses "shoulda-matchers". 
- Gemfile - rails itself is a ruby gem... 

# Rails and AUT (acceptance unit testing) continuation of demo with Faraz 

## set-up for rails
1. In Terminal in your chosen root folder`$ rails -v` shows verion.

2. on rubygems.org search for rails, we use 5.2.3 because it's more stable/bugfixes etc than 6.0 since 6.0 is so new. 
Copy install command and use it in Terminal`$ gem install rails -v 5.2.3`

3. `$ rails _5.2.3_ new rails_demo --database=postgresql --skip-test --skip-bundle` we specify which version we wanna use, ask to make a new thing, give it a name - use snake_case, or CamelCase, tell it the database, tell it to skip test (minitest), we wanna use Cucumber and RSpec, also skip the default bundling because we wanna add some more gems. 

The command has now created a folder and lots of files within that folder. 

*Commit that we've scaffolded the application*

4. Update README. 

5. Go into Gemfile, clean the GEmfile: remove the comments, delete coffee-rails (we don't use coffeescript since we use vanilla JavaScript). Delete byebug - we use pry instead. Delete tzinfo-data cause we don't use a windows environment.

6. Add our testingframeworks/gems inside the group :development, :test
    - add `gem 'rspec-rails'`
    - add `gem 'shoulda-matchers'` (make rspec expectations simpler to write)
    - add `gem 'factory_bot_rails'` (creates fake objects in ur database - sort of like instance doubles)

*Commit*

7. `$ bundle`
8. `$ bundle exec rails generate rspec:install` We can have generators for almost everything in rails, we need to specify we want to use it inside of rails. Bundle exec means use this version of rspec. In later versions/projects you can skip this. 

*Commit*

9. Clean up in spec: rails_helper.rb delete comments but do read them. 

10. Add code in rails_helper at the bottom: `Shoulda::Matchers...` (look at documentation)

11. `$ bundle exec rspec` to double check everything is ok. 

*commit*

12. Generators generate alot of code, and we need to turn off unneccesary generators in Config: application.rb:
    remove comments, add code-snippet `config.generators...` from documentation

13. run `$ bundle exec rspec` just to make sure all is OK. 

14. In rootfolder: .rspec-file we need to add `--format documentation`

*Commit*

15. `$ rails server` or `$ rails s`starts a server where we can view our code. It's good to check its working. Exit by ctrl + c.

Set-up finished!
---

## installing cucumber

1. Create new branch: `$ git checkout -b cucumber`

2. In codeeditor, Gemfile, under group :development :test, add `gem 'cucumber-rails', require:false` require false turns off errormessages we don't care about. Also add `gem 'database_cleaner` this purges the database from the testing data. 

3. `$ bundle exec rails generate cucumber:install` to install cucumber

4. `$ rails db:create` creates new database

5. `$rails db:migrate` needs to be done for this gem to work

6. `$ bundle exec cucumber` to check that cucumber works

*commit that we've added cucuber, databasecleaner*

7. Merge this branch to the master branch. `$ git checkout master` and then `$ git merge cucumber` - we're supposed to do it through a pull request cause then we get an extra commit and it works with collaboration. Merging through terminal doesn't work when you're collaborating. 

8. When you've developed a feature we run `$ rake` to double check that nothing breaks by running both unittests and featuretests. 

Cucumber set-up done!
---

## creating the application

IF YOU MERGE - REMEBER TO PULL IT DOWN!

 1. create a new .feature-file withing features-folder. Be specific when naming it like "list_articles_on_landing_page.feature"

 2. make sure you have cucumber gherkin installed (extension in VSC)

 3. Write your feature and feature description - as in user stories. 

 4. Write your scenario: When... Then.. And..

 *commit that you've added featurefile*

 5. `$ bundle exec cucumber features/list_articles...` to test it. 
 
 6. Go to basic_steps.rb and add step-difintions: 
    Input your stepdefinitions from the cucmber implementation step definition. If you leave the when block empty you'll have a false positive.

 7. add `visit root_path` in the When I am on the landing page do- block.

 8. Add `expect(page).to have_content content` assertion to the then I should see string..

 *commit*

 9. In routes.rb we set the root-path we've previously added. `root controller: :landing, action: index:`
 And action is like a ruby method! Now landingController is an uninitialized constant. 

10. `$ rails generate controller landing index` we generate a controller, gives it a name, and adds an action. 

A controller is the thing which decides where the data should go. 
Every controller will have a separete folder within views, and it will have a seperate index-file. 

11. run cucumber again and we'll be able to go on the landing page so 1 test green.

*Commit that we've creates new controller and view file*

12. In apps:view:landing: we have a index.html.erb file where we can hardcode things, but it's a false positive since we want to bring the info form our database. 

13. In our feature-file, we can add Background to the feature to populate the test database with information it will cross-check with the frontpage. The info inputted here will only run in the test-environment.

14. when using Background and Given we need to update our step-definitions in **basic_steps.rb**. 

15. since nothing exists in the database, we need to start working with models and unitspecs. 

*commit*
---
## start working with unit specs 

1. inside the spec-folder, create a models-folder. Create a specfile (name_spec.rb). 

2. inside the file, add `require 'rails_helper'` add `RSpec.describe Article, type: :model do end`

3. In terminal `$ bundle exec rspec spec/models/articles_spec.rb` to run/test the article_specfile. 

4. Add the `describe '..' do` `it {is_expeted.to have_db_column :id} end` etc for :title, :content block withing the RSpec.describe

5. Add another `describe 'Validates attributes' do  it {is_expected.to validate_presence_of :title} end` and for :content. Validates make sure we actually have content in what we're adding in, it makes sure we don't create empty rows in our database. 

6. Add another `describe 'Factory' do it 'should have a valid factory' do expect(FactoryBot.create(:article)).to be_valid end end`

We use the {} curlybrackets because 1, it starts a code block where we can write anykind of rubycode in it. 2, the imporation within the {} is added/brought from the shoulda::matchers. 

*commit that we've created spec-file*

7. run `$ rspec`or `$ bundle exec rspec`

8. `$ rails generate model Article title:string content:text` String has ish 140 characters, content is 1000s of characters. 

**Models are always named in singular!**
**Controllers are named in multiples!** And always snake_case!! 

9. don't overwrite the specs your just wrote! 
    If we create the models first and then it will  generate the models spec-file automaticly. 
    It will also create a factory. 

10. `$ rails db:migrate` runs the migration and our schema.rb will now have what we migrated in it. 

**Migration**
Migrations is a way to update the database with the new information. OUr migration files are basic ruby-files. WE create migration-files automaticly, rarely manually. 

*commit creates models and prints article model* We dont' have to specify that we've migrated because that's done on our local computer. 

**!!**If pair-programming we both have to migrate when we pull down someones code. When we pull down we: bundle, and do a migration. To make sure that our database is in the same state as our pairing-programmer. 

11. Add validation to article.rb under class Article `validates :title, presence: true` and `validates :content, presence: true`

*commit that we've added validations*

12. Inside our app:controllers:landing_controller.rb we use the `def index  end`action to do display an instance-variable from the database to the landingpage. 
```rb
def index 
@articles = Articles.all
end
```
Then we add the `@article` to the app:views:landing:index.html.erb 

Whatever is inside the <% %> is ruby code. Because it's embedded ruby. 
When we don't have the = it doesn't print it out to the screen, it only runs it. So = means to run and print it out. 

13. check `$ bundle exec rspec`.

Now we still don't have the content in real life since it's only in the testenvironment
---

1. `$ rails c` takes us to irb
2. Add some real content in irb `$ article = Article.create(title: "Yield is a problem", content: "HAve you looked inside the routes?")` 
3. To see all the arcitles`$ Article.all` to see amount of objects `puts Article.all` 

Now we have the content for real in the database on our localcomputer and it's visible on our localhost.3000-server. 
`$ rails server` or `$ rails -S` to run server. 

### we can make it prettier:
4. in the app:view:landing:index.html.erb
add a h1-tag around the `<h1><%=article.title&></h1>`
add a h4 around the content, a <br> inbetween the two and at the end.

*commit adds iteration of articles on the indexpage*
---

Needs to be done before Tuesday morning (tomorrow), the edit and create functionallity needs to be completed by Friday!


lägg in link to under 5.9 
lägg in till routes.rb resources: articles under 5 getting up and runing. 

### To destroy a model
`$ rails destroy model nameOfModel`

`$ rails db:drop`
.
---

# demo Introduction to Legacy Code Challenge with Faraz Naeem, 24/9
*Working with a new codebase* 

*Legacy code* = source code inhetired from one else &/ inherited from an older version of the software. 

### 7 Different approaches to unravel legacy code:
1. Rubber ducking: explaining the code, out loud to a rubber duck.
    When you have to explain it you'll find flaws, see where the code is breaking and notice the smaller details.

2. Testing the software with Acceptande & Unit Test(AUT-cycle):
    take a feature/functionality, add testing to that functionality.  

3. Following the dataflow: 
    Click around in the application and change small things in the codebase, like variablenames, and then you'll see how the data flows through the application. What methods are hit, what models are used, what gems are used. 
        It's a hard thing to do but good for complex solutions. 

4. History from commitmessages: 
    Go through the commits to look at specific methods, values. 

5. Changing the code: 
    Go in and change bits-and-pieces, add and delete, to understand how it turns out. Good for dealing with lots of styling. 

6.  Debuggers: stop the code execution, change or add a value and see what it does. (Chrome-console, Pry or others)

7. Refactor code: advanced technique. Take a bit of a functionality and refactor the code. Good for dealing with frameworks/languages you already understand. 
.
---

# demo Web architecture with Faraz Naeem 24/9

#### Tier vs Layer
**Layers** describe the logical groupings of functionality and componetns in an application - we decide where we put the code in different places.

**Tiers** describe the physical distribution of the functionality and components on seperate servers, computers, networks etc. - we have to put code in certain places. 

Although both layers and tiers use the same set of names(presentation, logic (business) and data) remember that only tiers imply a real separation.

The 3 tiers:
1. **Presentation tier**
    the user interface, displays info related to services (menu, shoppingcart), communicates with the other tiers from the backend and pushes it forward to the client to collect and display results. 

2. **logical tier** 
    coordinate the application
    processse commands and routes the traffic. 
    makes logical decisions - should be allow this action?
    evalutes and performs calculations
    moves and processes data between the 2 surroundning tiers (presentation & data)

3. **data tier**
    persistence tier, information is stored and retrieved from a database/file system. 

### Life cycle/data flow
see PPdemo.

### MVC (Model - view - controller) architectual pattern
Remind yourself in which part of the application you are working?:
- in the view?
- the controller?
- the model?
- the database? 
Should I be there?
Should I be adding logic here?

## Useful concepts
- **HTTP protocol** (HyperText Transer Protocol) functions as a Request-Response protocol in the client-server computing model.

- **URL** (Uniform Resource Locator is a reference to a web resource that specifies it's on a computer newtork and mechanism for retrieving it. Like an address. 

- **Request Methods:**
    - GET
        asking the server to give your some information

    - POST
        asking the server to save/create something on the server/database.

    - DELETE
        asking the server to delete the information that already exist

    - PUT/PATCH
        asking the server to update some specific information that already exist.

- **Server**
is a computer program or device that proveds funtiocnlity for other programs/devices/clients. 
ex. Application server, mail server, file server, web server. 

.
---

# demo The concept of the params hash, with Faraz Naeem, 25/9

Params Hash (parameter hash, a hash with parameters = {key: value})
It stores informatin passed from the users browser. Gives us the ability to use the users input in our applicaiton so we can create objects, display pages. 

Different types of Params:
- **Query string params**
    as seen in the url, the quesry starts with ?, then we have the key & value (ex. http://google/../../?name=ferret)

- **Route params** 
    links to a specific object (article, product, blogpost etc)
        - uses the id of the specific object
    When u have a number at the end of the url it's a route param.

- **Post params** sends information in order to create an object (article, product, blogpost etc), usually sent through a form. The info is stored in a param-hash. 

Codeing example - see demo. 


.
---
 ## Create Pull Request like a boss:

[EXAMPLE]

[PR-Title] Login Functionality
Link to PT

PR content
In this PR we are adding login functionality with the help of the gem Devise.

This PR contains: 
Configurations for devise
Login Views
Feature tests
A user model
user model specs
What I have learned
How to configure devise
How to create specs
How to add login functionality to our rails application

## Poetry mode
you don't always have to use (), to not use () is called poetry mode, you don't have to use it, but be consistent. 
No need to () on `visit landing_page`, `click_on button`, `click_link string`, `fill_in field, with: string`. 
You can add **optional words** to When cucumber strings, like `When("I click on {string}( button)") do |string|`.
You can also add interchangable words for click/press, like `When("I click/press on {string}( button)") do |string|`.
.
---

# demo introduction to deploy with Heroku with Oliver Ochman 26/9

Heroku - a cloud platform for deployment of applications, in our case. rails applications. 

Official documentation: http://devcenter.heroku.com

- On mac - install it with brew.
- Sign up on Heroku.com

- When installed you'll have the HerokuCLI - so in your Terminal you can write Heroku-commands.

Under "Deploy your application to Heroku" do the commands. 

To create the application on heroku `$ heroku create pia-rails-demo`
To push the application to heroku `$ git remote -v` shows origin and now you have heroku remote added.
`$ git push heroku master`

If you bundle with a version above 2.0 you'll run into problems: solution is a buildpassage for Heroku - message Oliver. 

To migrate our data-base `$ heroku run rails db:migrate` We don't need to create the database on heroku cause heroku does it for us. 

NOw we should have an empty page on our heroku-page. CAuse we need to create articles. 
`$ heroku run rails c`
`Article.create(title: "Hello", content: "how are yu")`

At the moment we need to push it up whenever we do a change - so commit and then push it up to git and then to heroku. 


**Challenge today** - deploy our AUT applications (rails_demo).

ISSUE: I have committed but it doesn't show on Heroku!!!!!!!!!

---


# demo about Validation with Faraz Naeem, 26/9
Validations are a way for us to make sure that the infomation being saved into our database contains the relevant data. 

Also important for ensuring that no malicious data orharmful data is added to our database. 

Why use validation? 
- *safety* less likely to be abused by hackers.
- *performance* need fewer empty rows in our database = more concide = more efficient
- *user experience* we give errormessages to user when they don't pass in the relevant data. 

We prefer to add the validations to the MODEL because:
- closer to the database
- client side validation is not enough (have to use JavaScript to validate on the client-side, it's easy for an outsider to go in to the browser and disable JS)
- controller validations are hard to maintain.

Methods that we can use validations on: create, save update, and create!, save!, update!.

Validation helpers
- Acceptande - validates that a checkbox on the user interface was checked when a form was submitted.
- Inclusion - validates that the attributes' values are included in a given set. 
- Length - validates the length of the attributes' values.
- Presence - validates that hte specified attributes are not empty.
and many more - see rails guides validation. 
---

# Hangout with Oliver 27/9
Usually we branch to development, branch off to rspec set-up, cucumber set-up with it's own pull-request. 

**!!**Always branch off from development

Otherwise you get the commits from the previous branch. 

Branched from wrong branch but ok: Log in, View Trash, forgot password
OK: Sign out, Sign up, 

**!!**When finished a Pull Request - ping coaches for a review in Slack! Write in slack when you've changed a review. 

We work with 3 step_definition-files:
- **basic_steps.rb** for being on landing page, click on |element|, fill in. (we use element since button/link are html elements.)
- **assertion_steps.rb** for assertions - expect something to happen i.e. (expect(page).to ...) Then-blocks and expect..
- **specificTesting_steps.rb** like send messages or mailers only regarding something specific. 

When it's a "then" we expect things to happen, since it's an assertion we use `expect(current_path).to.eq root_path`. 

**!!** Make sure everyone in the group uses the same spaces and tab intendations!

To pull upstream development: add upstream `$ git remote add upstream developmenturl (ex. https://github.com/CraftAcademy/rails_messaging-team2-september-2019.git)` `$ git pull upstream development` 
-
---

# demo Routing with Faraz Naeem, 27/9
Off.doc. http://guides.rubyonrails.org/routing.html

Routing helps us use the HTTP-methods requests: Get (retrieves information from the database), Post, Put (updates the entire app), Patch (updates a specific part), Delete and creates pathways. 

*The Terminalcommand `$ rails routes` shows you all the routes available in your application.*
- *Prefix* -the stuff we add in our code
- *Verb* - what kind of HTTP-action is takes
- *URI Pattern* - what we see in our url/browser
- *Controller#Action* - what controller and action is will hit

`root controller: :posts, action: :index ` is the first page that we come to. Here we specify a controller that we're gonna send the user to posts#index. This saves us from creating a specific controller for root. 

To limit the routes available we specify `resources :articles, only: [:index, :show, :edit]`


### Resouceful routing
CRUD-verbs & actions (CRUD = create, read, update, delete).

By adding `resources :articles` to the config routes.rb-file, we give the articles-controller access to the articles-resources different routes that correspond with the HTTP-methods actions/requests. 

![CRUD-image](crud.png)

Path & URL-helper: use _path 

### Non-resouceful routing
Old way to write routes: 
`get './articles/new, controller: :articles, action: :new'` 
`get './articles/new', to: 'articles/new'`
This isn't used to writing new software like articles anymore. Used with APIs. 

## Namespace
When we have multiple controllers that deal with similar things we wanna **organize** the routes under a specific folder. And group our controller routes.

We put the namespace code inside Routes-file!
```rb
namespace :newOfFolder do 
    resources :resourceControllerName1, :resourceControllerName2
end
```

## Nested routes
Nested routes is when we have a specific sub-model which belongs to a specific controller model. This is about **functionality**.  

ex. a Magazine-model - januaryEdition of that magazine - januaryEditions articles. 
```rb
resources :magazines do
    resources :articles
end
```
.
---

# WeekendChallenge intro 27/9
User Authenticaton with Devise

**Authentication** can be defined as process of verifying someone's identity by pre-required details (commonly username and password).

**devise** is rackbased, a complete MVC solution based on Rails engines, based on modulatiry concept (use only what u really need).

Challenge: 
- read Devise [off.doc](https://github.com/plataformatec/devise)
- Add login functionality to AUT-challenge
- Only allow logged in user to view articles.
    - feature test
    - unit test the user model we will add
- make a [WIP] PR towards ur own development branch
- Submit PR before Monday morning in slack.

Important to `$ rails generate device user` (or modelname u want to have)
add the `before_action : authenticate_user!`

WIP PR towards our own repo
[WIP]Weekend Challenge, devise implementation

Do it like the log in for the group-challenge scenario!
Assertion is that they should be able to see the article. 
And sad paths!

Do not push it up to heroku. 
---

# Rails recap - folder structure, with Faraz Naeem, 1/10

**App** (stores controllers, modells and views)
- assets - holds stylesheets, images, config-folder for javascript, links to directories that we use in our JS code - like a pop-up or specific styling.
- channel (framworks), like application_cabel: channel and connection which control chat-funcionality.
- controller - holds applicationcontroller which takes in funtionality from Actioncontroller. 
Here we add our different controllers.
  - concerns - whenever we extract a function or method or funtioncality from controllers which we use for majority of our controllers, we add then to the concerns folder - our refactored code lives here.  
- helpers - helpermethods
- javascript all our JS 
  - channels
  - packs 
- jobs - a function u run on a regular basis, not triggered by a specific event, on a timer
- mailers - works with Actionmailer, deals with any emails being sent in or out
- models - business logic as Classes
  - concern - deals with refactored code
- views. Partials: Navbar, form, footer is something we add to a partional. A partial is refactored code. 
  - layouts - all of the diofferent views

**Bin** - deals with setup

**Config** - routes etc 
  - environments - development, production and test (from Gemfile) If we want to overwrite something in the testing or production we do it here
  - initializers - contains files that kick in when our server starts. 
  - locales - our translation files (for static things)
  - webpack - used for JS and environments configurations.
  
Config files:
    - Application.rb - where we turn off  the generators. Generators are mechanism for scaffolding code, it creates a lot of files for us. But it also generates stylesheets and other code which we don't need - which is why we turn it off. 
    - cable.yml - where we tell Actionserver it's own server
    - credentials - holds all our credentials ex. encrypted_password, info for your heroku-account. 
    - masterkey - stored locally - never uploaded to git - added to .gitignore, used to access credentials folder and add/remove info from there. 
    - database.yml - config file for databases for different environments
    - puma - our webserver
    - routes.rb 
    - spring - load up the right rubyversion from our computer
    - storage.yml - if we use activestorage and need to configure it.
 
**db** 
- migrate - holds migrationfiles, has files with model-content-table/structure of our database. 
- schema.rb - never touch
- seeds.rb - where we can input our rails console command to create a new model `article = Article.create(title: "..")` and the seeds will do it for us. When pull it down - bundle, rails db:migrate, rails db:seed. You need to run the seed file for it to populate your database with the content in the seeds. 

**lib**
 - assets 
 - tasks

 **log** interesting for debugging - development.log has all the entries we do in our server. 

**node_modules** hold our nodes

**public** static pages that are displayed when server is down

**storage** information about ActiveStorage

**test** is instead of our Spec-folder, rails has a built in test-framework which is why we do skip-test when we build our application - since we use cucumber and RSpec

**tmp** database settings and other temporary files

**vendor** thirdparty static code which can't be added to any other folder (rarely used for us)
.
---

# demo Active Record Basis, with Thomas Ochman, 2/10

For more see [ruby off.doc](https://guides.rubyonrails.org/active_record_querying.html)

the M in MVC (model view controller), is the layer that represents the business data logic.

It's ORM - Object Relational Mapping. 

### Naming conventions 
- database table: plural with snake_case: underscores separating words. e.g. people, order_items, articles
- model class: singluar with the first letter of each word capatalized, PascalCase e.g. Person, OrderItem, Article

### Schema conventions
- Foreign keys: name following the pattern singularized_table_name_id
- Primary keys: Active REcord will use an integer column named id as table primary key
- This column is created automaticly

## Create Active Record Models
`$ rails generate model Article title:string content: text`
```rb
class Article < Application Record
end
```

The **new** method will instantiate the new object, then you set the title and content and then you have to use the .save command to save it to the database
```rb
article = Article.new
article.titile = 'Learning Rails'
puts article.title
```

The **create** method will instantiate the new object and save it to the database, also performs validations.
```rb
article = Article.create(title: "title here", content: "content here")
```

CRUD (Create - Read - Update - Delete) the things you can do to an object in a database. 

#### ACCESS your objects:
```
articles = Article.all
article = Article.first
article = Article.last
article = Article.find_by(title: "title here")
```

When we have stored all articles in "articles" we can actually use it as if it is an array. 
So we can call a specific article from articles by `articles[0]`
or `article.email`    `article[:email]`  `article['email']`
`user.find 1` finds user with id of 1. 

Can also search by `article.find_by_email "email@mail.se"`

`user.where email "email@mail.se"` will always return it as a collection. 


**To update**
```rb
article = Article.find_by(title: "title here")
article.update(title: "new titile", )
```
or you can do the longer verion 
```rb
article1.title = "new title"
article1.save
```
`article1.reload` reloads & displays article1 
If we do `.reload` before we save it, it will not be changed


**To delete**
```rb
article = Article.find_by(title: "title here")
article.destroy
```
To destroy everyting: `Article.destroy_all`


## Migrations
- alter database schema over time 
- use Ruby DSL (domain specific language), no need to write SQL
- schema & changes need to be DB independent
- stored in db/migrate
- migration name: YYYYMMDDHHMMSS_create_articles.rb

**Changing existing migrations** don't do it - write a new migration instead.

See [off. doc](https://edgeguides.rubyonrails.org/active_record_migrations.html)


.
---

# mob-session Advanced Routing, with Oliver Ochman 3/10

To test that we see a string in the right place: Scenario:
`Then I should see "Lasagna" in the "Main" section`
```rb
Then('I should see {string} in the {string} section') do |product, category|
product_category = Category.find_by(name: category)
dom_section = "#category_#(product_category.id)"
within(dom_section) do
expect(page).to have_content product
end
```

Add `@categories = Categories.all` to view. 

Inside the product-list in index.html.haml we add a `.div{id: dom_id(category)}` right after the Categories each do...

Add the Given the following products exist datatable in feature-scenario
Basic step:
```rb
Given("the following products exists") do |table|
  table.hashes.each do |table|
    category = Category.find_or_create_by(title: product[:category])
    table.except!('category') 
    FactoryBot.create( :product, table.merge(category: category))
  end
end
```
We use `table.except!('category')` because the category in the feature-step database table is a string and we want the real thing ge create on `category = Category.find_or_create_by(title: product[:category])`. 
    The factoryBotline tells us to merge the factories-settings for database-table with the given data-base we show in the feature-background. And we want the actual category to create it. 

To create a object models database-table with the associated models(the belongs to model) foreign-key`$ rails g object model Product name:string category:references`

To update a created models: `$ rails g migration AddProductsToCategory` within that def change add: `add_foreign_key :products, :category end`
or within def change`add_reference :products, :category, foreign_key: true`

Don't forget to add `describe 'Associations' do it { is_expected.to have_many :products} end` to the spec-file. 

And to add the `belongs_to` and `have_many` to the view:models being associated. The have_many makes it so that category can create products and call on the association through the category and products, the belongs_to makes it to that product can't be created without a category.

And add `category` to products factory. 
.

Since products belongs to categories we can do `main.products.create(name: "gorbys", description: "..", price: 3)`
.
---

# demo Advanced associations, with Oliver Ochman, 11/10.
Connections between models 

### Belongs_to
Needs to have what it belongs to

### has_one
Doesn't need to have it, but it can have it.

### has_many
zero or one to many connection with another model, often on the other side of a belongs_to association. 

### has_many :through
has many connections through a third model. Like Physician has many patients through appointments. Physician doesn't have_many patients on it's own. An appointment can only exist if there is a patient and a physician. 

### has_and_belongs_to_many
Connection to many models with connection through a third model. Has to have a connection, can't exist without the other ones. 

## Mob-session example of a forum with users and posts:
To generate a Forum model: `$ rails g model Forum name:string`

To generate a user model: `$ rails g model User name:string`

Migrate when you've created a model. `$ rails db:drop db:create db:migrate`

*Business logic:* A forum needs to have many posts, a user also needs to have many posts. So posts needs to belong to user and to forum.

To generate a model Post with association to the models user and forum.
`$ rails g model Post body:string user:references forum:references`
This will have a user foreign key and a forum foreign key. 

Migrate again `$ rails db:migrate`. 

In *rails C* we can check Post.connection (do the same for forum and user). We can see that Post has id, body, user_id, forum_id created_at etc.

Add association of `has_many :posts` to class Forum under App:models. 

Add association of `belongs_to :user` and `belongs_to :forum` to class Post under App:models. 

#### In rails c, 
create `$ user = User.create(name: 'Faraz')`

create `$ forum = Forum.create(name: 'Sports')`

create `$ post_1 = Post.create(user_id: 1, forum: forum, body: 'Some text about sports')`
user can be called with the user-object, or the user_id. Forum can be called with forum-object or forum_id. 

To display the posts that the created forum has`$ forum.posts` gives us an array. 

Can also to `$ user.posts.first`
Can also to `$ user.posts.first.forum.posts.first.user` which is super deep, and is the same as writing `$ user`


To see a error message `$ failed_post.errors` failed_post is the variable to a post we failed to create. 

To see the error message in a test (to display a error message or similar)`$ variableForWhatYou'veCreated.errors.full_messages`

If we're creating a post directly form the forum:
`$ post_2 = forum.posts.create(body: 'second comment', user: user)` then we don't have to add in which forum it's associated with in the (). 

Can also do `$ post_3 = user.posts.create(forum: forum, body: 'third comment!')`

Can do `$ current_user.posts.create(forum: forum. body: 'text')`

**Can't do** `$ post_4 = user.forum.create()` because user and forum has no association to each other.  


#### new example to be able to like a post
Like doesn't have any attributes.
`$ rails g model Like post:references user:references`
    Migrate

*business logic* A user should be able to have many likes on different posts, but should also be able to see how many likes his posts have gotten. 

Add to class Like:
`belongs_to :users`
`belongs_to :posts`
Add to class Post:
`has_many :likes`
Add to class User:
`has_many :likes`


#### In rails C
Change user to faraz. `$ faraz = User.first`

`$ noel = User.create(name: 'Noel')`

Noel is gonna like the second post from Faraz:
`$ noels_like = Like.create(user: noel, post: faraz.posts[1])`

To see noels likes: `$ noel.likes`

`faraz.posts[1].likes` now shows that Farax has 1 like on his second post. 
`faraz.posts.first.likes` shows up empty since no-one has liked that post. 

Add to class User the association has_many:through  
`has_many :post_likes, through: :posts, source: :likes` *post_likes* is a variable and can be named anything. 

To see who liked his first post: 
`$ faraz.post_likes.first.user`


We want to save a recipe, but we want to add notes - then we can have a user model, a recipe model, and a saved recipe model. So we can add stuff to the saved recipe model object and not change the original recipe model object.  


---
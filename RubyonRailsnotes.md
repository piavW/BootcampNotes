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

 9. In routes.rb we set the root-path we've previously added. `root controller: :landing, actoin: index:`
 And action is like a ruby method! Now landingController is an uninitialized constant. 

10. `$ rails generate controller landing index` we generate a controller, gives it a name, and adds an action. 

A controller is the thing which decides where the data should go. 
Every controller will have a separete folder withing views, and it will have a seperate index-file. 

11. run cucumber again and we'll be able to go on the landing page so 1 test green.

*Commit that we've creates new controller and view file*

12. In apps:view:landing: we have a index.html.erb file where we can hardcode things, but it's a false positive since we want to bring the info form our database. 

13. In our feature-file, we can add Background to the feature to populate the test database with information it will cross-check with the frontpage. The info inputted here will only run in the test-environment.

14. when using Background and Given we need to update our step-definitions in basic_steps.rb. 

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
Then we add the @article to the app:views:landing:index.html.erb 
```rb
<% @articles.each do |article| %>
<%= article.title %>
<%= article.content %>
<%end%>
```
Whatever is inside the <% %> is ruby code. Because it's embedded ruby. 
When we don't have the = it doesn't print it out to the screen, it only runs it. So = means to run and print it out. 

13. check `$ bundle exec rspec`.

Now we still don't have the content in real life since it's only in the testenvironment
---

1. `$ rails c` takes us to irb
2. Add some real content in irb `$ article = Article.create(title: "Yield is a problem", content: "HAve you looked inside the routes?")` 
3. To see all the arcitles`$ Article.all` to see amount of objects `puts Article.all` 

Now we have the content for real in the database on our localcomputer and it's visible on our localhost.3000-server. 

### we can make it prettier:
4. in the app:view:landing:index.html.erb
add a h1-tag around the `<h1><%=article.title&></h1>`
add a h4 around the content, a <br> inbetween the two and at the end.

*commit adds iteration of articles on the indexpage*
---

Needs to be done before Tuesday morning (tomorrow), the edit and create functionallity needs to be completed by Friday!






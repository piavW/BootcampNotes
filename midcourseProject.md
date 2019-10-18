# Mid-Course Project Challenge
*Team 1: Alex, Jonas, Yasmine, Becca, Pia.* 

Only have week 6!

Pick an API - build an application around it.

In Rails - an app that consumes an external API
Add authentication and authorization with OAuth  (like fb, google)
Add a payment gateway (like stripe)

## Resources:
We need to have a **restful API** - like sky scanner API, NASA API.

### Do during this weekend:
Come up with an idea, start the design sprint! 

- Think about scope - we only have 1 weeks so don't take on too much. 
- Don't build something trivial but build something managable. 

- Coaches will review our code and merge. **No merging ourselves!**
.
---

# How to get info from an API, with Thomas, 4/10

- Find api on google
- We can use the "rest client" gem (as a way to access exteral resources)

- Install chosen gem to our Rails application & bundle. 

- get the api url

### in rails c: 
`resp = RestClient.get(urllink)`
to access:
`resp.class`
`resp.methods` shows us our methods
`resp.body` shows us the data

It's in a JSON format - as a string formatted in a specific way. 

`JSON.parse(resp.body)` gives us a more readable JSON-object

`joke = JSON.parse(resp.body)`
`joke['value']` displays the value of the joke. 

`joke = JSON.parse(RestClient.get(url).body)['value']` does it in a oneliner

### In application:
add `root controller: :application, action:index` to routes. 

In application_controller (or the controller you wanna display it in)
```rb
def index
@joke = JSON.parse(RestClient.get(url).body)['value']
end

render :whatever 
```
`render :whatever` if you've named the index.html.haml to whatever.html.haml

`render :custom_folder_name/whatever` if the whatever.html.haml is located in the custom_folder_name folder. 

create index.html.haml file and add `%p @joke`


# Idea/design sprint:
[Food API](https://apilist.fun/api/food-api)[Api documentation](https://spoonacular.com/food-api)

Use PivotalTracker and create Lo-Fi's. 
Build it in Ruby on Rails.
- For unit testing: Rspec
- For feature-testing: cucumber, with capybara. 

We need to:
- Authenticate who you are with OA-uth or similar 
- payment option. 

Idea: to provide a way for a user to search for recipiec based on what ingredients you have in your fridge, or based on what ingredients you want to use.  

If you're a premium user, you can save a recipie to your cookbook. 

---

# How to consume an API, with Oliver Ochman, 7/10.
 
Generate controller `$ rails g controller Recipes index`
Add `root controller: :recipes, action: :index` to routes.rb And remove the old (automaticly created) syntax `'get recipes/index'`


Add `gem 'rest-client'`, bundle, 

Can call the rest-client fetch in the controller, but since we want the controller to be clean and readable we can on a module (which has the service) instead. 

So in controller: index:
`response = FoodService.get_cheese` 
(get_cheese is method we're gonna define within a module called FoodAPI)

in App: create services-folder, name it food_service.rb in services file:
```rb
require 'rest-client'
require 'json'

module FoodService
  def self.get_cheese
  response = RestClient.get('url from the api, can change the number in the end')
  recipes = JSON.parse(response)
  recipes['results']
  end
end
```

Services can have other functionality that we don't want to have inside the controller. 

For saving: `DummyVariable = JSON.parse(response)` We have an array and a bunch of objects.

`DummyVariable['recipes']` shows us the array with the recipe, all in a long string. 

`recipes = JSON.parse(response)` takes the stringified answer and makes it more readable
`recipes['recipes']` gives us only the recipes. 

In APP:Views: create folder 'recipes', create file: 'index.hthml.haml'
```rb
%hi Recipes
- @recipes.each do |recipe|
  %h2= recipe['title']
```

### to stub out the result from the API - cause it's bad practice and it can cost money
We use the Gem webmock
We add the `gem 'webmock'` under the development test in Gemfile. Add `require 'webmock/cucumber'` in the support file - i.e. features - support - env.rb. 
Also in env.rb add 
```rb
Before '@get_cheese' do
stub_request(:get, url to api search)
Headers.....#look at documentation
end
```
In the env.rb we need to tell webmock that we allow networkcalls:
`WebMock.allow_net_connect!`

- Add a 'fixtures'-folder, where we add the file api_response_food_get_cheese.txt
- Add the search-resuts into the fixtures file. 
- Within our feature-file, we add @get_cheese on the top so that the feature takes a look at the env.rb file. 

The info in the fixtures is instead of background and factory for the test. 


# demo OAUTH for Facebook, with Oliver Ochman, 9/10.
Using Omni-auth gem: `gem 'omniauth-facebook'` now we have new rails routes!

#### Feature testing: Scenario:
```rb
Given I visit the landing page
When I click on "Login with Facebook"
Then I should be on the home page
And I should see "Successfully authenticated from Facebook account"
```

#### New step-definitions:
```rb
Then("I should be on the home page") do
expect(current_path).to eq root_path
end
```

#### In body:
```rb
link_to 'Login with Facebook', user_facebook_omniauth_authorize_path 
```

#### To App:models: user.rb under Devise add 
`:omniauthable, omniauth_providers : [:facebook]`

Also add:
```rb
def self.new_with_session(params,session)
  super.tap do |user|
    if data= session['devise.facebook_data'] && session['devise.facebook_data']['extra']['raw-info']
    user.email = data['email'] if user.email.blank?
    end
  end
end

def self.from_omniauth(auth)
  where(provider: auth.provider, uid: auth.uid).first_or_create do |user|
  user.email = auth.info.email
  user.password = Devise.friendly_token[0,20]
end
```

#### Routes: under 
```
devise for :users, controllers: {
  omniauth:callbacks: :omniauth_callbacks }
```

#### Controllers
Create the controller: omniauth_callbacks_controller.rb which inherits from `< Devise::OmniauthCallbacksController`. And add the following:
```rb
class OmniauthCallbacksController < Devise::OmniauthCallbacksController

def facebook
@user = User.from_omniauth(request.env['omniauth.auth'])
set_flash_message(:notice, :success, kind: 'Facebook') if is_navigational_format?
else
session['devise.facebook_date'] = request.env['ominauth.auth']
redirect_to new_user_registration_path
end
end
end
``` 

#### In config : initializers : devise.rb
Clean up file from comments, add on top line:
`config.omniauth :facebook` (using the gem we added we tell devise that omniauth has the functionality of adding facebook)
``

## Stub out the login-functionality
Loging into facebook doesn't work in the test environment cause Facebook has restricted the access - which means we need to stub out the request. 

#### In features: support : env.rb
Under Before do 
```rb
OmniAuth.config.test_mode = true
OmniAuth.config.mock_auth[:facebook] = OmniAuth::AuthHash.new(OmniAuthFixtures.facebook_mock)
```
Create a new support file called omni_auth_fixtures.rb
```rb
module OmniAuthFixtures
  def self.facebook_mock
  {
    provider: 'facebook',
    uid: 10205522242159630,
    info: {
      email: '', 
      name: '', 
      image: ''}, 
      credentials:, {
      token: '', 
      expires_at: 1517839337,
      expires: true
      },
      extra: {
        raw_info: {
          name: '', 
          email: '',
          id: ''
        }
      }
    }
  end
end
```

#### Add the provider and uid to user table. 
`$ rails g migration AddOmniauthToUsers provider:string uid:string`
also do a `$ rails db:migrate` to add it to database.


#### Need to have APP-id to pass in everytime we access facebook with our code

Make your facebook a developers facebook. Find your app-id in settings:basic

In Products: facebook Login : settings
we can find "Valid OAuth redirect URIs" 

We want to add it in a masterkey encrypted credentials. `$ EDITOR="code --wait" rails credentials:edit`
within master.key
```
facebook:
  app_id: youridnumber
  app_secret: 'yourappsecretnumber'
```

Add your App-id for facebook to your application: within config:initializers:devise.rb  
```rb
config.omniauth :facebook,
Rails.application.credentials.facebook[:app_id],
Rails.application.credentials.facebook[:app_secret]
```


#### Create a Heroku application to make sure it works
`$ heroku create nameofapplication`
Add the URL to facebooks URIs on the settings-page under Valid OUath Redirect URIs.

Heroku needs to have access to our masterkey:
In Heroku, in the app, under settings, add the masterkey long-line and add it into Config Vars. 

`$ git push heroku oauth:master` so we take our oauth branch and push it into the heroku master branch. And run `$ heroku run rails db:migrate`



---

# demo Form Helpers in Rails, with Faraz Naeem, 9/10
See off. doc. ActionView form helpers on Rubyguides. 

FYI the <input type="submit" value="submit"> is not a button or a link, it's a input type. 

**form_tag** was used when passing in info without a model. *depricated now*

**form_for** was used when creating an instance of a Model. `form_for @user do |form|  form.text_field :email   form.submit` You need to have an underlying model to use this form. *depricated now*

**form_with** combination of form_for and form_tag. Allows us to generate form tags based on urls, scopes and models. It's not bound by Models attributes. 

`form_with url: posts_path do |form|  form.text_field :title  end` will generate 
```html
<form action="/posts" method="post" data-remote="true">
<input type="text" name="post[title]">
</form>
```
With an exisiting model
`form_with model: @post do |form|  form.text_field :title  end`

With new instance of a model
`form_with url: Post.new do |form|  form.text_field :title  end`

Submit button:
`form.submit` will generate <input type="submit" value="submit">

`form.submit value: "My button text"` will generate<input type="submit" value="My Button Text">

All forms generated by form_with will be submitted by an XHR (Ajax) request by default. 
  Now we don't always want to make a Ajax call, then change the local to false. 

### Form controls:
- form.text_area(:comment, :text, size:"20x30")
- form.password_field(login, :pass, size: 20) *will see stars instead of password*
- form.hidden_field(:user, :token)
- form.search_field(:user, :name)
- form.telephone_field(:user, :phone)
- form.date_field(:user, :born_on)
- form.datetime_field(:user, :graduation_day)
- form.month_field(:user, :birthday_month)
- form.week_field
- form.url_field
- form.email
- form.color_field
- form.time_field
- form.number_field
- form.range_field

Options:
:authenticity_token, :url, :local:, :model, :scope, :id etc


---

# demo Stripe, with Thomas Ochman 10/10
Have to do:
- Sign up for Stripe
- Never add your publishable or secret keys online - we will encrypt them!

Uses GEM:
- chromedriver-helper
- selenium-driver (rather use gem 'webdriver' because chromedriver-helper is deprecated)

Add some feature tests to make sure we can access the website: Given I visit homepage, Then I should see "hello". 

`$ rails g controller course index show (specify actions)`

Update routes.rb: `root controller: :courses, action: index, show`

Create index page and add some h1 content.

---
Now that we know the website is accessable - delete the old featurefile. 

### Write a new feature file 
named: visitor can purchase a course.
Add userstory...
```
Background:
Given the following courses exists
  | title       |
  | JS Intro    |
  | React Intro |
Given I visit the application
```
**adding @javascript makes cucumber use selenium driver!!**
```
@javascript 
Scenario:
  Given I click on "Buy" for course "JS Intro"
  Then I should be on a purchase page 
  And I fill in the Stripe field "CC Number" with "4242424242424242"
  And I fill in the Stripe field "Expiry date" with "01/2022"
  And I fill in the Stripe field "CVC" with "123"
  And I submit the Stripe form 
  Then I should see "Thank you!"
```
 ### Update basic_steps
Given I visit the application.. `visit root path`

Given the following courses exists... 
```rb
table.hashes.each do |course_hash| 
 FactoryBot.create(:course, course_hash)
```
```rb
Given I click on {string} for course {string} do |button_text, course_title|
course = Course.find_by_title course_title
within("#course_#{course.id}") do
click_on button_text
end
end
```


In controller add`@courses = Course.all` under index

In index.html.haml:
```haml
- @courses.each do |course| 
  #div
    = course.title
    = link_to "Buy", "#"
```

### Create a Charges controller with 2 actions: new and create 
`$ rails g controller charges new create --skip_routes` To skip the auto-generated routes in routes.rb so we can set them manually. 
  Delete unnecessary: view create, spec charges_controller_spec, spec/views, spec/helper/chegers, app/assets/stylesheets.

Go into config: routes:
`resources :charges, only [:new, create]`

Change in view: index, add new_charge_path(id: course.id) instead of "#" dummypath. 

In controller: charges_controller:
```rb
def new
  @course = Course.find(params:[id])
end
```

In charges: new.html.haml `%h1 Payment form for %= @course.title` 

### Mount the form

step definitions:
```rb
Then("I fill in the Stripe field {string} with {string}") do |input_field, value|
  stripe_frame = find("iframe[name='__privateStripeFrame5']")
  case input_field
  when "CC Number"
    field = 'cardnumber'
  end
  within_frame(stripe_frame) do
    find(field).send_keys(value)
  end
end
```

Inside view: layout: application.html in head div: `%script src="https://js.stripe.com/v3/"`

In our view:charges:new.html.haml
```haml
%form_with url: charges_path, local: true, method: :post, id: :charge_form do
  #card-element

```

Inside the APP: assets: javascript: under the require block
*The turbolinks:load is instead of DOMLoaded*
```js
require("@rails/ujs").start() require("turbolinks").start()

const initiateStripe = (stripeForm) => {
  const stripe = Stripe('public_key')
  const elements = stripe.elements()
  const card = elements.create('card')
  card.mount('#card-element')
}

document.addEventListener('turbolinks:load', () => {
  let stripeForm = document.getElementById('charge_form')
  if (stripeForm) {
    initiateStripe(stripeForm)
  }
})
```
---

## Demo Stripe part 2
Removes chromedriver helper, re-adds webdrivers version 4? Didn't do much but removes deprication warning. 
Set it in env.rb the version depends on ur chrome-version. Also needs to incluce headless because if we run in headless mode then we can find th elements:


CHAGNED step:
```rb
Then("I fill in the Stripe field {string} with {string}") do |input_field, value|
  case input_field
  when "CC Number"
    frame_name = '#card-number div iframe'
    field_name = 'cardnumber'
    when "Expiry date"
  frame_name = '#card-expiry div iframe'
  field_name = 'exp-date'
    when "CVC"
  frame_name = '#card-cvc div iframe'
  field_name = 'cvc'
  end
  stripe_frame= find(frame_name)
  within_frame stripe_frame do
    page.driver.browser.find_element(name: field_name).send_keys(value)
  end
end

Then("I submit the stripe form") do
  click_on 'Submit Payment'
end
```

New/changed code in application.js. We want to send back the (below) created token to the backend and to stripe, so we create a hidden inputfield.
```js
const initiateStripe = (stripeForm) => {
const stripe = Stripe(public_key)
const elements= stripe.elements()
let cardNumber = elements.create('cardNumber')
let cardExpiry = elements.create('cardExpiry')
let cardCVC = elements.create('cardCvc')
cardNumber.mount('#card-number')
cardExpiry.mount('#card-expiry')
cardCVC.mount('#card-cvc')

stripeForm.addEventListener('submit', () => {
  event.preventDefault()
  stripe.createToken(cardNumber, cardExpiry, cardCVC).then((result) => {
    const hiddenField = document.createElement('input')
    hiddenField.setAttribute('type', 'hidden')
    hiddenField.setAttribute('name', 'stripeToken')
    hiddenField.setAttribute('value', result.token.id)
    stripeForm.appendChild(hiddenField)
    stripeForm.submit()
  })
})

}
```

### see printscreens!!!
Add to App: Models: Charges: new.html.haml form_with: 
`form.hidden_field :course_id, value: @course.id`
and add
`form.label :email`
and add
`form.text_field :email` 


Charges_controller.rb
```rb
def create
  course = Course.find params[:course_id]

  customer = Stripe::Customer.create(
    email: current_user.email,
    source: params['stripeToken'],
    description: "#{current_user.email}"
  )

  charge = Stripe::Charge.create(
    customer: customer.id,
    amount: 100 * 100,
    currency: 'sek',
    description: "Purchase of #{course.title}"
  )

  if charge[:paid] == true
    redirect_to root_path, notice: "Thank you"
  else
    redirect_to root_path, notice: "That transaction did not work, please try again."
  end
end
``` 
If it costs 100kr you need to do 100*100 because stripe works in cents/öre. 
We can also do `customer = ... description: "Customers email is #{params[:email]}"`


we want *current_user.toggle.subscription to true???*

Modify feature-step with "And I fill in "Email" with "mail""
Steps: fill_in field, with: value


#### Gemfile: add gem 'stripe-rails'
It's now when we're performing the charge that we want to get the gem. 

bundle the gem
go into your credentials and add stripe api keys:
```yml
stripe:
  publishable_key: pk_test_....
  secret_key: sk_test_....
```

Config: application.rb
```rb
config.stripe.publishable_key = Rails.application.credentials.stripe[:publishable_key]
config.stripe.secret_key = Rails.application.credentials.stripe[:secret_key]
```

## to stub out stripe for testing
add to group development :test `gem 'stripe-ruby-mock'`

In features: support: env.rb we want to create a hook for the scenarios that use stripe
```rb
Before '@stripe_step' do
  chrome_options << 'headless'
  StripeMock.start
end

After '@stripe_step' do
  StripeMock.stop
end
```

#### Mark the stripe scenario with @stripe_step next to @javascript

In Charges controller
remove source, and add `source: get_token(params),`

in the same file but at the bottom add:
```rb
private

def get_token(params)
  Rails.env.test? ? StripeMock.create_test_helper.generate_card_token : params[:stripeToken]
end
```

Can add `Then I wait 2 seconds` to feature-file to make cucumber wait 2 seconds so the mock has time to run. 

Remember that every step we are running that includes stripe needs to be tagged with @javascript and our @stripe_step to be stubbed out. 

---

To myself:
Lägg in Membership belongs_to :user
och User has_one :membership
som booleon true eller false.

READ up on Params!

The Beautify for VSC?
Have a look at indentation and cucumbersteps (when, then, and etc)



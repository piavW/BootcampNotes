# week 7 of Bootcamp @ Craft Academy

# demo Rest on Rails, with Faraz Naeem, 16/10
*Theoretical talk*

REST - Representational state transfer

Uses a request - response architecture (send of a request, get response back) It does not remember what it sent of, or what it recieved cause it has no state. 


### What is STATE:
Application state - should live on the Client, be supplied with each client request. The client is responsible for remembering all the data, not the servers.

Resource State - the state that is passed in needs to be persistent even if client restarts.

**Statelessness** means that the client state shouldn't be stored on server between request. Each request should have no contect of the requests that came before it. 

We want the server to not remember the state of the application. The client therefore has to send all the info the client needs. 

A system is **statefull** if it's designed to remember information that has happended. 

We also use CRUD actions - corresponds to/built upon the HTTP requests: POST, GET, PUT & DELETE. 
The names identify the resources.

### Resource identification
- Each request should uniquely identify a single resource - with all articles or an article. 
- Each request that modifies the database should act on one & only one row of one & only one database table. 
- Requests that only fetch info should get zero or more rows from one table. 

**Representational state transfer** the resource endpoints should return represenations of the resource as data (JSON or XLM format, JSON is the new industry standard). The returned info should be sufficient for the client to uniquely identify & manipulate the database row(s) in question. 

Get XLM or JSON data as a response. 

Convention over configuration - we don't need to think about hard-core routing or configuration since rubyonrails does it for us. 

### Naming conventions
Use nouns, don't use verbs when naming things. 

### Why buildning an API?
We want to use an api because it's the easiest way to connect to another resource and get information from the backend of that resource. 

Why use rails - because it gives us ActiveController etc, pre-existing security, uses the CRUD-actions and good testing for free with RubyonRail. It's also built around being restful. 

- We can also add API functionality to a pre-existing rails application. 
- We can follow best practices with RubyonRails.
- Can use easy versioning of the API. 
  App:Controller:API:V0 and App:Controller:API:V1
    When dealing with an API we don't know how they've built their client, if we update our API and only use one version we'll be breaking the clients functionality if they don't update their client. 
When *creating a new version* we provide new entrypoints for new functionality. 

## Request Specs
Request specs are for APIs what acceptance test are for web application. 
  We make sure we get the expected output from the API. That the information is going out, and going in. 

We use RSpec to do so but rails has a built in frame. We don't use cucumber because adding the middle layer adds unnecessary complexity, using RSpec is also industry standard. 

Always start with request specs first!

---

# Weekend Challenge week 7, intro with Oliver Ochman

TODO:
- add semantic UI React package
  - add some basic styling
- display historic data as a diagram using ChartJS (https://www.chartjs.org/) React-chartsjs-2 package
- answer a question - add to readme: 
  - Where are we doing the claculation? 
  - Where do we check the result of the cooper test? - client or server/api?
  - what are the pros and cons of doing it that way?

the diagrams are components, pass in the data as props to the components. 

Give credit if you borrow/take inspiration from code-solutions. 

Submit repo and (screenshots in the readme) to your deployed app by 9am. (API to heroku, client to netlify)

## demo-ish

All we currently get from the database it average, excellent etc. 

WE need to send in the values of age, distance, gender to the aPI through:

const gender, distance, age = values (see screenshot) of the const saveData = (result, values)
# Notes about React

## demo Getting to know React with Oliver Ochman 16/9

React makes it easier to interact with the DOM without re-rendering the whole application.

React is a JavaScript library (not a framework) for creating user interfaces. React is the view of the MVC (Model view Presenter).

In React you get HTML, CSS and JavaScript all in the same file. There's no separation of concern. 

Raact is declarative, component-based. 
- Declarative vs Imperative: programming paradigms (approaches), you focus on what the component should look like in it's new state, not hot we want to accomplish that result. 

- Component-based - focus on createing small, self-contained componentes that can be strung togehter to build fully-featured user interfaces (UI). There is no massive file where we have everything, instead we have small component which we call upon. 

**Components**: can be made for other smaller components, built-in or custom. 

The **state** drives a one-way reactive data flow, meaning tha tour UI will react to every change of state. 
Components and UIs are simple state machines. 
When you update a component's state React then renders a new UI based on this state. React takes care of updating the DOM for you in the most efficient way. 

Components can also be functions that take parameters and return a result. There are Class components and Functional components. 

in our html: 
`<div id="root"></div> `
everything we build inside the react will be rendered inside the div. 

In our react:
```js
import React, {Component} from "react":
// ...more code here...
ReactDOM.render(
    <HelloWorld />
    document.getElementById("root")
);
```

## JSX Syntax
JSX Syntax adds XML syntax to JavaScript, needs to be processed, usually through Babel.
Curly braces "escape" from JSX into normal JS expressions and JS logic.

We use camelCase. 

Props are values passed from parent to child, they are read-only. The object i savailable as this.prps for class components, and is the only parameter for functional components (then calls upon by props).    Props is a way you can pass in information to other components. 

### component state
For ES6 *class components* intitial statate is defined in the **constructor**.
The state object is avaviable as this.state and can be read from directly.
Stats is updated by calling `this.setState({someField : someValue})`
You should not modify th estate object directly. Every call to `setState()` triggers a re-render. *Remember there is no state in functional components!*

Constructor is sort of like attr_accessor in ruby. 

We need to use a `render() { }` method to be able to use a functional method..? 

## beginners coding in react - creating a helloworld app:
$ npm install npx -g
run that in our rootfolder. 

Add the extension "ES7 react/redux/graphQL/reactnative snippet"to VSC.

NPM is used to install packages. 
NPX makes it so we can run the "create react"-app without having to intsall it on our computer. 
$ npx create-react-app hello_world

Gives us: 
    "Success! Created hello_world at /Users/piavonwachenfelt/bootcamp/thirdWeek/hello_world
    Inside that directory, you can run several commands:

    yarn start
        Starts the development server.

    yarn build
        Bundles the app into static files for production.

    yarn test
        Starts the test runner.

    yarn eject
        Removes this tool and copies build dependencies, configuration files
        and scripts into the app directory. If you do this, you can’t go back!

    We suggest that you begin by typing:

    cd hello_world
    yarn start

    Happy hacking!"

Make sure you .gitignore the node_modules

- delete the app-test
- serviceWorker - don't touch it or remove it. REad about progressive web-applications if you want to know more. 
- we can clean up the files by removing all the elements, css, logo that we don't want from the scaffolded code in app.js index.js etc, remove the folders as well.
- To start the application `$ npm start`

Add the text helloworld to the app.js under funtion app return ()

We can't work with state in a functional component. 

`rce` choose reactComponentExport which scaffolds a react component in your app.js

make sure you have `export default App;` in the bottom of App.js

```js
class App extends Component {
    state = 
        message: 'hello world'
    }
    inputHandler = (event) => {
this.setState({
    message: event.target.value
})
    }
    render() {
        return (
            <>
 <!-- if you have more than one element they all need to be inside a new div/react/JSX fragment because it needs a parent element -->
            <div> {this.state.message} </div>
            <input 
            onChange={this.inputHandler}
            />
 <!--  /> this makes it selfclosing -->
            </>
        );
    }
}
```

`onChange`renders the page with each change.
`onBlur` renders the page when you've changed something and then presses with the mouse somewhere else on the page.


Create a new file called Message.js
```js
import React from 'react';

const Message = (props) => {
    return {
<p>Hello from Message component</p>
    };
}
export default Message;
``` 

in App.js we need to `import Message from './Message'; `
In App.js under render retunr div div this.state.message

```js
<Message 
message={this.state.message}
/>
```

Now we can delete the div this.state.message from App.js since we're gonna get the message from the Message component in the new file. 

We can also do, in the Message.js, 
```js
return (
    <p>{props.message}</p>) 
```

# Prop vs State
Props = properties

The difference is all about which component owns the data. State is owned locally and updated by the component itself. Props are owned by a parent component and are read-only. Props can only be updated if a callback function is passed to the child to trigger an upstream change.

---

# Component lifecycle events
Components can be defined as classes or functions. The methods that you can use on these are called lifecycle events. These methods can be called during the lifecycle of a component, and they allow you to update the UI and application state. Mounting, Updating, and Unmounting are the three phases of the component lifecycle.

### Mounting
Mounting phase is when an instance of a component is being created and inserted into the DOM. Apart from the constructor(), we have access to two lifecycle methods in this phase: componentWillMount, and componentDidMount.

constructor() is the first function called upon instantiating a React class and is where the initial state of the component is being set.

componentWillMount is called only once in the component lifecycle, immediately before the component is rendered (marked for deprecation in future releases of the library, please use componentDidMount below instead).

componentDidMount is also only called once, but immediately after the render() method has taken place. That means that the HTML for the React component has been rendered into the DOM and can be accessed if necessary.

### Updating
Anytime a component is updated or state changes then it is rerendered. These lifecycle events happen during updating in this order.

static getDerivedStateFromProps enables a component to update its internal state as the result of changes in props.
shouldComponentUpdate allows your Component to exit the Update life cycle if there is no reason to apply a new render.
render create elements (generally via JSX) and return them. Unlike any other method in the Life Cycle, render() is the one method that exists across multiple life cycle phases. It occurs in Mount as well as in Update phases.
componentDidUpdate called every time a re-render has been performed, such as when this.setState() is called.

### Unmounting
The unmounting (or deletion, or "cleanup") phase of the life cycle, called when a component is being removed from the DOM. During this phase componentWillUnmount is the only lifecycle event we can call.

---

# demo intro to React 2.0 with Oliver Ochman 18/9
We often use `<button...>` `onBlur={}` `onChange?{}`and `onClick={}`

we use *this.* because it is a class, we don't have access to this in functional components!

serviceworker - progressive webbapplication (like android phones) you can go to an application in the browser an add that to your homescreen and have some offline functionality. - just ignore it cause we won't work with it in the bootcamp.

*.setState* is not super fast, console.log() is faster. In JavaScript the code "runs everything at the same time", but in Ruby it runs "one line at a time" (this is oversimplification). 

**functional component**
We can't define another method inside a functional component. This can only be done in a class. Inside functional components we can declare variables and use if-statements using objects/data specificied in the parent component (the component where the functional component is rendered).

the method `ComponentDidMount(){}`, of all the lifecycle-event, is the most common one. 

Shows us how to do a LogInForm in the demo.

---
# Week 7

---


# demo Outside-in testing, with Thomas Ochman, 14/10
Focused on satisfying the stakeholder/user. 

Outside part covered by acceptance test - sometimes called N2N tests (N2N is ).

Inside part is unit/component test - to make sure that if we for ex. fetch something from an API can we know what the outcome will be.

When testing ask yourself what functionality you'd like to have, what outcome do I want? Try to use the test to drive your development. 


### Delete: 
App.css 
app.test.js 
remove everything in index.css 
remove logo.svg
Rename app.js to app.jsx if we want since it's gonna return something to index.js

### add testing framework
We get JEST directly from out react create scaffold so we don't need to install it. 

`$ yarn add cypress --dev`
`./node_modules/.bin/cypress open` will open & run an installation script
Keep most folders and read through the code to understand it and the testfiles. 
*When you submitt it for code-review make sure those unnecessary files (examples folder) are removed.*

We need the **integration folder** - it's where we place our tests. 

We need to add a scripts under "scripts"`"cy:open": "BROWSER=none yarn start & cypress open"`
to call in Terminal `$ yarn run cy:open`

`killall node` closes everything that runs on localhost:3000

Inside the eslintConfig setting, after extends..., we're gonna add 
```
"globals": {
  "cy": "cy"
}
```
#### VSC extensions
Add the "cypress snippets" extension
Can also add "Cypress Helper" and "Open Cypress" but Thomas isn't using the last 2. 

## first tests
create a new file in cypress/integration. We have our describe section with an it-block.
Every cypress command is pre-fixed with 'cy.'
```js
describe('/index Displays a list of employees', () => {
  it('when user visits the page', () => {
    cy.visit('http://localhost:3000')
    cy.get('h1').should('contain', 'Employee list')
  });
});
```
Can also write the it-block like:
```js
 it('when user visits the page', () => {
    cy.visit('http://localhost:3000')
    cy.get('h1')
      .should('contain', 'Employee list')
  });
```
should's first argument Contain is a matcher, the second argument is a value. 
We can chain matchers:
```js
 it('when user visits the page', () => {
    cy.visit('http://localhost:3000')
    cy.get('h1')
      .should('contain', 'Employee list')
      .should('have.length', 1)
  });
```
Can use another selector instead of `cy.get('h1')` we can use `cy.get('section[name="header"]')`
Then we need to add <section name="header"> <h1>Employee list</h1></section> into the app.js page. 

Can also write
`cy.get('section[name="header"] h1')` to check the section and the h1 within it. 

Within the testing-page we can use the open-selector playground to hover over the page to get ideas. Can also alway inspect to see what things look like.

## to add Enzyme
We want to add enzyme to help our already installed testing framework Jest
`$ yarn add enzyme enzyme-adapter-react-16`

We need to do some configuration for testing:

`touch src/setupTests.js`
In that file we
`import {configure} from 'enzyme'`
`import Adapter from 'enzyme-adapter-react-16'`
Write the command within the file:
`configure({ adapter: new Adapter() })`

Also: create a folder within our src-folder where we will have our component tests
`$ mkdir src/__tests__` this name is dictated by convention
inside __tests__ we want to create a new file called: `EmployeeList.test.js` according to naming conventions. It needs to be the same name as the Component.
Within this file we need to import react, import 2 components from enzyme and import our component.
```js
import React from 'react'
import { mount, shallow } from 'enzyme'
import EmployeeList from '../components/EmployeeList'

describe('<EmployeeList />', () => {
  it('renders <ul> with 5 <li>', () => {
    const describedComponent = shallow(<EmployeeList />)
    expect(describedComponent.find('ul')).toHaveLength(1)
     expect(describedComponent.find('li')).toHaveLength(5)
  });
});
```
**Shallow** takes a react component into memory and renders it into test. 
**Mount** it the same thing, but it takes any component this component has as children. 

It is bad practice to have 2 expect-statements in the same it-block.
Could be written as:
```js
describe('<EmployeeList />', () => {
  
  let describedComponent //can not use a const cause then the beforeEach doesn't work

  beforeEach (() => {
     describedComponent = shallow(<EmployeeList />)
    });

  it('renders <ul>', () => {
    expect(describedComponent.find('ul')).toHaveLength(1)
  });

  it('renders 5 <li>', () => {
     expect(describedComponent.find('li')).toHaveLength(5)
  });
});
```

**To skip an it-block: but a `x` in front of the it: like `xit(...)`**

**You can also use `test(...)` instead of `it(...)`**


## Create the actual Component
create a file `EmployeeList.jsx` (PascalCase) Thomas uses jsx because they are supposed to ??

Within our `EmployeeList.jsx` We do:
```js
import React from 'react'

class EmployeeList extends Component {
  render() {
    return (
      <> //this is a fragment
      <ul>
        <li> </li>
        <li> </li>
        <li> </li>
        <li> </li>
        <li> </li>
      </ul>
      </>
    )
  }
}
export default EmployeeList;
```

## To fetch from an API
the **Axios library** is often used to Fetch and Post external data to API's. 

We can write a test to make sure Axios is actually used in our set-up. 

Wihtin the `__test__` in the `EmployeeList.test.js` file
We want to spy on the axios get-requests (axios's get-module) and make sure it was actually called at least once.
```js
import axios from 'axios'
it('should use Axios to featch data', () => {
  const axiosSpy = jest.spyOn(axios, 'get')
  mount(<EmployeeList />)
  expect(axiosSpy).toBeCalled()
});
```

In our EmployeeList component we change and add: We use a dummy-data-API for demo-purposes: http://reqres.in

The response is the full everything, the body in axios is called data, and we want the specific data within that?
```js
import React from 'react'
import axios from 'axios'
class EmployeeList extends Component {
  state = {
    employees: []
  }
  componentDidMount() {
    axios.get('https://reqres.in/api/users?per_page=5').then(response => {
      // console.log(response.data.data)
      this.setState({ employees: response.data.data })
    })
  }
  render() {
    return (
      <> 
        <ul>
        </ul>
      </>
    )
  }
}
export default EmployeeList;
```

To make sure our component does mount:
In test.js
```js
it('should have a list of employees as state after mount', () => {
  let list = mount(<EmployeeList />)
  console.log(list.state)
});
```
---

#### RETRY:

```js
import React from 'react'
import axios from 'axios'
class EmployeeList extends Component {
  state = {
    employees: []
  }
  componentDidMount() {
    axios.get('https://reqres.in/api/users?per_page=5').then(response => {
      // console.log(response.data.data)
      this.setState({ employees: response.data.data })
    })
  }
  render() {
    let employeeListDisplay = this.state.employees.map(employee => {
      return (
        <li key={employee.id}>
        {`${employee.first_name} ${employee.last_name}`}
        </li>
      )
    })
    return (
      <> 
        <ul>
        {employeeListDisplay}
        </ul>
      </>
    )
  }
}
export default EmployeeList;
```


`wrapper`is the same as `describedComponent`


## update feature test:
In our integration folder: `displayEmployeeList.js`file
```js
describe('<index Displays a list of employees />', () => {
  
  before(() => {
     cy.visit('http://localhost...')
    });

  it('when user visits the apge', () => {
    cy.get('section[name="main" div h1'])
    .should('containt', 'Employee list')
  });
    it('shows 5 list items with employee data', () => {
    cy.get('li'])
    .first().should('contain', 'George Bluth')
    .next().should('contain', 'Janet Weaver')
    .next().should('contain', 'First Last')
    .next().should('contain', 'First Last')
    .next().should('contain', 'First Last')
  });
});
```

To stub it out:
```js
describe('<index Displays a list of employees />', () => {
  
  before(() => {
     cy.server()
     cy.route({
       url: 'http://',
       method: 'GET',
       response: 'fixture:mockedResponse.json'
     })
     cy.visit('http://localhost')
    });

  it('when user visits the page', () => {
    cy.get('section[name="main" div h1'])
    .should('containt', 'Employee list')
  });
    it('shows 5 list items with employee data', () => {
    cy.get('li'])
    .first().should('contain', 'George Bluth')
    .next().should('contain', 'Janet Weaver')
    .next().should('contain', 'First Last')
    .next().should('contain', 'First Last')
    .next().should('contain', 'First Last')
  });
});
```

Create the folder: `fixtures` and the file: `mockedResponse.json`  and Add the response you want into that file. 


### Add some styling with Semantic UI
can add it using `$ yarn add semantic-ui-react semantic-ui-css`
In the index.js `import ''semantic-ui-css/semantic-ui-min`

In app.jsx add `import { Container } from 'semantic-ui-react'`
 add <Container /> within the page under EmployeeList. 

Within EmployeeList.jsx
`import { List, Image } from 'semantic-ui-react'` Add some semantic ui components - see screenshot 16:09.

When we use our tests: `$ yarn run test` we have now changed our list usin componentbased lines for styling, and <li> etc won't work for our tests. 
Use inspect to checkout the html. You'll se it's a div with a role of list. and 5 divs with the role of listitem. <div role="list">
So in our test we're gonna specify `expect(describedComponent.find('div[role="list"]')).toHaveLength(1)`

When using **shallow** in beforeEach on <EmployeeList/> it doesn't work, when we use **mount** it works. This is because shallow only renders the component itself, whilst mount renders the component and it's children component. 


---
# Styling with Semantic UI in React, 15/10, with Thomas Ochman.

[Semantic UI React](https://react.semantic-ui.com/), there is a wrapper made for React!
Adds semantic-ui-react and semantic-ui-css because we need to import the packages globally `import "semantic-ui-css/semantic.min.css";`- normally the index.js file. 

If you want to use certain components we need to import them as modules `import { Container, Form, Grid }'semantic-ui-react';`

### Create a navbar
Create a new component file. 

Add the `<Navbar />` to your App.js page on the top of the fragment under return. 

Within the component file:
```js
import react from 'react';
import { Container, Menu } from 'semantic-ui-react';
import './Navbar.css'
class Navbar extends COmponent {
  render() {
    return(
      <>
        <div className="ui stackable menu"> // Can also write it `<Menu stackable>` or `<Menu stackable className="logo">` to change it using regular css as well.
          <Container>
            <Menu.Item>
              BMI Calculator
            </Menu.Item>
          </Container>
        </div>
      </>
    )
  }
}
export default Navbar 
```

Create a file NavBar.css in components add:
```css
@import url(http://)
.logo {
  font-size: 20px !important;
  font-weight: bolder !important;
  font-family: "sans-serif";
}

.menu {
  border-radius: 0 !important;
}
```
--- 


## Props from Semantic UI
This is all done in the App.js file

```js
<Header>
as="h1"
textAlign="center"
</Header>
```
as and textAlign are props!
On the website we can see more props we can use. 

If we change the state of textAlign
and add a state called `alignment` under constructor(props). And the initial state is: `alignment: 'center'`

```js
<Header>
as="h1"
textAlign={this.state.alignment}
</Header>
```

Under DisplayResult add:
```js
<div>
<button onClick={this.changeAlignment}>left</button>
<button onClick={this.changeAlignment}>right</button>
<button onClick={this.changeAlignment}>center</button>
</div>
```

create new function, the (e) is for event. Here we change the alignment to whatever the buttons text is.
```js
changeAlignment = (e) => {
  this.setState({
    alignment: e.target.innerText
  })
}
```
**event.target** is always the element the event came from/triggered it. 

instead of innertext we can also do `e.target.name/id` or similiar. Just check with debugger what you have access to when you type `event.target`.

### CSS tips & tricks
**"!important"** overrides and forces the change. Generally speaking important is bad practice but OK when using semantic UI.
 
**border-radius** gives us rounded corners. 

---


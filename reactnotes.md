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


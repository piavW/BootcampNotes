# Livia More, head of marketing and PR at Antler.
Antler = global startup generator - help u get the money for ur company.
You join as an individual, don't have to habe an idea or team.  The program is 6 months, after 10 week meeting with investment committe - go forward or go home. 


# Getting to know React hands on, with Thomas Ochman, 10/9 at Antler!
React = a javascript **library** for creating user interfaces. 
MVC - model view control, react deals with the view. 

React is a javascript-based library - everything we can do in javascript, we can do in react. 
Declarative vs imperative - see codeburt.io comment on this. In reatsfocus on what the component should ook like in it's new state, not how it's supposed to work. 
Component-based to build fully freatured userinterfaces (UI), reuseablility.

Learning curve: 
- learning reats basic conepcts and API : easy
- learning to think in react : intermediate
- all the stuff you can do with react: advanced. 

React are builds aroud 2 components/principles: componentes and states. 
components can be made of other smaller components, build-in or custom. 
React takes care of updating the DOM for you when u update the components. 

YOU need to have <div id="idName" ></div> in a html.index page to be able to connect the html-file and the react application!
In react: `ReactDOM.render( document.getElementtById("idName") )`
JSX syntax preprocessor step taht adds XML syntax to Javascript. You can use it without JSX but it makes it a lot more elegant. However JSX needs to be compiled into javascript, like through Babel.

Use camelCase when u create a component, PascalCase when u declare variables! *It's very case sensitive*
Anything can be passed as a prop. 

State is updated by calling `this.setState({someField : someValue})` You should not modify the stateobject directly. 

Separation of concern - in react you mix presentation and logic in the same file. 

### The difference between state and props:
The difference is all about which component owns the data. State is owned locally and updated by the component itself. Props are owned by a parent component and are read-only. Props can only be updated if a callback function is passed to the child to trigger an upstream change.


According do Jelica Ristic - met her here -  Materialize CSS and Bootstrap are good CSS framworks with react, preferably materialize. 






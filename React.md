# Learning React

## ES6 Syntax and Feature Overview
Legend:
Variable: `x`
Object: `obj`
Array: `arr`
Function: `func`
Parameter, method: `a, b, c`
String: `str`

`var`: (can be reassigned and redeclared)(only available inside function)(defined throughout the program)
- type of scope: function
- hoisting: yes
- can be reassigned: yes
- can be redeclared: yes

`let`: (scoped to the block which is a set of opening/closing brackets)(has deadzones)
- type of scope: block
- hoisting: no
- can be reassigned: yes
- can be redeclared: no

`const`:
- type of scope: block
- hoisting: no
- can be reassigned: no
- can be redeclared: no

- arrow functions(shorter code of function)
- template literals, span multiple lines without concatenation

- array iteration:
```js
for (let i of arr) {
    console.log(i)
}
```

## Intro to React / JSX
React is a Javascript library!
* JSX is a syntax extension to JS, using it with React allows it to describe what the UI should look like, similar to a *template language* but uses power of JS
```js
const element = <h1> Hello, world! </h1>;
```
- React separates *concerns* with units called **components** that contain both, React does not require JSX but it is helpful as a visual aid and shows more cases of errors and warnings

- integrating expressions in JSX
```js
const name = 'brendan';
const element = <h1> Hello, {name} </h1>;

ReactDOM.render(
    element,
    document.getElementById('root')
);
```
- here we used the variable name and then used it in JSX by wrapping in curly braces
- here is a more intense example... from reactjs.org
```js
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
- you can use JSX as an expression in functions for evaluating JS objects

### Children w JSX
- similar to HTML JSX can contain children like w an `h1` inside a `div`

- Use `React.createElement()` for creating an object
```js
const element = React.createElement(
    'h1',
    {className: 'greeting'},
    'Hello, world!'
);
```

## Rendering Elements
- elements describe what you want to see on the screen

1. rendering an element into the DOM
`<div id='root'></div>`
- we call this a root DOM node because everything inside will be managed by React DOM
- if you want to render a React element into a root DOM node, pass both to `ReactDOM.render()`
```js
const element = <h1> Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```
## Updating the Rendered Element
- react elements are **immutable**, once it is created you *cannot* change its children or attributes, think of a frame in a movie where it represents the UI at a certain point in time
- in practice, most React apps only call `ReactDOM.render()` once
- React only updates what is necessary

## Components and Props
- components let you split UI into *independent, reusable pieces*
    - conceptually, components are like JS functions, and accepts *inputs called props*

- the simplest way to write a component is to write a JS function
```js
function Welcome(props) {
    return <h1> Hello, {props.name} </h1>;
}
```
- can also use `class` to define a component
### Rendering
- elements can also represent user-defined components:
```js
const element = <Welcome name="Sara" />;
```

- this example renders "Hello, Sara" onto the page!
```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
1. We call ReactDOM.render() with the <Welcome name="Sara" /> element.
2. React calls the Welcome component with {name: 'Sara'} as the props.
3. Our Welcome component returns a <h1>Hello, Sara</h1> element as the result.
4. React DOM efficiently updates the DOM to match <h1>Hello, Sara</h1>.

## Composing Components
- components can **refer** to other *components* in their output whether it is for a button, form, a dialog, etc.

- example of an *App* component that renders *Welcome*
```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```
## Extracting Components
- do not be afraid to split components into smaller components and then inserting back into main component
- props are read-only

## State and Lifecycle
- state is similar to props, but is private and fully controlled by the component

### Converting a Function to a Class
1. Create an ES6 class, with the same name, that extends the `React.Component`
2. Add a single empty method to call it `render()`
3. Move the body of the function into the `render()` method
4. Replace `props` with `this.props` in the `render()` body
5. Delete the remaining empty function declaration

```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
- `Clock` is now defined as a class rather than a function
- the `render` method will now be called each time an update happens, so as long as we render `<Clock />` into the same DOM node, only a single instance of the `Clock` class will be used

**Adding a Local State to the Class**
- we will move `date` from props to state in three steps
1. Replace `this.props.date` with `this.state.date` in `render()` method
```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
2. Add a class constructor that assigns the initial `this.state`
```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
- class components should always call the base constructor with `props`
3. Remove the `date` prop from the `<Clock />` element
```js
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
- result:
```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
**Adding Lifecycle Methods to a Class**
- in apps with many components, it is important to free up resources taken by components when destroyed
- example with mounting and unmounting the timer for the clock!
```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
- recap from example from reactjs.org
1. When `<Clock />` is passed to ReactDOM.render(), React calls the constructor of the Clock component. Since Clock needs to display the current time, it initializes this.state with an object including the current time. We will later update this state.
2. React then calls the Clock component’s render() method. This is how React learns what should be displayed on the screen. React then updates the DOM to match the Clock’s render output.
3. When the Clock output is inserted in the DOM, React calls the componentDidMount() lifecycle method. Inside it, the Clock component asks the browser to set up a timer to call the component’s tick() method once a second.
4. Every second the browser calls the tick() method. Inside it, the Clock component schedules a UI update by calling setState() with an object containing the current time. Thanks to the setState() call, React knows the state has changed, and calls the render() method again to learn what should be on the screen. This time, this.state.date in the render() method will be different, and so the render output will include the updated time. React updates the DOM accordingly.
5. If the Clock component is ever removed from the DOM, React calls the componentWillUnmount() lifecycle method so the timer is stopped.

### Using State Correctly
- what to know about using `setState()`
1. Do not modify state directly
- // Wrong
    - this.state.comment = 'Hello';

- Instead, use setState():

- // Correct
    - this.setState({comment: 'Hello'});
2. State updates may be asynchronous
    - React may batch multiple `setState()` calls into a single update

- wrong
```js
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```
- right
```js
// Correct
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```
3. State updates are merged
- when you call `setState()`, React merges the object you provide into the current state

## Handling Events
- React events are named using camelCase rather than lowercase
- with JSX you pass a function as event handler rather than a string
```js
<button onClick={activateStuff}>
  Activate Stuff
</button>
```
- you also cannot return `false` to prevent behavior, you must call `preventDefault`
```js
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```
- you usually do not need to call `addEventListener` to add listeners to a DOM element after it is created, instead just provide a listener when *the element is initially rendered*
- a common usage for an event handler is for it to be a method on the class... Such as having a `Toggle` component that renders a button that lets user switch from ON and OFF
```js
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```
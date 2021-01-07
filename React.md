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

## Conditional Rendering
- you can create distinct components that hold certain behaviors where you can *render* only **some** of them depending on state of application
- use `if` or `conditional operator` to create elements representing current state, and then let React update UI to match
```js
function UserGreeting(props){
  return <h1> Welcome back User! </h1>;
}

function GuestGreeting(props){
  return <h1> Sign up! </h1>;
}
```
- now we separate to render based on behavior
```js
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```
### Element Variables
- use variables to store elements to conditionally render a part of the component
```js
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;
    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);
```
### Inline Operators
- `&&` evaluates the left side first, if left side is true then right side will be executed
- if-else is `?` which is `true : false`
- in some cases you want a component **NOT** to render, to do this return **null** instead of its render output

## Lists and Keys
- you can build collections of elements and include them in JSX by using `{}`
```js
const nums = [1, 2, 3, 4, 5];
const listNums = nums.map((nums) =>
<li>{nums}</li>
)
ReactDOM.render(
  <ul>{listNums}</ul>,
  document.getElementById('root')
);
```
### Basic List Component
- usually you want to render lists inside a component
- example from reactjs.org
```js
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
    {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```
- you need a `key` to include when creating lists of elements
### Keys
- keys help React identify which items changed, added, or removed
- keys should be given to elements inside array to give them a *stable* identity
  - use a string that uniquely identifies a list item among its siblings... Most often you would use IDs from your *data as keys*
```js
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```
- when you do not have stable IDs for rendered items, you may use `index` as a key as last resort

```js
<li key={index}>
  {todo.text}
</li>
);
```
### Extracting Components w Keys
- rule of thumb: elements inside the `map()` call need keys
- keys do not need to be globally unique, but must be among their siblings

## Forms
```js
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
- use setState for the value to change whenever the value is updated

- the `<textarea>` element defines its text by its children
```js
class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 'Please write an essay about your favorite DOM element.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('An essay was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Essay:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
- the `this.state.value` is initialized in the constructor so that the text area starts off w some text in it
- the `<select>` creates a drop-down list with using `<option>` and `value`
```js
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Your favorite flavor is: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Pick your favorite flavor:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">Grapefruit</option>
            <option value="lime">Lime</option>
            <option value="coconut">Coconut</option>
            <option value="mango">Mango</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
- the `<input type="file">` lets user choose one or more files from their device storage to be uploaded to a server

## Lifting State Up
```js
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    return (
      <fieldset>
        <legend>Enter temperature in Celsius:</legend>
        <input
          value={temperature}
          onChange={this.handleChange} />
        <BoilingVerdict
          celsius={parseFloat(temperature)} />
      </fieldset>
    );
  }
}
```
- an input is rendered that lets you enter the temperature and keeps value in this.state.temperature

- two inputs
```js
const scaleNames = {
  c: 'Celsius',
  f: 'Fahrenheit'
};

class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    const scale = this.props.scale;
    return (
      <fieldset>
        <legend>Enter temperature in {scaleNames[scale]}:</legend>
        <input value={temperature}
               onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```
## Composition vs Inheritance
### Containment
- some components do not know their children ahead of time
- such components should use the special `children` prop to pass children elements directly into their output
```js
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```
- anything inside fancyBorder gets passed into the component as a `children` prop
- specialization = adding a more specific component that builds off a generic one (WelcomeDialog vs. Dialog)

## Thinking in React
1. break down the UI into a component hierarchy
  - draw boxes around every component and subcomponent in mock and give them all names
  - use single responsibility principle, a component should ideally do one thing
2. build a static version in React
  - build components that reuses other components and pass data using *props*, as they are a way of passing data from parent to child
  - *state* is reserved for interactivity, that is data changes over time
  - there are two types of model data in React: *props* and *state*
3. identify minimal (but complete) representation of UI state
  - to make UI more interactive, you need to trigger changes to underlying data model as this is achieved with *state*
  - try not to Repeat Yourself!
4. Identify where your state shoud live
  - React is a one-way data flow down component hierarchy
  - for each piece of state in your application:
    - Identify every component that renders something based on that state.
    - Find a common owner component (a single component above all the components that need the state in the hierarchy).
    - Either the common owner or another component higher up in the hierarchy should own the state.
    - If you can’t find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common owner component.
5. add inverse data flow


# Next.js
- it is the React framework
## Creating a Next.js app
1. open terminal and `cd` into a directory and run `npx create-next-app nextjs-blog --use-npm --example "https://github.com/vercel/next-learn-starter/tree/master/learn-starter"`
- this is for the starter blog app
2. we now have a directory called `nextjs-blog`, now `cd` into it
3. run `npm run dev`
- this starts the development server on port 3000

- editing the page...
4. make sure the Next.js development server is still running
5. open `pages/index.js` with text editor
6. change something and check the browser!

- adding more pages...
  - pages are associated with their / route after pages
7. create a new page by creating a `posts` directory under `pages`
8. create a file called `first-post-js` inside `posts` directory with this...
```js
export default function FirstPost(){
  return <h1> First Post </h1>
}
```
- pages/posts/first-post-js
  - /posts/first-post is the route
9. Linking components
- link between pages using the `Link` Component from `next/link` to wrap the `<a>` tag
- `<link>` allows you to do client-side navigation to a different page in the application

10. open `pages/index.js` and import the `Link` component by adding `import Link from 'next/link'`
```js
<h1 className="title">
  Read{' '}
  <Link href="/posts/first-post">
    <a>this page!</a>
  </Link>
</h1>
```
- client-side navigation
- the `link` component enables client-side navigation between two pages in the same Next.js app

## Assets, MetaData, and CSS
- Next.js servers static files, like images, under the *top-level* `public` directory... Files inside the `public` can be referenced from the root of the app
```js
<Head>
  <title>Create Next App</title>
  <link rel="icon" href="/favicon.ico" />
</Head>
```
- notice that `<Head>` is capitalized bc it is a React component
- if you want to add make sure to import
  - `import Head from 'next/head'`
```js
export default function FirstPost() {
  return (
    <>
      <Head>
        <title>First Post</title>
      </Head>
      <h1>First Post</h1>
      <h2>
        <Link href="/">
          <a>Back to home</a>
        </Link>
      </h2>
    </>
  )
}
```
```js
<style jsx>{`
  …
`}</style>
```
- this is the css incorporated within React component
- you can import `.css` and `.scss` files

## Creating a layout component
- create a top-level *directory* called `components`
- inside `components`, create a file called `layout.js` with...
```js
export default function Layout({children }) {
  return <div>{children}</div>
}
```
- then open `pages/posts/first-post.js` and add an import for the `Layout` component and make it the outermost component
```js
import Head from 'next/head'
import Link from 'next/link'
import Layout from '../../components/layout'

export default function FirstPost() {
  return (
    <Layout>
      <Head>
        <title>First Post</title>
      </Head>
      <h1>First Post</h1>
      <h2>
        <Link href="/">
          <a>Back to home</a>
        </Link>
      </h2>
    </Layout>
  )
}
```
## adding CSS
- go to `Layout` component
- create a file called `components/layout.module.css`
```js
.container {
  max-width: 36rem;
  padding: 0 1rem;
  margin: 3rem auto 6rem;
}
```
- to use this `container` class inside `components/layout.js` you need to...
  - import css file and assign name to it like `styles`
  - use `styles.container` as the `className`
- open `components/layout.js`
```js
import styles from './layout.module.css'

export default function Layout({ children }) {
  return <div className={styles.container}>{children}</div>
}
```
## global styles
- to have styling for every page...
  - create a file called `pages/_app.js` and add...
```js
export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```
- you need to restart development server by ctrl + c and then do `npm run dev`

## Pre-Rendering and Data Fetching
- next.js pre-renders every page in advance which results in better performance and SEO
  - check that it is happening by disables JS in browser and try accessing page

**Forms of Pre-Rendering**
1. *Static Generation*
- pre-rendering method that generates the HTML at **build time**. The pre-rendered HTML is then *reused* on each request
2. *Server-Side Rendering*
- is the pre-rendering method that generates the HTML on *each request*

**When To Use**
1. *Static Generation* should be whenever used possible, but ask yourself "Can I pre-render this page **ahead** of a user's request?
  - *Static Generation* is not a good idea if you cannot pre-render a page ahead of a request
2. *Server-Side Rendering* will be slower, but will always be up-to-date

### Static Generation
- can be done with or without data
- however, some pages may not be able to render HTML without first fetching some external data
  - may have to access file system, external API, or query your database at build-time

- when you export a page component, you can also export a `async` function called `getStaticProps`
  1. `getStaticProps` runs at build time in production
  2. Inside the function, you can fetch external data and send as props to the page
  - basically, you are telling Next.js "this page has some data dependencies, so when you pre-render this page at build-time make sure to resolve them first"
    ### Implementing Static Props by Parsing
    - `npm install gray-matter`
    - this helps us parse metadata in md file
```js
export async function getSortedPostsData() {
  // Instead of the file system,
  // fetch post data from an external API endpoint
  const res = await fetch('..')
  return res.json()
}
```
- in development, `npm run dev` `getStaticProps` runs on every request
- in production, `getStaticProps` runs at build time

### Fetching Data at Request Time (Server-Side Rendering)
- to use server-side rendering you need to export `getServerSideProps` instead of `getStaticProps` from your page

## Dynamic Routing
- when you want the URL for pages to depend on data such as for a blog
- page path depends on external data

- when we want a post for a blog use a path such as `/posts/<id>` where `id` is the name of a key or file, etc.
- create a page called `[id].js`... pages that begin with [] are dynamic routes!
```js
import Layout from '../../components/layout'

export default function Post() {
  return <Layout>...</Layout>
}

export async function getStaticPaths() {
  // Return a list of possible value for id
export async function getStaticProps({params}){
  // fetch necessary data for blog post using params.id
}
```
- use `getStaticProps` to fetch data for a post

**How to generate pages w dynamic routes**
- if you want to generate a page at a path called `/posts/<id>` where `id` can be dynamic, then...

- a Page file must contain...
1. A React component to render this page
2. *getStaticPaths* which returns an array of possible values for id
3. *getStaticProps* which fetches necessary data for the post with id

## Deployment
- Github repo can be public or private, no need to initialize with README or other files
- deploy to Vercel platform, create an account at https://vercel.com/signup
- import your repo on Vercel
- Develop, Preview, Ship
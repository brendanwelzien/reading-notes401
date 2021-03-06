# Fundamental React.js concepts

1. React is all about *components*
- reusable components which are small and then brought together to form bigger components
- they are *reusable*
- in its simplest form, it is a Javascript function
```js
function Button(props){
    return.....
}
ReactDom.render...
```

- every component receives a list of **attributes** which are called **props**
- **JSX** is a Javascript extension and is also a *compromise*

2. JSX
- React's `createElement` is a higher-level function that creates elements to represent React components... It accepts a number of arguments after the second one to represent *children*, so `createElement` makes a `tree`
- JSX is a compromise that allows us to write React components in a syntax similar to HTML

3. You can use JS expressions anywhere in JSX
- this means you can use any JS expressoin *within a pair of curly braces*
- caveat is you cannot use statements like `if`, but a ternary expression is ok

4. You can write React components with Javascript classes
- define a class that extends `React.Component` which defines a single instance function `render()` and that render function returns virtual DOM element
    - you use `this.props.label` inside JSX in rendered output because every element rendered through a class component *gets a special instance property called props* that holds all values passed to that element when it is created
    - if you want to customize the props with an id for example you would use a *constructor function*
```js
// Example 10 -  Customizing a component instance
// https://jscomplete.com/repl?j=rko7RsKS-
class Button extends React.Component {
  constructor(props) {
    super(props);
    this.id = Date.now();
  }
  render() {
    return <button id={this.id}>{this.props.label}</button>;
  }
}
// Use it
ReactDOM.render(<Button label="Save" />, mountNode);
```
5. Events in React: Two Differences
- all react elements attributes events included are named using camelCase
- we pass a JS function reference as the event handler, rather than the string... It is `onClick={handleClick}`, not `onClick="handleClick"`

6. Every react component has a story
- only applies to class component only (those that extend React.Component). Function components have a slgihtly different story
    1. First, we define a template for React to create elements from the component
    2. Then, oinstruct React to use it somewhere (render for another component for example)
    3. React instantiates an element and gives it a set of *props* that we can access with `this.props` (what is passed in step 2)
    4. The constructor method will be called (if defined), this is the first of what we call: *component lifecycle methods*
    5. React then computes the output of the render method(virtual DOM node)
    6. Since this is the first time React is rendering the element, React will communicate w browser to display element(mounting)
    
7. React components can have a private state




# React Native
- framework for building native ios or android apps using Javascript
- facebook, instagram are built with react native
1. React native CLI or Expo CLI to build react native apps

- use expo if you have never built an app before
- expo does have its drawbacks as it does not have all the flexibility compared to react native CLI

## Setting up development environment
1. make sure you are running node 12.0 version or higher
- `node -v`
2. `npm i -g expo-cli`
3. install expo client on your phone so you can run your app on device
... will continue by creating an app
4. `expo init` to pick starting template
5. `npm start` in termninal will start the app
6. in simulator to open developer tool use `ctrl + d` and `command + d`, the dropdown list should appear

- since we do not have div and other html access we use `View /` as a layout to represent such entities
-  `safeareaview` used for padding and proper formatting, which you need to import
- wrap `text /` with component

# Dimensions of Components
- import view component
- account for points in pixels and the scale multiplier which will give the correct pixels needed for the height and width of device
- use console.log(dimensions.get("screen"));
- import
- changes `orientation` mode to default from portrait to adjust for dimension changes in app.json
- hooks start with `use`
  - npm i @react-native-community/hooks
  - import { useDimensions, useDeviceOrientation } from '@react-native-community/hooks'
  - this will get us the dimensions of the screen for multiple orientations
  - console.log(useDimensions, useDeviceOrientation)
    - this will give us the properties for each orientation when we rotate the phone (portrait and/or landscape)
    - const orientation = useDeviceOrientation(); 

# Flexbox
- setting flex to 1 gives the view to take entire space of screen
- align children inside flex container
- add another `<View />` with `style={{}}` as a child to fill container
- `flexDirection`, by default items are laid out in portrait mode
- justifyContent aligns content along main axis (either column for flexDirection Column or row for flexDirection Row)
- alignItems aligns content along secondary axis
- alignSelf is used for children element to move independently inside flex container
- alignContent only works when flexWrap is enabled
- absolute positioning: moves dependent container
- relative positioning: moves inside container

- create a new folder `app` and put all of the source code in there, so move the assets folder inside and update the path for assets in json file if needed
- add component folders if you want for organization... Such as screens and then screens/welcomeScreen.js, etc.

# Importing style sheet

- when wanting to add style
  1. you can use the *style* property to add styles inline BUT you should use the **styleSheet* for styling

App.js
```js
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
import PresentationalComponent from './PresentationalComponent'

export default class App extends React.Component {
   state = {
      myState: 'This is my state'
   }
   render() {
      return (
         <View>
            <PresentationalComponent myState = {this.state.myState}/>
         </View>
      );
   }
}
```
PresentationComponent.js
```js
import React, { Component } from 'react'
import { Text, View, StyleSheet } from 'react-native'

const PresentationalComponent = (props) => {
   return (
      <View>
         <Text style = {styles.myState}>
            {props.myState}
         </Text>
      </View>
   )
}
export default PresentationalComponent

const styles = StyleSheet.create ({
   myState: {
      marginTop: 20,
      textAlign: 'center',
      color: 'blue',
      fontWeight: 'bold',
      fontSize: 20
   }
})
```
- notice the `const` for styles and to access you use `props.myState`
  - this will render a blank screen with blue text "this is my state"

# Layout
- flexDirection
  - 'column', 'row'	
    - Used to specify if elements will be aligned vertically or horizontally.
- justifyContent
  - 'center', 'flex-start', 'flex-end', 'space-around', 'space-between'
    - Used to determine how should elements be distributed inside the container.
- alignItems
  - 'center', 'flex-start', 'flex-end', 'stretched'
    - Used to determine how should elements be distributed inside the container along the secondary axis (opposite of flexDirection)

App.js
```js
import React, { Component } from 'react'
import { View, StyleSheet } from 'react-native'

const Home = (props) => {
   return (
      <View style = {styles.container}>
         <View style = {styles.redbox} />
         <View style = {styles.bluebox} />
         <View style = {styles.blackbox} />
      </View>
   )
}

export default Home

const styles = StyleSheet.create ({
   container: {
      flexDirection: 'column',
      justifyContent: 'center',
      alignItems: 'center',
      backgroundColor: 'grey',
      height: 600
   },
   redbox: {
      width: 100,
      height: 100,
      backgroundColor: 'red'
   },
   bluebox: {
      width: 100,
      height: 100,
      backgroundColor: 'blue'
   },
   blackbox: {
      width: 100,
      height: 100,
      backgroundColor: 'black'
   },
})
```
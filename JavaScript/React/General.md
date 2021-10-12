# General

React is a JS library that aims to simplify the development of visual interfaces.

### Installation & Launching

The most simple way to install react is to navigate to the destination of the project and run the command `npx create-react-app <app name>`. This will download the latest release of `create-react-app`, run it, and then remove it from your system. It will also initialize a [Git](../../Git.md) repository.

You can then start the app by targeting the newly created application folder and running `npm start`

 ## React Components

A typical react application comes with a series of files that do various things, mostly related to configuration. These are called [Components](Components/General.md). The first and main component is `App.js`

```jsx
import React from 'react'
import logo from './logo.svg'
import './App.css'

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  )
}

export default App
```

#### JSX

The HTML like language used to build a component's output in react is called **JSX**. A component's ultimate goal is returning some JSX. However, it also has other characteristics.

Everything returned by a component is in JSX format. React processes JSX and transforms it in JS that the browser can interpret. 

JSX makes it easier to compose and build UI interfaces.

#### State

A component can have its own [state](#Managing State), meaning it encapsulates some variables that other components can't access unless this component exposes this state to the rest of the app.

#### Prop

A component can also receive data from other components. These received data are called props.

### Creating Components

A component is usually created in its own file. This makes it easier to reuse a component by importing it in other components. Components however can also be created in the same file as other components.

The general format of a component is:

```jsx
function WelcomeMessage() {
    return <p>Welcome!</p>
}
```

To display the component onto the webpage, we add it into the `App()` function in the `App.js`

```jsx
<WelcomeMessage/>
```

### Imbedding JS into JSX

JS can be used in JSX code by using curly brackets. 

For example, to reference a JS variable in JSX, we do:

```jsx
import logo from './logo.svg'
...
<img src={logo} className='App-logo' alt="logo" />
```

You can add any JS statement inside curly brackets. However, a pair of curly brackets is limited to one statement. That statement must also return a value.wha

```jsx
const message = 'hello'
return {message === 'hello' ? 'Hello!':message}
```

## Managing State

A state is the set of data that is managed by a component. Every component can have its own state. React is based on and makes heavy use of component's state.

Ex:

> An html form is composed of individual input elements,  including buttons or links. Each of these input elements is responsible for managing its own state. 
>
> The button is responsible for knowing if it's being clicked, or if it's on focus.
>
> The link is responsible for knowing if the mouse if hovering over it, or if it is being clicked.

A state is managed using `useState` . To import it, use `import React, { useState } from 'react'`.

The function `useState()` can take in the initial value of the state item and returns an array containing the state variables as well as the function to call to alter the state.

```javascript
const [count, setcCount] = useState(0)
```

Calling the modifier function is the only method to alter the value of a state variable directly. Otherwise, the component will not update its UI to reflect the changes of data.

 The function can be used as many times to create as many state variables as needed. 

```jsx
const [count, setCount] = useState(0)
const [count2, setCount2] = useState(0)
```

### Example

```jsx
const Counter = () => {
    const [count, setCount] = useState(0)
    return (
    	<div>
        	<p>You clicked me {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click Me!</button>
        </div>
    )
}
```

## Component Props

Props are the initial values passed to a component.

### Passing Props

Props can be passed as arguments inside the component:

```jsx
function WelcomeMessage(props) {
    return <p>Welcome!</p>
}
```

When calling the component inside of JSX, the prop is passed as an attribute

```jsx
<WelcomeMessage myprop={'value'} />
```

In order to get a prop by name, object destructuring can be used:

```jsx
function WelcomeMessage( { myprop }) {
    return <p>{myprop}</p>
}
```

### Children

Children are special props which contain the value of anything that is passed between the opening and closing tags of the component

```jsx
<WelcomeMessage> Message </WelcomeMessage>
function WelcomeMessage( { children }) {
    return <p>{chidlren}</p>
}
```

## Data Flow in React App

A component either holds data (has state) or receives data through its props. 

Data typically flows from a parent component to a child component using props. If you pass a function to the child component, you can change the state of the parent component from a child component.

```jsx
const [count, setCount] = useState(0)
<Counter setCount={setCount} />
```

Inside the `Counter()` component, the `setCount` prop can be called to update the `count` state in the parent component.

```jsx
function Counter({ setCount }) {
    setCoiunt(1)
}
```

## Handling User Events

### Click Events

Click events are usually handled by the `onClick` attribute used in a JSX element

#### Handle Event Within Element

```jsx
<button onClick = { (event) => {
  	/* Code to Handle Event */  
}}>
	Click Me
</button>
```

#### Handle Event through External Function

```jsx
const handleClickEvent = (event) => {}
function App() {
    return <button onClick={handleClickEvent}>Click Me!</button>
}
```

Other events supported by react include `onKeyUp`,  `onFocus`, `onChange`, `onMouseDown`,  `onSubmit` and many more.

## Lifecycle events in a Component

The `useEffect` hook allows components to have access to the lifecycle events of a component. When a hook is called, a function passed to it which will run when the component is first rendered as well as on every subsequent re-render/update. `useEffect()` is usually used for adding logs, accessing 3rd party APIs, and more.

React first updates the DOM, then calls any function passed to `useEffect()` while also not blocking any UI rendering.

### Clicker Example

```jsx
import React, {userState, useEffect} from 'react'
const CounterWithNameANdSideEffect = () => {
    const [count, setCount] = useState(0)
    useEffect(() => {
        console.log('You clicked ${count} times')
    })
    return (
    <div>
    	<p>You clicked {count} times</p>
		<button onClick = {() => setCount(count+1)}>Click Me!</button>
	</div>
    )
}
```

In this example, react will listen for a button click, which will change the value of `count`. Then, the next time that react subsequently re-renders/updates, the new value will be displayed. 

However, re-running the `useEffect()` function constantly to re-render a component can have impacts on performance. Therefore, the function can be declared with a second parameter which is an array containing a list of state variables to watch for. React will then only re-run the side effect if one of the items in this array changes

```jsx
useEffect(() => {
    console.log('Hi ${name} you clicked ${count} times')
}, [name, count])
```

Passing an empty array, `useEffect(() => {}, [])`, can also tell react to only execute the side effect once










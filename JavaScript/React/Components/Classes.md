## Classes

### Constructors

The class constructor for a react component is called before it is mounted.  

It is usually unnecessary to implement a constructor unless for two purposes:

* Initializing `local state` by assigning an object to `this.state`
* Binding `event handler` methods to an instance

> **State:** are similar to props but are private and fully controllable by the component

A constructor also can have `props` passed into it. The first statement in a constructor class should be `super(props)`. Otherwise, `this.props` will be undefined in the constructor (However,  if a constructor is not needed, `this.props` can still be used in other methods without declaring `super(props)`)

Constructors are the only place that states can be initialized by using `this.state`. In other class methods, the function `this.setState()` should be used instead

```jsx
constructor(props) {
    super(props);
    this.state = {counter: 0}
    this.handleClick = this.handleClick.bind(this);
}
```

### Render

The `render()` method determines what the component will render. It is the only **required method** in a class.

A render method should not modify component states. It should return the same result each time it is invoked, and it does not directly interact with the browser.

When called, the `render()` method should examine `this.state` and `this.props` and return one of the following:

* React Elements
* Arrays and Fragments
* Portals
* String and Numbers
* Booleans or Null

### Component Did Mount

The `componentDidMount()` hook function is invoked after a React component has been mounted (After it is inserted into the HTML tree and the first instance of `render()` is called)

The hook is really useful for fetching data or making API calls, as these should only be done usually when the component loads or otherwise there could be inconsistencies in the code.

#### Using `setState()`

Although `setState()` can be used in `componentDidMount()`, it is not recommended. The state will change immediately, however, it will also cause a second re-render. This second re-render is not seen by the user as the page is still loading, however, there can be some performance issues because of this. Therefore, the state should only be initialized in a constructor. 

#### Example

An example in use is the following:

```jsx
class ChildComp extends React.Component {
    componentDidMount() {
        console.log('Mounted')
    }
    render() {
        console.log('rendered')
        return <h1>Clicked {this.props.number} times</h1>
    }
}
class App extends React.Component {
    state = {num: 0};
	handleClick() {
        this.setState(state => ({num:state.num +1}));
    }
	render() {
        return (
        	<button onClick={this.handleClick.bind(this)}>Increment</button>
            <ChildComp number={this.state.num} />
        )
    }
}
```

### Component Did Update

The method `componentDidUpdate(prevProps, prevState, snapshot)` is invoked immediately after updating occurs but not for the initial render. 

This method can be used to to operate on the DOM when the component has been updated, or do network requests or anything that depends on the component states updating.

It is important to note that any statements executed in the method must be encapsulated by some condition |(usually comparing current state/prop to previous state/prop), or else all statements will be executed when only one state has changed

```jsx
componentDidUpdate(prevProps, prevState) {
    if(this.props.userID !== prevProps.userID) {
        this.fetchData(this.props.userID)
    }
}
```

#### Using `setState()`

Although it can be used in the method, `setState()` should be wrapped in a condition or else an infinite loop will be caused. This is because `componentDidUpdate()` is also called when a state is updated, and `setState()` does just that.

### Component Will Unmount

The method `componentWillUnmount()` is invoked immediately before a component is unmounted and destroyed.. The method can be used to perform any necessary cleanup like invalidating timers, cancelling network requests, or cleaning up any subscriptions that were created in `componentDidMount()`

#### Using `setState()`

Since the component is being destroyed and therefore will never be re-rendered, the `setState()` function should not be called.

## Using State Correctly

### 1. States Should not be Modified Directly

In order for the component to re-render, the states must be modified using `setState()`. Doing `this.state.comment = 'Hello'` will not re-render the state. The only place where the state can be modified directly is in the constructor

### 2. State Updates may be Asynchronous

React may batch multiple `setState()` calls into a single update for performance. Therefore, the values of  `this.props` and `this.state` should not be relied upon for calculating the next state as they may be update asynchronously. 

An example of code that may fail to update is this counter:

```jsx
// Wrong
this.setState({ 
	counter: this.state.counter + this.props.incremeent;
})
```

To fix this code, pass a function with object parameters into `setState()`. This function will receive the previous state as the first argument, and the props at the time the update is applied as the second argument

```jsx
// Correct
this.setState((state, props) => ({
    counter: state.counter + props.increment
}));
```

### 3. State Updates are Merged

When `setState()` is called, react merges the object provided into the current state. A state may contain several independent variables which can be independently updated with separate `setState()` calls.
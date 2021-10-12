

## Clock Example

### Adding Local State 

In this example, a function of a ticking clock will be converted into a class

```jsx
function Clock(props) {
    return (
    	<div>
            <h2>The time is {props.date.toLocaleTimeString(){</h2>
        </div>
    );
}
function tick() {
    ReactDOM.render(
    	<Clock date={new Date()} />
        document.getElementById('root')
    );
}
setInterval(tick, 1000)
```

In order to make the clock update itself without doing so in the `ReactDOM.render()` function, we will have to add a `state` to the Clock component. 

In order to convert the function to a class:

1. Create an ES6 class which extends `React.Component`
2. Implement a method called `render()` into the class
3. Replace `props` with `this.state`

```jsx
class Clock extends React.Component {
    render() {
        return (
        	<div>
 				<h1>It is {this.state.date.toLocaleTimeString()}</h1>           
            </div>
        )
    }
}
```

The `render()` method is called each time an update happens. In addition, as long as `<Clock />` is rendered into the same `ReactDOM.render()` node, only a single instance of Clock class will be used.

Then, in order to initiate the state variable, we can have a `constructor()` which is passed a prop that defines the initial value of the state.

```jsx
constructor(props) {
    super(props);
    this.state = {date: new Date()}
}
```

Now, the render method can be changed to include the new Clock class

```jsx
ReactDOM.render(
	<Clock />,
    document.getElementById('root')
)
```

### Adding Lifecycle Methods

Firstly, whenever the clock is [mounted](#Component Did Mount), a timer must be set up. When the clock is [unmounted](#Component Will Unmount), the timer must be also cleared.

```jsx
componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
}
```

Then, we can tear down the timer when the clock is unmounted:

```jsx
componentWillUnmount() {
    clearInterval(this.timerID);
}
```

Finally, a `tick()` method will be implemented which will run every second and update a state of the variable

```jsx
tick() {
    this.setState({
        date: new Date()
    });
}
```

### Recap

Let’s quickly recap what’s going on and the order in which the methods are called:

1. When `<Clock />` is passed to `ReactDOM.render()`, React calls the constructor of the `Clock` component. Since `Clock` needs to display the current time, it initializes `this.state` with an object including the current time. We will later update this state.
2. React then calls the `Clock` component’s `render()` method. This is how React learns what should be displayed on the screen. React then updates the DOM to match the `Clock`’s render output.
3. When the `Clock` output is inserted in the DOM, React calls the `componentDidMount()` lifecycle method. Inside it, the `Clock` component asks the browser to set up a timer to call the component’s `tick()` method once a second.
4. Every second the browser calls the `tick()` method. Inside it, the `Clock` component schedules a UI update by calling `setState()` with an object containing the current time. Thanks to the `setState()` call, React knows the state has changed, and calls the `render()` method again to learn what should be on the screen. This time, `this.state.date` in the `render()` method will be different, and so the render output will include the updated time. React updates the DOM accordingly.
5. If the `Clock` component is ever removed from the DOM, React calls the `componentWillUnmount()` lifecycle method so the timer is stopped.


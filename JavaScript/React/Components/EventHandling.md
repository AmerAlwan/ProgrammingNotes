# Event Handlers

### Preventing Default Events

To prevent default events (like the default link behaviour of opneing a new page), you have to use the `event.preventDefault()` function

```jsx
function handleClick(event) {
    event.preventDefault()
}
```

## Adding Listeners

Unlike HTML, react does not call `addEventListener()` to add listeners to a DOM element after its creation. Instead, a listener is provided when the element is initially rendered.

```jsx
handleClick() {
    this.setState(state => ({
		isToggleOn: !state.isToggleOn
    }));
}
```

There are usually two methods of adding listeners:

### Binding

#### In Element Attribute

```jsx
<button onClick={this.handleClick.bind(this)}
```

#### In Component Constructor

```jsx
constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
}
...
<button onClick={this.handleClick}></button>
```

### Arrow Functions

#### Class Fields Syntax

```jsx
class Button extends React.Component {
    handleClick = () => {console.log(this)}
    render() {
       return (<button onClick={this.handleClick}></button>);
    }
}
```

#### Without Class Fields Syntax

```jsx
<button onClick={() => this.handleClick()}</button>
```

The problem with this syntax is that a different callback is created each time the `LoggingButton` renders. In most cases, this is fine. However, if this callback is  passed as a prop to lower components, those components might do an extra re-rendering. We generally recommend binding in the constructor or  using the class fields syntax, to avoid this sort of performance  problem.

## Passing Arguments to Event Handlers

### With Arrow Function

With an arrow function, parameters are passed into the event handling method direcelty. The event parameter is also passed in last

```jsx
<button onClick={(e) => this.deleteRow(id, e)}></button>
```

### With Binding

```jsx
<button onClick={this.deleteRow.bind(this, id)}></button>
```


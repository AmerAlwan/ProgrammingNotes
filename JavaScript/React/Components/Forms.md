# Forms

HTML form elements work a little differently from other DOM elements in React, because form elements naturally keep some internal state.

## Controlled Components

In HTML, form elements such as `<input>`, `<textarea`, and `select` typically maintain their own state and update it based on user input. In react, mutable state is typically kept in the state property of components, and only updated with `setState()`

The two can be combined by making the React state be the "single source of truth". Then, the react component that renders a form also controls what happens in that form on subsequent user input.. These input form elements whose value is controlled by react in this way are called a **controlled component**.

### Example

Take this example if a form that takes some input and then prints it to the console when the submit button is pressed.

```jsx
class NameForm extends React.Componenet {
    constructor(props) {
        super(props)
        this.state = {value: ''};
        this.handleChange = this.handleChange.bind(this);
        this.handleSubmit = this.handleSubmit.bind(this)
    }
    handleChange(event) {
        this.setState({value: event.target.value})
    }
    handleSubmit(event) {
        console.log(this.state.value)
        event.preventDefault(); // Prevents default behaviourof HTML form of refreshing page on submit
    }
    render() {
        return (
        	<form onSubmit={this.handleSubmit}>
            	<label>
                	Name:
                    <input type="text" value={this.state.value} onCahnge={this.handleChange} />
                </label>
                <input type="submit" value="Submit" />
            </form>
        );
    }
}
```

In this example, the `value` attribute of the form element is set to be `this.state.value`. This makes the react state the source of truth. Since `handleChange` runs on every keystroke to update the React state, the displayed value will update as the user types.

**What is the point:** Although we have written more code, the input;s value will always be driven by the React state. This state can now be passed to other UI elements or reset from other event handlers.

## Text Area

In React, a `<textarea>` uses a `value` attribute instead of having the text defined by its children as in HTML.

```jsx
class EssayForm extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            value: 'Text'
        }
        this.handleChange = this.handleChange.bind(this);
        this.handleSubmit = this.handleSUbmit.bind(this);
    }
    handleChange(event) {
        this.setState({value: event.target.value});
    }
    handleSubmit(event) {
        event.preventDefault();
    }
    render() {
        return (
        	<form onSubmit={this.handleSubmit}>
            	<label>
                	Essay
                    <textarea value={this.state.value} onChange={this.handleChange} />
                </label>
                <input type="submit" vslue="Submit" />
            </form>
        )
    }
}
```

## The Select Tag

In HTML, the select tag produces a dropdown where the default selected value is defined by a `selected` attribute. In react however, the default selected element is set by adding using a `value` attribute on the root `select` tag.

```jsx
class SelectForm extends React.Component {
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
        event.preventDefault();
    }
    render() {
        return (
        	<form onSubmit={this.handleSubmit}>
            	<label>
                	Pick your Favorite Flavour:
                    <select value={this.state.value} onChange={this.handleChange}>
                    	<option value="grapefruit">Grapefruit</option>
                        <option value="lime">Lime</option>
                        <option value="coconut">Coconut</option>
                        <option value="mango">Mango</option>
                    </select>
                </label>
                <input type="submit" value="Submit" />
            </form>
        )
    }
}
```

#### Selecting Multiple Values

To select multiple elements, the `multiple` attribute is assed as well as an array is passed into the `value` attribute allows selecting multiple items in the `select` tag.

```jsx
<select multiple={true} value={['B', 'C']}></select>
```






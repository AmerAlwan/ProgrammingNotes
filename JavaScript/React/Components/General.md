# Components and Props

Components are like JS functions, as in they accept arbitrary inputs (called props or properties) and return react elements describing what should appear on the screen.

## Function and Class Components

### Function Components

Function components are called so because they are exactly like normal JS functions except that they accept a single props object argument and return a react element in the form of JSX.

```jsx
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>
}
```

### ES6 Class

A component can also be defined using a `ES6 Class`.

```jsx
class Welcome extends React.Component {
    render() {
        return <h1> Hello, {this.props.name}</h1>
    }
}
```

This above class will behave similarly to the [function component](#Function Components).

## Component Rendering and Composition

React elements cannot only be represented as DOM tags like `const element = <div />;`, but they can also be represented as user-defined components like `const element = <Welcome name="Amer" />;`

The JSX attributes and children of a component are passed into the component as a single object, `props`.

Components can also refer to other components in their output, which allows the use of the same component abstractions for any level of detail. Components can usually be expressed by buttons, forms, dialogs, screens, and many other typical html implemented or custom attributes.

### Extracting Components

In this example, a `Comment` component is split into smaller components. 

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

The component accept `author` (an object), `text` (a string), and `date` (a date) as props, and describes a comment on a social media website.

Firstly, the `Avatar` element can be extracted into its own component. 

```jsx
function Avatar(props) {
    return (
    	<img className="Avatar"
            src = {props.user.avatarURL}
            alt = {props.user.name}
    )
}
```

Next, `UserInfo` component can be extracted which renders an `Avatar` next to the user's name

```jsx
function UserInfo(props) {
    return (
    	<div className="UserInfo">
        	<Avatar author={props.user} />
            <div className="UserInfo-name">
            	{props.user.name}
            </div>
        </div>
    )
}
```

Finally, the `Comment` props is reduced to the following:

```jsx
function Comment(props) {
    return (
    	<div className="Comment">
        	<UserInfo user={props.author} />
            <div className="Comment-text">
            	{props.text}
            </div>
            <div className="Comment-date">
            	{formatDate(props.date)}
            </div>
        </div>
    );
}
```


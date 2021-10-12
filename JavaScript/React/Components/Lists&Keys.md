# List and Keys

Collections of elements can be built and included in JS and are usually should be rendered inside a component.

List items should also be given a key, which are a special string attribute.

```jsx
function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) => <li key={number.toString()}>{number}</li>);
	return (<ul>{listItems}</ul>);
}
const numbers = [1,2,3,4,5]
ReactDOM.render(
	<NumberList numbers={numbers} />
    document.getElementById('root')
)
```

## Keys

Keys help react identify which items have changed, are added, or are removed. 

### Extracting Components with Keys

Keys should always be specified on the `ListItem />` component rather than on the `<li>` element in the `ListItem` itself.

```jsx
function ListItem(props) {
    // Wrong! The key should not be speciied here
    return <li>{props.value}</li>
}
function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) => 
	// Correct! The key shoul be speicifed inside the array
	<ListItem key={number.toString()} value={number} />
	);
	return (<ul>{listItems}</ul>)
}
const numbers = [1,2,3,4,5];
```

Keys used within arrays should be unique among their siblings. However they don't need to be globally unique. The same component type can have the same key as long as they are in different arrays.

Keys serve only as hints to React but they do not get passed to the components. Therefore, if they key is to be accessed, it has to be passed explicitly  as a prop with a different name.

```jsx
const content = posts.map(post) => <Post key={post.id} id={post.id}});
```

### Embedding Map in JSX

Instead of extracting the components into a separate variable, the components can be embedded into the expression `<ul>` itself.

```jsx
function NumberList(props) {
    const numbers = props.numbers;
    return (
    	<ul>
    		{numbers.map((number) =>
      			<ListItem key={number.toString()} value={number} />                  
			)}    
		</ul>
    );
}
```




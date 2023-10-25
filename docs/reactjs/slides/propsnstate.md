#### What are Props?

- **Props** (short for properties) are used for passing data from a parent component to a child component.
- They are read-only and help make your components reusable.

---

#### Example Component
```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Usage
<Greeting name="Janardhan" />
```

- In the example, the `name` prop is passed from the parent component.

---

#### Default Props

- You can provide default values for props.
- These defaults are used if the parent component doesn't provide a value.

```jsx
Greeting.defaultProps = {
  name: "Guest",
};
```

---

#### What is State?

- **State** is a mechanism for components to have their internal data that can change over time.
- State allows components to be dynamic and interactive.

---

#### Example Class Component
```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return (
      <div>
        Count: {this.state.count}
      </div>
    );
  }
}
```

- The `count` property in the component's state is displayed in the render method.

---

#### Modifying State

#### Example Class Component with State Modification
```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  incrementCount() {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        Count: {this.state.count}
        <button onClick={() => this.incrementCount()}>Increment</button>
      </div>
    );
  }
}
```

- `setState` is used to update the state, which triggers a re-render of the component.

---

#### Props vs. State

- **Props** are external and should not be changed by the component.
- **State** is internal and can be changed by the component.
- Props are for parent-to-child communication, while State is for a component's internal data.

---

#### Lets Greet by name

``` js []

function Greeting(props) {
    return (
        <h1>Hello {props.name}</h1>
    )
}
export default Greeting;

// We can pass name from parent component
<Greeting name="Janardhan" />
```
- we can pass functions also as props 

``` js [5]
const logGreeting = () => {
    console.log('Greeted')
}

<Greeting name="Janardhan" onGreet={logGreeting} />

```
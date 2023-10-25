## Module 2: React Component Fundamentals

---

#### Lifecycle Methods

- Components have a lifecycle.
- Lifecycle methods are functions called at different stages.
- Common lifecycle methods include `constructor`, `componentDidMount`, and `componentWillUnmount`.


```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    // Initialize state and other setup
  }

  componentDidMount() {
    // Perform tasks after component is mounted
  }

  componentWillUnmount() {
    // Clean up resources before unmounting
  }
}
```

---

#### Handling Events

- React components can handle user events.
- Event handlers are defined as functions.
- Events like `onClick` and `onChange` trigger handlers.


```javascript
import React, { Component } from 'react';

class ClickCounter extends Component {
  state = { count: 0 };

  handleClick = () => {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Clicked {this.state.count} times
      </button>
    );
  }
}
```

---

#### Conditional Rendering

- Conditionally render components or content.
- Use `if` statements or ternary operators.
- Decide what to display based on component state or props.


```javascript
import React from 'react';

function Greeting(props) {
  return (
    <div>
      {props.isLoggedIn ? <h1>Welcome, User!</h1> : <h1>Please sign in.</h1>}
    </div>
  );
}
```

---

#### Lists and Keys

- Render lists of items efficiently.
- Use the `map` method to iterate and create components.
- Provide a unique `key` to each list item for efficient updates.


```javascript
import React from 'react';

function ItemList(props) {
  const items = props.items;
  const listItems = items.map((item) => (
    <li key={item.id}>{item.name}</li>
  ));

  return <ul>{listItems}</ul>;
}
```

---

#### Forms and Controlled Components

- Create forms in React for user input.
- Use controlled components to manage form state.
- Handle form submission and validation.


```javascript
import React, { Component } from 'react';

class NameForm extends Component {
  constructor(props) {
    super(props);
    this.state = { value: '' };
  }

  handleChange = (event) => {
    this.setState({ value: event.target.value });
  }

  handleSubmit = (event) => {
    alert('Name submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="text" value={this.state.value} onChange={this.handleChange} />
        <button type="submit">Submit</button>
      </form>
    );
  }
}
```

---

#### What is JSX?

- JSX stands for JavaScript XML.
- It's a syntax extension for JavaScript.
- JSX allows us to write HTML-like code in JavaScript.

---

#### Why Use JSX?

- JSX is used in React for defining the structure of components.
- Benefits of JSX:
  - Declarative: Easier to visualize the UI.
  - Integrates HTML-like tags with JavaScript.
  - Provides a concise and readable way to create components.

---

#### JSX Syntax

- JSX elements resemble HTML elements.
- JSX expressions are enclosed in curly braces `{}`.
- Elements must have a single root element (e.g., `<div>`).
- Class and style attributes are written as `className` and `style`.


```javascript
const element = <h1>Hello, JSX!</h1>;
```

---

#### JSX and JavaScript

- JSX is transpiled to JavaScript.
- JSX elements become `React.createElement()` calls.
- JavaScript expressions are evaluated inside `{}`.

```javascript
const element = <h1>Hello, JSX!</h1>;
```

```javascript
const element = React.createElement("h1", null, "Hello, JSX!");
```

---

#### JSX Elements

- JSX elements can be assigned to variables.
- Elements can include children, attributes, and expressions.


```javascript
const greeting = <h1>Hello, JSX!</h1>;
const name = "React";
const element = <p>{`Welcome, ${name}`}</p>;
```

---

#### Conditional Rendering with JSX

- JSX can be used for conditional rendering.
- Ternary operators or `if` statements can be used within `{}`.


```javascript
const isLoggedIn = true;
const greeting = isLoggedIn ? <p>Welcome, User!</p> : <p>Please sign in.</p>;
```

---

#### Mapping and Lists with JSX

- JSX is commonly used to map over arrays and create lists.
- Each item must have a unique `key` for efficient rendering.


```javascript
const items = ["Item 1", "Item 2", "Item 3"];
const listItems = items.map((item, index) => (
  <li key={index}>{item}</li>
));
```

---

#### JSX and Events

- JSX supports event handlers.
- Event handlers are defined as functions.
- Common events include `onClick`, `onChange`, and more.


```javascript
function handleClick() {
  alert("Button clicked!");
}

const button = <button onClick={handleClick}>Click Me</button>;
```

---

#### JSX and Components

- JSX can include other React components.
- Components can be composed within JSX.

### Example
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="React" />;
```

---

#### Understanding Nested Components

- Nested components are components within other components.
- They enable complex UI structures and modular development.

- **Advantages of Nested Components**
  - Reusability
  - Separation of Concerns
  - Improved Readability
  - Maintenance Ease

---

#### Real-World Example: iTunes Music Search App

- Let's explore a music search app.
- This app allows users to search for music on iTunes.

- **Components in the App**
- `App` (Parent Component)
- `SearchBar` (Child Component)
- `SearchResults` (Child Component)

---

#### `App` Component

- The top-level component.
- Contains the state and logic for the app.
- Renders the child components.


```javascript
import React, { Component } from 'react';

class App extends Component {
  constructor() {
    super();
    this.state = { query: '', results: [] };
  }

  render() {
    return (
      <div>
        <SearchBar />
        <SearchResults results={this.state.results} />
      </div>
    );
  }
}
```

---

#### `SearchBar` Component

- Responsible for user input and search actions.
- Communicates with the parent component (`App`) using props and callbacks.


```javascript
import React, { Component } from 'react';

class SearchBar extends Component {
  constructor() {
    super();
    this.state = { query: '' };
  }

  handleInputChange = (event) => {
    this.setState({ query: event.target.value });
  }

  handleSearch = () => {
    // Perform search and update parent's state
    this.props.onSearch(this.state.query);
  }

  render() {
    return (
      <div>
        <input
          type="text"
          value={this.state.query}
          onChange={this.handleInputChange}
        />
        <button onClick={this.handleSearch}>Search</button>
      </div>
    );
  }
}
```

---

#### `SearchResults` Component

- Displays the search results.
- Receives data from the parent (`App`) via props.


```javascript
import React from 'react';

function SearchResults({ results }) {
  return (
    <ul>
      {results.map((result, index) => (
        <li key={index}>{result.trackName}</li>
      ))}
    </ul>
  );
}
```

---

#### Nested Component Interaction

- Interaction between parent and child components.
- `SearchBar` communicates search queries to `App`.
- `App` fetches data and passes it to `SearchResults`.


1. User inputs a query.
2. `SearchBar` sends the query to `App`.
3. `App` fetches music data.
4. `App` updates the state with the results.
5. `SearchResults` displays the search results.

---

#### Benefits of Nested Components

- **Modularity:** Each component has a specific responsibility.
- **Reusability:** Components can be reused in other parts of the app.
- **Separation of Concerns:** Easier to understand and maintain.
- **Scalability:** Easy to extend and add new features.

---

#### Real-World Applications

- Nested components are used in various applications.
- E-commerce websites, social media platforms, and more.
- React's component-based architecture simplifies complex UIs.



#### What is ReactJS?

- ReactJS is a popular JavaScript library for building user interfaces.
- Developed and maintained by Facebook.
- Used to create interactive, reusable UI components.

- **Key Features**
  - Component-Based Architecture
  - Virtual DOM
  - Unidirectional Data Flow
  - Reusable UI Components

---

#### The React Ecosystem

- React is often used with other tools and libraries.
- Key tools in the React ecosystem include:
  - React Router (for routing)
  - Redux (for state management)
  - Babel (for transpiling)
  - Webpack (for bundling)

React Ecosystem Example
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import { BrowserRouter as Router } from 'react-router-dom';

ReactDOM.render(
  <Router>
    <App />
  </Router>,
  document.getElementById('root')
);
```

---

#### Setting up the Development Environment

- Setting up a development environment is crucial.
- You'll need Node.js and npm (Node Package Manager).
- Create a new React app using Create React App (CRA).


```bash
npx create-react-app my-react-app
cd my-react-app
npm start
```

---

#### Creating Your First React Application

- A React app consists of components.
- Components are building blocks of your UI.
- Components are composed to create the app.


```javascript
import React from 'react';

function App() {
  return (
    <div>
      <h1>Hello, React!</h1>
    </div>
  );
}
```

---

#### Understanding Components

- Components are the core of React.
- They are reusable, self-contained pieces of UI.
- Components can be functional or class-based.

```javascript
import React from 'react';

function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

---

#### JSX (JavaScript XML) Syntax

- JSX is a syntax extension for JavaScript.
- It looks similar to HTML, but it's not.
- JSX gets transpiled to JavaScript.
- JSX allows embedding expressions.


```javascript
import React from 'react';

function App() {
  const name = 'React';
  return (
    <div>
      <h1>Hello, {name}!</h1>
    </div>
  );
}
```

---

#### React Component Hierarchy

- In React, components can be nested.
- This forms a hierarchy of components.
- Parent components can pass data to child components.


```javascript
import React from 'react';

function App() {
  return (
    <div>
      <Header />
      <MainContent />
      <Footer />
    </div>
  );
}
```

---

#### Virtual DOM and Reconciliation

- React uses a virtual DOM to optimize updates.
- The virtual DOM is a lightweight copy of the actual DOM.
- React performs "reconciliation" to update the real DOM efficiently.


```javascript
const virtualDOM = (
  <div>
    <h1>Hello, React!</h1>
  </div>
);
```

---

#### Component State and Props

- Components can have state.
- State is mutable data that influences rendering.

- Components can receive props (properties).
- Props are read-only and help pass data from parent to child.

```javascript
class Greeting extends React.Component {
  constructor(props) {
    super(props);
    this.state = { message: 'Hello' };
  }

  render() {
    return <h1>{this.state.message}, {this.props.name}!</h1>;
  }
}
```


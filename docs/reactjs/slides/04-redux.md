## Module 4: State Management with Redux

---

#### What is Redux?

- Redux is a predictable state container for JavaScript applications.
- It's commonly used with React but can be integrated into any JavaScript app.
- Redux centralizes and manages the state of your application.

---

#### Key Concepts

- **1. Store**
  - The single source of truth for your application's state.
  - Maintains the state tree.
  - Accessible to all components.
- **2. Actions**
  - Plain JavaScript objects that describe changes to the state.
  - Dispatched by components to update the state.
- **3. Reducers**
  - Pure functions that specify how the state changes.
  - Take the current state and an action, and return the new state.

---

#### Redux Workflow

1. An action is dispatched by a component.
2. The action is processed by a reducer.
3. The reducer updates the state.
4. The updated state is stored in the Redux store.
5. Connected components receive the updated state.

---

#### Setting Up Redux

- Install the `redux` and `react-redux` packages in your project.
- Create a Redux store using `createStore`.
- Use the `Provider` component to wrap your app in Redux.


```javascript
// store.js
import { createStore } from 'redux';
import rootReducer from './reducers';

const store = createStore(rootReducer);

// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import store from './store';
import App from './App';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

---

#### Actions

- Actions are plain JavaScript objects.
- They have a `type` property that describes the action.
- Additional data can be included in the `payload` property.


```javascript
{
  type: 'ADD_TODO',
  payload: 'Buy groceries'
}
```

---

#### Reducers

- Reducers are functions that specify how the state changes.
- They take the current state and an action as parameters.
- The reducer calculates the new state based on the action.


```javascript
const initialState = {
  todos: [],
};

const rootReducer = (state = initialState, action) => {
  if (action.type === 'ADD_TODO') {
    return {
      ...state,
      todos: [...state.todos, action.payload],
    };
  }
  return state;
};
```

---

#### Dispatching Actions

- Components can dispatch actions using `dispatch` from `react-redux`.


```javascript
import { connect } from 'react-redux';

const TodoList = ({ todos, dispatch }) => {
  const addTodo = (text) => {
    dispatch({ type: 'ADD_TODO', payload: text });
  };

  // Rest of the component code
}
```

---

#### Connect Components to Redux

- Use the `connect` function to connect a component to the Redux store.
- It provides the component with state and dispatch.


```javascript
import { connect } from 'react-redux';

const mapStateToProps = (state) => ({
  todos: state.todos,
});

export default connect(mapStateToProps)(TodoList);
```

---

#### Middleware in Redux

- Middleware allows you to add custom functionality to the Redux dispatch process.
- Common middleware includes `redux-thunk` for async actions and `redux-logger` for debugging.


```javascript
import { applyMiddleware, createStore } from 'redux';
import thunk from 'redux-thunk';
import logger from 'redux-logger';
import rootReducer from './reducers';

const store = createStore(rootReducer, applyMiddleware(thunk, logger));
```

---

#### Combining Reducers

- As your app grows, you can split your reducers into smaller functions.
- Use `combineReducers` to combine them into one root reducer.


```javascript
import { combineReducers } from 'redux';
import todosReducer from './todosReducer';
import userReducer from './userReducer';

const rootReducer = combineReducers({
  todos: todosReducer,
  user: userReducer,
});
```

---

#### Actions with Async Operations

- Use `redux-thunk` or other middleware for actions with async operations.


```javascript
const fetchTodos = () => {
  return (dispatch) => {
    dispatch({ type: 'FETCH_TODOS_REQUEST' });

    // Perform async operation
    fetch('/api/todos')
      .then((response) => response.json())
      .then((data) => {
        dispatch({ type: 'FETCH_TODOS_SUCCESS', payload: data });
      })
      .catch((error) => {
        dispatch({ type: 'FETCH_TODOS_FAILURE', payload: error });
      });
  };
};
```

---

#### Redux DevTools

- Redux DevTools is a browser extension for debugging Redux applications.
- It provides a visual interface to inspect and time-travel through your state changes.

---

#### What is Redux Toolkit?

- Redux Toolkit is an official package for efficient state management in Redux.
- It simplifies common Redux patterns and provides utilities to streamline development.

- **Why Redux Toolkit?**
  - Reduces boilerplate code.
  - Encourages best practices.
  - Improves developer productivity.

---

#### Key Features of Redux Toolkit

- **1. ConfigureStore**
  - A function that simplifies store configuration.
  - Automatically includes middleware and enables the Redux DevTools Extension.
- **2. createSlice**
  - A function for generating reducer functions and actions.
  - Defines reducers, actions, and initial state in one place.
- **3. useDispatch**
  - A hook for accessing the store's dispatch function in functional components.
- **4. useSelector**
  - A hook for selecting data from the store's state.

---

#### Setting Up Redux Toolkit

- Install the `@reduxjs/toolkit` package in your project.
- Create a slice using `createSlice` for each piece of state.
- Combine slices using `configureStore` to create the Redux store.


```javascript
// todoSlice.js
import { createSlice } from '@reduxjs/toolkit';

const todoSlice = createSlice({
  name: 'todos',
  initialState: [],
  reducers: {
    addTodo: (state, action) => {
      state.push(action.payload);
    },
  },
});

export const { addTodo } = todoSlice.actions;
export default todoSlice.reducer;
```

---

```javascript
// store.js
import { configureStore } from '@reduxjs/toolkit';
import todoReducer from './todoSlice';

const store = configureStore({
  reducer: {
    todos: todoReducer,
  },
});
```

---

#### Actions with Redux Toolkit

- Redux Toolkit automatically generates action creators.
- Use these action creators to dispatch actions.


```javascript
import { useDispatch } from 'react-redux';
import { addTodo } from './todoSlice';

const TodoForm = () => {
  const dispatch = useDispatch();

  const handleAddTodo = (text) => {
    dispatch(addTodo(text));
  };

  // Rest of the component code
}
```

---

#### Selectors with Redux Toolkit

- Redux Toolkit simplifies state selection using selectors.
- Use `useSelector` to access specific parts of the state.


```javascript
import { useSelector } from 'react-redux';

const TodoList = () => {
  const todos = useSelector((state) => state.todos);

  // Rest of the component code
}
```

---

#### Middleware in Redux Toolkit

- Redux Toolkit configures middleware and the Redux DevTools Extension automatically.
- You can still add custom middleware when needed.

### Example
```javascript
import { configureStore, getDefaultMiddleware } from '@reduxjs/toolkit';
import todoReducer from './todoSlice';
import customMiddleware from './customMiddleware';

const store = configureStore({
  reducer: {
    todos: todoReducer,
  },
  middleware: [...getDefaultMiddleware(), customMiddleware],
});
```

---

#### Summary

- Redux Toolkit simplifies and streamlines state management in Redux.
- Key features include `configureStore`, `createSlice`, `useDispatch`, and `useSelector`.
- Actions are generated with action creators.
- Selectors provide easy access to specific parts of the state.
- Middleware configuration is simplified.
- Redux Toolkit promotes best practices and reduces boilerplate code.

---

## Building an iTunes Search App with Redux Toolkit

---

#### Step 1: Project Setup

- Create a new React project using Create React App.
- Install required dependencies:
  - `react-redux` for integrating Redux.
  - `@reduxjs/toolkit` for Redux Toolkit.

*Project Structure*
```
my-itunes-search-app/
  src/
    components/
    features/
      search/
      results/
    app/
    store.js
    index.js
```

---

#### Step 2: Define a Slice

- Create a new slice for the search feature.
- Define the initial state for search results.

###### `searchSlice.js`
```javascript
import { createSlice } from '@reduxjs/toolkit';

const searchSlice = createSlice({
  name: 'search',
  initialState: {
    results: [],
    loading: false,
    error: null,
  },
  reducers: {
    setSearchResults: (state, action) => {
      state.results = action.payload;
      state.loading = false;
      state.error = null;
    },
    setSearchLoading: (state) => {
      state.loading = true;
    },
    setSearchError: (state, action) => {
      state.error = action.payload;
      state.loading = false;
    },
  },
});

export const { setSearchResults, setSearchLoading, setSearchError } = searchSlice.actions;
export default searchSlice.reducer;
```

---

#### Step 3: Create the Redux Store

- Create the Redux store using `configureStore`.
- Add the `search` slice to the store's configuration.

###### `store.js`
```javascript
import { configureStore } from '@reduxjs/toolkit';
import searchReducer from './features/search/searchSlice';

const store = configureStore({
  reducer: {
    search: searchReducer,
  },
});

export default store;
```

---

#### Step 4: Set Up the Search Component

- Create a `Search` component that dispatches search actions.
- Use the `useDispatch` hook to dispatch actions.

###### `Search.js`
```javascript
import React, { useState } from 'react';
import { useDispatch } from 'react-redux';
import { searchiTunes } from './searchSlice';

function Search() {
  const [query, setQuery] = useState('');
  const dispatch = useDispatch();

  const handleSearch = () => {
    dispatch(searchiTunes(query));
  }

  return (
    <div>
      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
      />
      <button onClick={handleSearch}>Search</button>
    </div>
  );
}
```

---

#### Step 5: Define an Async Action

- Create an async action to fetch iTunes search results.
- Use Redux Toolkit's `createAsyncThunk` for async actions.

###### `searchSlice.js`
```javascript
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';

export const searchiTunes = createAsyncThunk('search/searchiTunes', async (query) => {
  const response = await fetch(`https://itunes.apple.com/search?term=${query}`);
  const data = await response.json();
  return data.results;
});
```

---

#### Step 6: Handle Async Action Results

- Update the slice to handle the async action results.
- Use the `fulfilled`, `pending`, and `rejected` reducers.

###### `searchSlice.js`
```javascript
const searchSlice = createSlice({
  name: 'search',
  initialState: {
    results: [],
    loading: false,
    error: null,
  },
  reducers: { /* ... */ },
  extraReducers: (builder) => {
    builder
      .addCase(searchiTunes.fulfilled, (state, action) => {
        state.results = action.payload;
        state.loading = false;
        state.error = null;
      })
      .addCase(searchiTunes.pending, (state) => {
        state.loading = true;
      })
      .addCase(searchiTunes.rejected, (state, action) => {
        state.error = action.error.message;
        state.loading = false;
      });
  },
});
```

---

#### Step 7: Display Search Results

- Create a `Results` component to display search results.
- Use the `useSelector` hook to access the state.

###### `Results.js`
```javascript
import React from 'react';
import { useSelector } from 'react-redux';

function Results() {
  const results = useSelector((state) => state.search.results);

  return (
    <ul>
      {results.map((result) => (
        <li key={result.trackId}>{result.trackName}</li>
      ))}
    </ul>
  );
}
```

---

#### Step 8: Integrate Components

- Integrate the `Search` and `Results` components in your app.

### `App.js`
```javascript
import React from 'react';
import Search from './features/search/Search';
import Results from './features/results/Results';

function App() {
  return (
    <div>
      <Search />
      <Results />
    </div>
  );
}
```


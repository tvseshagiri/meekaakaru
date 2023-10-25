
## Unit Testing and Jest

---

#### What is Unit Testing?

- **Unit Testing** is a software testing technique where individual components or functions of a program are tested in isolation to ensure they work correctly.

- **Purpose**
  - **Validation**: Verify that each part of the software performs its functions as expected.
  - **Regression Testing**: Detect and prevent software bugs when making changes.
  - **Documentation**: Provide documentation and examples of how the code should be used.

---

#### What is Jest?

- **Jest** is a popular JavaScript testing framework.
- Developed by Facebook, it's commonly used for testing JavaScript and TypeScript applications.
- Jest is built on top of Jasmine and provides a rich set of features for writing unit tests.

- **Features**
  - **Automatic Mocking**: Mocking of functions and modules.
  - **Assertion Library**: Built-in assertions using `expect`.
  - **Test Runner**: Execute tests and provide test results.
  - **Snapshot Testing**: Capture snapshots of rendered UI components.

---

#### Writing Your First Jest Test


1. Install Jest:

   ```bash
   npm install --save-dev jest      
   ```

2. Create a test file:

   ```javascript
   // myFunction.test.js

   test('Example Test', () => {
     // Test code here
   });
   ```

3. Run the tests:

   ```bash
   npx jest
   ```

---

#### Writing Test Suites and Test Cases

- **Test Suite**: A collection of test cases for a specific module or component.
- Create a test suite using `describe`:

  ```javascript
  describe('Math Functions', () => {
    // Test cases go here
  });
  ```

- **Test Case**: An individual test scenario within a test suite.
- Create a test case using `test`:

  ```javascript
  test('Addition', () => {
    // Test addition functionality here
  });
  ```

---

#### Using Jest's Expect for Assertions

- **`expect`** is used for making assertions in Jest.
- It allows you to specify what you expect the outcome to be.

```javascript
test('Addition', () => {
  expect(add(2, 3)).toBe(5);
});
```

- Jest provides a variety of assertion methods, like `toBe`, `toEqual`, `toBeTruthy`, and more.

---

#### Running and Organizing Tests

- Run all tests in the project:

  ```bash
  npx jest
  ```

- Run specific test files or test suites:

  ```bash
  npx jest myFunction.test.js
  ```

- Keep test files alongside the code to be tested (e.g., `myFunction.js` and `myFunction.test.js`).
- Organize tests into folders and subfolders to match your project's structure.

---

#### Basic Matchers and Matchers API

- **Common Matchers**:

  - `toBe()`: Strict equality (===).
  - `toEqual()`: Deep equality.
  - `not.toBeNull()`: Ensure a value is not null.

- **Chaining Matchers**:

  ```javascript
  expect(result).toBeGreaterThan(10).toBeLessThan(20);
  ```

- **Negating Matchers**:

  ```javascript
  expect(result).not.toBeFalsy();
  ```

---

#### Detailed Explanation of Matchers

- **Matchers** are functions that check values against expectations.
  - Jest provides a rich set of matchers for various scenarios.
  - `toBe(value)`: Strict equality.
  - `toEqual(value)`: Deep equality.
  - `not`: Inverts the matcher.
  - `toContain(item)`: Checks if an array or string contains an item.
  - `toMatch(regexp)`: Matches a string against a regular expression.

---


#### Testing React Components

- **Component Testing** is the practice of testing individual React components in isolation to ensure they work as intended.

- **Importance of Component Testing**

  - Ensures components render correctly and behave as expected.
  - Helps catch UI bugs early in the development process.
  - Provides confidence when making changes or adding new features.

---

#### Rendering Components for Testing

- **Setting Up a Testing Environment**
  - Choose a testing framework: Jest is commonly used with React.
  - Install required dependencies, e.g., `react-testing-library`.
  - Configure your test environment.


```javascript
import { render } from '@testing-library/react';
import MyComponent from './MyComponent';

test('MyComponent renders correctly', () => {
  const { getByText } = render(<MyComponent />);
  expect(getByText('Hello, World!')).toBeInTheDocument();
});
```

---

#### Assertions on React Components

- **Assertions** validate whether the component behaves as expected.
- Common assertions are provided by the testing library.

```javascript
import { render } from '@testing-library/react';
import MyComponent from './MyComponent';

test('MyComponent renders correctly', () => {
  const { getByText } = render(<MyComponent />);
  expect(getByText('Hello, World!')).toBeInTheDocument();
});
```

---

#### Common Assertions

- `toBeInTheDocument()`: Checks if an element is in the document.
- `toHaveTextContent(text)`: Checks for specific text content.
- `toHaveAttribute(attrName)`: Checks for attributes.

---

#### Testing Component Props and State

- Pass props when rendering components for testing.

```javascript
import { render } from '@testing-library/react';
import MyComponent from './MyComponent';

test('MyComponent receives and displays a prop', () => {
  const { getByText } = render(<MyComponent message="Hello, Test!" />);
  expect(getByText('Hello, Test!')).toBeInTheDocument();
});
```

---

#### Testing State

- Use React Testing Library to interact with and test state changes.

```javascript
import { render, fireEvent } from '@testing-library/react';
import Counter from './Counter';

test('Counter increments when the button is clicked', () => {
  const { getByText } = render(<Counter />);
  const button = getByText('Increment');
  fireEvent.click(button);
  expect(getByText('Count: 1')).toBeInTheDocument();
});
```

---

#### Importance of Mocking in Unit Testing

- **What is Mocking?**

  - **Mocking** is the practice of simulating the behavior of external dependencies or functions during unit testing.
  - It allows you to isolate the code being tested and control the behavior of external components.

- **Why Mocking Is Important**

  - Ensures tests focus on the specific functionality under examination.
  - Speeds up tests by avoiding actual external calls.
  - Makes testing more deterministic and reproducible.

---

#### Using Jest Mocks for Functions and Modules

- **Jest Mocks**
  - Jest provides a built-in mocking system for JavaScript functions and modules.

```javascript
// Original function
const fetchData = () => { /* ... */ };

// Mocked function
jest.mock('./api', () => ({
  fetchData: jest.fn(() => 'Mocked Data'),
}));
```

---

#### Mocking a Module

```javascript
// Original module
import axios from 'axios';

// Mocked module
jest.mock('axios');
axios.get.mockResolvedValue({ data: 'Mocked Data' });
```

---

#### Handling Asynchronous Code with Mocks

- Mocking asynchronous functions with Jest:

```javascript
const fetchData = jest.fn().mockResolvedValue('Mocked Data');

test('Async Function Test', async () => {
  const result = await fetchData();
  expect(result).toBe('Mocked Data');
});
```

- Controlling Asynchronous Timers

- Use `jest.advanceTimersByTime(ms)` to control timers:

```javascript
jest.useFakeTimers();
jest.advanceTimersByTime(1000); // Advance timers by 1 second
```

---

#### Mocking API Calls and Third-Party Libraries

- Mocking HTTP requests with `axios`:

```javascript
import axios from 'axios';

jest.mock('axios');
axios.get.mockResolvedValue({ data: 'Mocked Data' });
```

- Mocking external libraries with `jest.mock`:

```javascript
jest.mock('external-library', () => ({
  someFunction: jest.fn(() => 'Mocked Result'),
}));
```

---

#### Testing Asynchronous Operations with async/await

- **Asynchronous Testing**

  - Many functions in modern applications involve asynchronous operations like API calls, timers, and events.
  - It's essential to test these asynchronous behaviors to ensure your application functions correctly.

- **Using async/await**

  - `async/await` simplifies testing asynchronous code.
  - `await` is used to pause the test until the promise resolves or rejects.

---

```javascript
test('Async Function Test', async () => {
  const result = await fetchData();
  expect(result).toBe('Expected Data');
});
```

---

#### Handling Promises in Tests

- Use `.resolves` and `.rejects` matchers to test promise resolutions and rejections.

```javascript
test('Promise Resolves', async () => {
  await expect(Promise.resolve('Resolved')).resolves.toBe('Resolved');
});

test('Promise Rejects', async () => {
  await expect(Promise.reject('Rejected')).rejects.toThrow('Rejected');
});
```

---

- You can combine `await` with `.resolves` and `.rejects` for testing.

```javascript
test('Async Promise Resolves', async () => {
  await expect(fetchData()).resolves.toBe('Expected Data');
});
```

---

#### Testing Timeouts and Delays

- Use `jest.useFakeTimers()` to control timers.

```javascript
test('Timeout Test', () => {
  jest.useFakeTimers();
  delayedFunction();
  jest.advanceTimersByTime(1000);
  expect(mockCallback).toHaveBeenCalledTimes(1);
});
```

- Use `setTimeout` with a Promise to simulate delays in tests.

```javascript
test('Delayed Function Test', async () => {
  const result = await delayedFunction();
  expect(result).toBe('Delayed Result');
});
```

---

#### Simulating Async Behavior with Jest

- Jest provides methods for simulating async behavior without actual delays.

```javascript
test('Simulated Async Test', async () => {
  jest.spyOn(global, 'fetch').mockResolvedValue({
    json: jest.fn().mockResolvedValue('Simulated Data'),
  });
  const result = await fetchData();
  expect(result).toBe('Simulated Data');
});
```

---

#### Resetting Spies and Mocks

- Don't forget to reset mocks and spies after testing.

```javascript
beforeEach(() => {
  jest.clearAllMocks();
});
```


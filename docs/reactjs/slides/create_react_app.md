#### Let's Create React App with CRA

* __Create React App__ is  an officially  way (one of the ways) to create  React applications. 

``` bash []
    npx create-react-app my-app
    # where 'my-app' is name of our application
    
    # It will take a minute or more to create the app
    
    cd my-app

    #start the application
    npm start 
```

- open http://localhost:3000/ to see the app.

---

#### Folder Structure 
``` bash [8,18]
my-app
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    ├── reportWebVitals.js
    └── setupTests.js

```
- `src/index.js` is the JavaScript entry point.
- `public/index.html` is the page template.

---


#### Commands 
- `package.json` contains following command to manage the application
  
``` json [14:]

"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
```

- `npm start`
    -- Starts the development server.
-  `npm run build`
    -- Bundles the app into static files for production.
-  `npm test`
    -- Starts the test runner.
-  `npm run eject`
    -- Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

---

#### Let's understand how it works

- `public/index.html` defines root element for our application

``` html [29:]
<body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>

    ...
```
- In `src/index.js`, ReactDOM get holds of root element and renders React Component

``` js [7: ]
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

---

#### React Component

`src/App.js` defines the React Component with name __App__

``` js []

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

```

---

#### Try It!!!

Remove everything in between __( )__ of return and Just write `<h2>Hello World!!!</h2>`

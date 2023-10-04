#### React Components

- React apps are made out of components.
- A component is a part of the UI with its own logic and appearance
- React components are JavaScript functions that return markup in the form of JSX

``` js []
// Function Component 
function Greeting() {
    return (
        <h1>Hello World!!!</h1>
    )
}
// Class component 
import React from "react";
class Greeting extends React.Component {
    render() {
        return <h1>Hello, World</h1>;
    }
}
```



---

#### Component Structure 

- Typically React Components defined in its own JS file
- Component names must always start with capital letter
- Components must return markup using return


``` js []

function <Component Name>() {
    return <JSX>
}

export default <Component Name>;

```

---

#### What is JSX

- JavaScript Extension to write HTML in React 
- It is similar to HTML but not lenient
- It helps to write logic, markup in same place which is not the case in HTML

##### Rules
- Must return only a single root element
- __Fragment_ need to be used in case of returning multiple elements
- Follows strict syntax eg. all tags must be closed
- Element attributes names follow cameCases 

---

#### Examples

``` js [4-7, 13-19]

    function Track() {
        return (  // OK Return single DIV as root element 
            <div>
              <h4>Track Name: Jack Johnson</h4>
              <p>artistName: This Bike Is a Pipe Bomb</p>
            </div>
        )
    }

    function Track() {
        return (  // NOT OK  Multiple root elements
            <div>
              <h4>Track Name: Jack Johnson</h4>
              <p>artistName: This Bike Is a Pipe Bomb</p>
            </div>
            <div> 
              <img src="https://is1-ssl.mzstatic.com/image/thumb/Music124/v4/f3/ee/b3/f3eeb3ff-ca32-273a-15aa-709bdfa64367/mzi.izwiyqez.jpg/30x30bb.jpg" />
            </div>
        )
    }
```

---

#### Accessing Dynamic Data in JSX

- Dynamic data can be accessed using __{}__
- __{{}}__ used for passing JavaScript Objects including CSS 

``` js [11, 13-14,19]

const track = {
    title: "Let It Be",
    artist: "The Beatles",
    album: "This Bike Is a Pipe Bomb",
    coverUrl: "https://is1-ssl.mzstatic.com/image/thumb/Music124/v4/f3/ee/b3/f3eeb3ff-ca32-273a-15aa-709bdfa64367/mzi.izwiyqez.jpg/100x100bb.jpg"
}
function Track() {
    return (
        <div>
            <h4>Track Name: {track.title}</h4>
            <div>
                <div style={{ "float": "left", "paddingRight": "12px" }}>
                    <img src={track.coverUrl} alt={track.title} width={100} height={100} />
                </div>
                <div>
                    Artist: {track.artist} <br />
                    Album Name: {track.album}<br />
                    Last Fetched On: {Date()}<br />
                </div>
            </div>
        </div>
    )
}

```
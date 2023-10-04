####  Components Communication - Props

- React components use props to communicate with each other
- Every parent component can pass information to its child components using props
- Props are  like HTML attributes but 
    - HTML attributes can have only string as value
    - React Props values can be objects, functions

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
<Greeting name="John" />
```
- we can pass functions also as props 

``` js [5]
const logGreeting = () => {
    console.log('Greeted')
}

<Greeting name="John" onGreet={logGreeting} />

```
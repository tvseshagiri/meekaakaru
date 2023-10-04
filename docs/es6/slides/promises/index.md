#### Promises

- The __Promise__ object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

- A Promise is in one of these states:
  * pending: initial state, neither fulfilled nor rejected.
  * fulfilled: meaning that the operation was completed successfully.
  * rejected: meaning that the operation failed.

---


#### Promise methods

- Promise has two handler methods
    * __then()__ will be called when Promise is fulfilled (success)
    * __catch()__ will be called when something went wrong

``` js []

fetch(`https://itunes.apple.com/search?term=${term}&media=music&limit=20`)
  .then(res => {
    return res.json()
      .then(data => {
        console.log(data)})
      .catch(err => { alert(err) })})// This will handle if any error happens while converting res->JSON
  .catch(err => { alert(err) }) //This will handle any fetch invocation errors
  
```

---

#### await & async

- await & async simplifies promise handlers handling

``` js []
async function serachiTunes(term) {
  try {
        const resp = await fetch(`https://itunes.apple.com/search?term=${term}&media=music&limit=20`);
        const searchResults = await resp.json();
        return searchResults;
    } catch(e) {
      console.error(e)
    }
}

```
- enclosed function of __await__ must be marked with __async__
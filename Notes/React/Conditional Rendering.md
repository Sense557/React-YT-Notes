
**Conditional Rendering**
**Methods**
**Benefits**

#### Conditional Rendering
- Displaying contain based on *certain conditions*
- Allows for *dynamic* user interfaces

#### Methods
- **If-else statements:** Choose between two **blocks of content** (*covers complete component*)
- **Ternary Operations:** Quick way to choose between **two options**
- **Logical Operators:** Useful for rendering content when a condition is **true**

#### Benefits
- Enhance user **experience**
- **Reduces** unnecessary rendering
- Makes app more **interactive** and **responsive**


## NOTE
- We can't write if-else code / loop inside `JSX`
- So for this we have to do this

## Page looks like this
![[Pasted image 20241021202437.png]]


#### if-else

Using `if-else` to make `dynamic` & `responsive`
```JSX
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  let foodItems = [];

  // let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];

  if(foodItems.length === 0){
    return 'I am Hungry';
  }
  
  return (
    <>
      <h1>Healthy Foods</h1>
  
      <ul className="list-group">
        {foodItems.map((items) => (
          <li key={items} className="list-group-item">{items}</li>
        ))}
      </ul>
    </>
  );
}

export default App;
```
![[Pasted image 20241021203150.png]]


#### Ternary Operators
```JSX
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {

  let foodItems = [];
  // let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];
  let emptyMessage = (foodItems.length === 0) ? <h3>I am Hungry</h3> : null;

  return (
    <>
      <h1>Healthy Foods</h1>

      {emptyMessage}

      <ul className="list-group">
        {foodItems.map((items) => (
          <li key={items} className="list-group-item">
            {items}
          </li>
        ))}
      </ul>
    </>
  );
}

export default App;
```
![[Pasted image 20241021202310.png]]

#### Logical Operators
```JSX
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  let foodItems = [];

  // let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];
  
  return (
    <>
      <h1>Healthy Foods</h1>

      {foodItems.length === 0 && <h3>I am hungry</h3>}

      <ul className="list-group">
        {foodItems.map((items) => (
          <li key={items} className="list-group-item">
            {items}
          </li>
        ))}
      </ul>
    </>
  );
}

export default App;
```
![[Pasted image 20241021202239.png]]



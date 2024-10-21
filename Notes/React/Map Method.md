1. **Purpose:** Render lists from array data
2. **JSX Elements:** Transform Array items into JSX
3. **Inline Rendering:** Directly inside JSX 
	`{items.map(item => <li key={item.id}>{item.name}</li>)}`
4. **Key Prop:** Assign unique key for optimized re-renders
	`<div key={item.id}>{item.name}</div>`


> [!NOTE] Purpose - 
> *Render lists from array data*





**Without** using `map method` helps ? **Hard-Coded**
```JSX
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  return (
    <>
      <h1>Healthy Foods</h1>
      <ul className="list-group">
        <li className="list-group-item">Roti</li>
        <li className="list-group-item">Dal</li>
        <li className="list-group-item">Eggs</li>
        <li className="list-group-item">Milk</li>
        <li className="list-group-item">Apple</li>
      </ul>
    </>
  );
}

export default App;
```


Using `map method` helps ? **helped a lot** 
```JSX
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];
  
  return (
    <>
      <h1>Healthy Foods</h1>

      <ul className="list-group">
        {foodItems.map((items) => (
          <li className="list-group-item">{items}</li>
        ))}
      </ul>
    </>
  );
}

export default App;
```


Using **Key Prop**  *to Assign unique key for optimized re-renders*
```JSX
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];
  
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




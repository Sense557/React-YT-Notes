
1. **What?**
	- Allows grouping of multiple elements without extra DOM nodes
2. **What?**
	- Return multiple elements without *a wrapping parent*
	- *Cleaner DOM* & Consistent Styling
3. **How?** *Two Syntaxes:*
	- `<React.Fragment>...</React.Fragment>`
	- Short: `<>...</>`




## Example
Let's first do some cleanup i.e.
- Delete `index.css`
- Create `App.css`
- do some changes inside `main.jsx`
- do some changes inside `App.jsx`

inside `main.jsx`
```JSX
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import 'bootstrap/dist/css/bootstrap.min.css'
ReactDOM.createRoot(document.getElementById('root')).render(

  <React.StrictMode>
    <App />
  </React.StrictMode>
)
```

inside `App.jsx`
```JSX
import './Index.css'

function App() {
  return (
    <div>
		<h1>Fragment</h1>
    </div>
  )
}

export default App
```


Now the page will look like this
![[Pasted image 20241021001856.png]]


Let's add some **Bootstrap components** and **CSS**

First *install Bootstrap*
```JSX
npm i bootstrap@5.3.3
```

import it inside `App.jsx` & `main.jsx`

#### App.jsx
add some **Bootstrap** components as well and do some changes in list items as well
```JSX
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  return (
    <div>
      <h1>Healthy Foods</h1>
      <ul className="list-group">
        <li className="list-group-item">Roti</li>
        <li className="list-group-item">Dal</li>
        <li className="list-group-item">Vegetables</li>
        <li className="list-group-item">Milk</li>
        <li className="list-group-item">Apple</li>
      </ul>
    </div>
  );
}

export default App;
```


#### main.jsx
```JSX
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./App.css";
import "bootstrap/dist/css/bootstrap.min.css";
ReactDOM.createRoot(document.getElementById("root")).render(

  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```


Now the page looks like this
![[Pasted image 20241021005923.png]]

---

> [!Success] Usage of React Fragment
> In React, fragments allow you to group multiple elements without adding extra nodes to the DOM. You can use fragments in two ways:
> - `<React.Fragment>...</React.Fragment>`
> - Short: `<>...</>`

Benefit of using React Fragments
![[Pasted image 20241021010113.png]]

Without React Fragments
![[Pasted image 20241021010228.png]]


#HOW
- Using `<React.Fragment>`
- Need to *import* `React` else won't work
```JSX
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  return (
    <React.Fragment>
      <h1>Healthy Foods</h1>;
      <ul class="list-group">
        <li class="list-group-item">An item</li>
        <li class="list-group-item">A second item</li>
        <li class="list-group-item">A third item</li>
        <li class="list-group-item">A fourth item</li>
        <li class="list-group-item">And a fifth one</li>
      </ul>
    </React.Fragment>
  );
}

export default App;
```

#HOW
- Using the short syntax `<> </>`
```JSX
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  return (
    <>
      <h1>Healthy Foods</h1>;
      <ul class="list-group">
        <li class="list-group-item">An item</li>
        <li class="list-group-item">A second item</li>
        <li class="list-group-item">A third item</li>
        <li class="list-group-item">A fourth item</li>
        <li class="list-group-item">And a fifth one</li>
      </ul>
    </>
  );
}

export default App;
```







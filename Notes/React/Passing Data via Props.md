
- **Props in React**
- **Usage**
- **Key Points**
- **Examples**

#### Props in React
- Short for *properties*
- Mechanism for *passing data*
- *Read-only* by default

#### Usage 
- Pass data from *parent to child component*
- Makes components *reusable*
- Defined as *attributes* in JSX

#### Key Points
- Data flows *one-way* (downwards)
- Props are *immutable*
- Used for *communication between components*


#### Examples
	`<Header title="My App" />`
 

Let's take an example to see **how Data passing happens via props** ?

To understand it very well take the example of **Healthy Food list** we made earlier in the `conditional rendering` session and do some changes `for better vizualization`

Let's make the app more modular

We have to create `3 components` respectively
1. `FoodItems.jsx`
2. `ErrorMessage.jsx`
3. `Item.jsx` 

### FoodItems.jsx
create a folder named `components` inside `src` i.e. `src/components`

create file named `FoodItems.jsx`  inside `components` folder

let's define `FoodItems` **component** inside it
```JSX
const FoodItems = () => {
    // let foodItems = [];
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];

  return (
    <ul className="list-group">
      {foodItems.map((item) => (
        <li key={item} className="list-group-item">
          {item}
        </li>
      ))}
    </ul>
  );
};

export default FoodItems;
```


**import** that `FoodItems` inside `App.jsx`
```JSX
import FoodItems from "./components/FoodItems";
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  // let foodItems = [];
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];

  return (
    <>
      <h1>Healthy Foods</h1>
      {foodItems.length === 0 && <h3>I am still hungry</h3>}

      <FoodItems />
    </>
  );
}

export default App;
```



### ErrorMessage.jsx
create file named `ErrorMessage.jsx`  inside `components` folder

let's define `ErrorMessage` **component** inside it
```JSX
const ErrorMessage = () => {
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];
  
  return <>{foodItems.length === 0 && <h3>I am still hungry</h3>}</>;
};

export default ErrorMessage;
```


**import** that `ErrorMessage` inside `App.jsx`
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  // let foodItems = [];
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];

  return (
    <>
      <h1>Healthy Foods</h1>
      <ErrorMessage />
      <FoodItems />
    </>
  );
}

export default App;
```


But there is a problem that we have `foodItems` present in all the 3 components and We need to think for the `Item` individually to maintain the UI uniformly

So, let's create `Item.jsx`

### Item.jsx
create file named `Item.jsx`  inside `components` folder

let's define `Item` **component** inside it i.e. move that item   `<li>...</li>`  part from the `FoodItems.jsx` file and replace with the exported component of `Item.jsx`  
```JSX
const Item = () => {
  return (
    <li key={item} className="list-group-item">
      {item}
    </li>
  );
};
  
export default Item;
```


**import** that `Item.jsx` inside `App.jsx`
```JSX
import Item from "./Item";
const FoodItems = () => {

  // let foodItems = [];
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];

  return (
    <ul className="list-group">
      {foodItems.map((item) => (
        <Item></Item>
      ))}
    </ul>
  );
};

export default FoodItems;
```


But the problem is **Item** is not available inside `Item.jsx`

So, we have to pass the *Item* as an attribute inside `<Item></Item>` to make sure that `Item.jsx` got it's item

Let's do some changes inside `App.jsx`
```JSX
import Item from "./Item";
const FoodItems = () => {

  // let foodItems = [];
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];
  
  return (
    <ul className="list-group">
      {foodItems.map((item) => (
        <Item foodItems = {item}></Item>
      ))}
    </ul>
  );
};

export default FoodItems;
```

**pass**  that item as `props` inside `Item.jsx`
```JSX
const Item = (props) => {
  return (
    <li key={props.foodItems} className="list-group-item">
      {props.foodItems}
    </li>
  );
};

export default Item;
```


![[Pasted image 20241021220144.png]]


**Let's resolve this issue**

So, we have to remove the unique `key` present inside `Item.jsx` 
```JSX
const Item = (props) => {
  return (
    <li className="list-group-item">
      {props.foodItems}
    </li>
  );
};
  
export default Item;
```


and put that removed `key` inside `FoodItems.jsx`
```JSX
import Item from "./Item";

const FoodItems = () => {
  // let foodItems = [];
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];

  return (
    <ul className="list-group">
      {foodItems.map((item) => (
        <Item key={item} foodItems = {item}></Item>
      ))}
    </ul>
  );
};

export default FoodItems;
```

Now the `issue is resolved`


There is `another way` how we can resolve the issue using the `de-structuring method`

do some changes inside `Item.jsx`
```JSX
const Item = (props) => {
  let {foodItems} = props;
  return <li className="list-group-item">{foodItems}</li>;
};

export default Item;
```


There is `one more thing` we can do to make it more efficient directly we can pass the `{foodItems}` in place `props`

do changes inside `Item.jsx`
```JSX
const Item = ({foodItems}) => {
  return <li className="list-group-item">{foodItems}</li>;
};

export default Item;
```


One more thing we need to do as we can see the `foodItems` is defined  individually in more than one places. But what it is needed to do is we can pass as `items` to the respective components where it is needed as there we have to **catch** that `items`

this way we can resolve this issue *more efficiently*

do some changes inside `App.jsx`
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";

function App() {
  // let foodItems = [];
  let foodItems = ["Roti", "Dal", "Vegetables", "Milk", "Apple"];

  return (
    <>
      <h1>Healthy Foods</h1>
      <ErrorMessage items = {foodItems} />
      <FoodItems items = {foodItems} />
    </>
  );
}

export default App;
```


let's catch the `items` in place of `fooditems` where it is present in out component file

inside `ErrorMessage.jsx` file do some changes
```JSX
const ErrorMessage = ({items}) => {
  return <>{items.length === 0 && <h3>I am still hungry</h3>}</>;
};

export default ErrorMessage;
```


inside `FoodItems.jsx` file also do some changes 
```JSX
import Item from "./Item";
const FoodItems = ({ items }) => {

  return (
    <ul className="list-group">
      {items.map((item) => (
        <Item key={item} foodItem = {item}></Item>
      ))}
    </ul>
  );
};

export default FoodItems;
```


Now all `issues are resolved`

Let's do a change and `see how our app reacts`

**Change the list and see**
![[Pasted image 20241021224805.png]]



---



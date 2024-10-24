

```JSX
<Container>
	<h1>Welcome to My App</h1>
	<p>This content is passed as children to the
	Container component.</p>
</Container>
```


```JSX
function Container (props) {
	return (
		<div className="container-style">
			{props.children)
		</div>
	);
}
```


1. **children** is a ***special prop*** for passing ***elements into components***
2. **Used for flexible** and ***reusable*** component designs
3. **Common** in layout or ***container components***
4. **Accessed** with ***props.children***
5. **Can be any content:** strings, numbers, **JSX** and components
6. **Enhances** component ***composability*** and ***reusability***

Let's understand this with an #example 

Open our previous project **Healthy Foods Project**

Let's do some changes inside `Item.jsx` file

 
> [!NOTE] Before
```JSX
import styles from "./Item.module.css";

const Item = ({ foodItem }) => {
  return (
    <li className={`${styles["kg-item"]}`}>
      <span className={styles["kg-span"]}>{foodItem}</span>
    </li>
  );
};
  
export default Item;
```

![[Pasted image 20241023085151.png]]



> [!NOTE] After
```JSX
import styles from "./Item.module.css";

const Item = ({ foodItem }) => {
  return (
    <li className={`${styles["kg-item"]} list-group-item`}>
      <span className={styles["kg-span"]}>{foodItem}</span>
    </li>
  );
};
  
export default Item;
```

![[Pasted image 20241023085222.png]]



Only the changes we did is in the list item `list-group-item` is added to apply the **Bootstrap CSS**
```
<li className={`${styles["kg-item"]} list-group-item`}>
```


But here in this the **problem** is see it is **taking the whole width**  but the content is not filled in full width

How to **resolve** that Let's see

Let's ***make a bind container*** so that we can put anything inside that **container**

So Create `Container.jsx` file inside which do some changes
```JSX
const Container = () => {
  return <div>Container</div>
}

export default Container;
```

We are simply returning a blind container

Let's import that inside `App.jsx` inside which do some changes

> [!NOTE] Before
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
  
function App() {
  // let foodItems = [];
  let foodItems = ["Biryani", "Dal", "Vegetables", "Milk", "Apple"];
  
  return (
    <>
      <h1 className="food-heading">Healthy Foods</h1>
      <ErrorMessage items = {foodItems} />
      <FoodItems items = {foodItems} />
    </>
  );
}

export default App;
```




> [!NOTE] After
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
  
function App() {
  // let foodItems = [];
  let foodItems = ["Biryani", "Dal", "Vegetables", "Milk", "Apple"];
  
  return (
    <Container>
      <h1 className="food-heading">Healthy Foods</h1>
      <ErrorMessage items = {foodItems} />
      <FoodItems items = {foodItems} />
    </Container>
  );
}

export default App;
```


we have simply `imported` the ***Container*** component inside `App.jsx`


Now the page will look like this
![[Pasted image 20241023090217.png]]


Why it is looking like this because we have used the Blind/ blank container inside which we just returning the `Container` nothing else

So let's just pass the ***props*** inside which so that we can see some contents of the **container**

Let's do some changes inside the `Container.jsx` file  where the **container** is definded
```JSX
const Container = (props) => {
  return <div>{props.children}</div>
}

export default Container;
```


Now the page again will look like this
![[Pasted image 20241023091009.png]]



Now if you see container has no idea which is being passed inside it and it has no **CSS** added

So let's add some **CSS** 

For this create `Container.module.css` file and define  **CSS** and then import that inside the `Container.jsx` file
```JSX
import styles from "./Container.module.css";
const Container = (props) => {
  return <div className={styles.container}>{props.children}</div>
}
  
export default Container;
```


Or, we can also write like this **without using** the `prop` keyword
```JSX
import styles from "./Container.module.css";
const Container = ({children}) => {
  return <div className={styles.container}>{children}</div>
}
  
export default Container;
```


inside  `Container.module.css` file do some changes so that **CSS** will be visible
```CSS
.container {
  border: 1px solid black;
  margin: 5px;
  border-radius: 5px;
  width: 50%;
  min-width: 300px;
  padding: 15px;
}
```


see we have successfully linked the module **CSS** with the `Container.jsx` file
![[Pasted image 20241023091817.png]]




After **CSS** it will look like this
![[Pasted image 20241023092402.png]]


Now we can do one more thing i.e. can we move the `Healthy Foods heading` to center `Yes`

let's do some changes inside `App.css`
```CSS
.food-heading {
  background-color: grey;
  text-align: center; //This is new line
}
```



Now the page will look like this
![[Pasted image 20241023223655.png]]



Can we jus **add a new container** just *below the main container* 
`Yes`
Let's do some changes inside the `App.jsx`


> [!NOTE] Before
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
  
function App() {
  // let foodItems = [];
  let foodItems = ["Biryani", "Dal", "Vegetables", "Milk", "Apple"];
  
  return (
    <Container>
      <h1 className="food-heading">Healthy Foods</h1>
      <ErrorMessage items = {foodItems} />
      <FoodItems items = {foodItems} />
    </Container>
  );
}

export default App;
```




> [!NOTE] After
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";

function App() {
  // let foodItems = [];
  let foodItems = ["Biryani", "Dal", "Vegetables", "Milk", "Apple"];

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodItems items={foodItems} />
      </Container>
      <Container>
        <p>
          Above there is the list of healthy foods that are good for health and
          well being
        </p>
      </Container>
    </>
  );
}

export default App;
```



Now the page will look like this
![[Pasted image 20241023224443.png]]


![[Pasted image 20241023224601.png]]

1. **React** events use ***camelCase*** e.g. ***onClick***
2. **Uses synthetic events**, not direct browser events
3. **Event handlers** can be ***functions*** or ***arrow functions***
4. **Use onChange** for controlled form inputs
5. **Avoid inline arrow functions** in ***JSX for performance***

Let's take example of we took for the `Passing children lecture`

Same code same all just to start with 



![[Pasted image 20241023230149.png]]

So let's start the lecture

## Task 
we need to add some `buttons` side by side to `Buy` the products that we wrote in the `Healthy Foods list`

How can we add the `Buy` buttons besides the list items

So let's do some changes inside `Item.jsx`
```JSX
import styles from "./Item.module.css";
const Item = ({ foodItem }) => {
  return (
    <li className={`${styles["kg-item"]} list-group-item`}>
      <span className={styles["kg-span"]}>{foodItem}</span>
      <button>Buy</button>
    </li>
  );
};

export default Item;
```




Now it will look like this
![[Pasted image 20241023232606.png]]


then we need to add some **CSS** for proper visualization 
```CSS
.kg-item {
  background-color: khaki;
}

.kg-span {
  font-weight: 500;
  color: orangered;
}

  
// Newly added codes
.button {
  float: right;
}
```




Now it will look like this
![[Pasted image 20241023232601.png]]


## onClick
Let's make our `Buy buttons` functional using some `methods`

***For better understanding*** let's use `onClick method` here in our code

Let's do some changes inside the `Item.jsx` file
```JSX
import styles from "./Item.module.css";
const Item = ({ foodItem }) => {
  return (
    <li className={`${styles["kg-item"]} list-group-item`}>
      <span className={styles["kg-span"]}>{foodItem}</span>
      <button
        className={`${styles.button} btn btn-info`}
        onClick={() => console.log("Buy Button Clicked")}
      >
        Buy
      </button>
    </li>
  );
};
  
export default Item;
```


Let's check whether our `onClick method` is **working** or **not**
![[Pasted image 20241023233406.png]]

Yes it is working


Now we want to `print the items name` on clicking the `Buy button`
Let's do some changes inside `Item.jsx` file
```JSX
import styles from "./Item.module.css";

const Item = ({ foodItem }) => {
  return (
    <li className={`${styles["kg-item"]} list-group-item`}>
      <span className={styles["kg-span"]}>{foodItem}</span>
      <button
        className={`${styles.button} btn btn-info`}
        onClick={() => console.log(`${foodItem} is bought`)}
      >
        Buy
      </button>
    </li>
  );
};

export default Item;
```

Here we go ***Yes*** it is working
![[Pasted image 20241023233332.png]]



Make it more modular let's do some changes inside `Item.jsx` 
```JSX
import styles from "./Item.module.css";

const Item = ({ foodItem }) => {
  const handleBuyButtonClicked = (foodItem) => {
    console.log (`${foodItem} is bought`)
  }

  return (
    <li className={`${styles["kg-item"]} list-group-item`}>
      <span className={styles["kg-span"]}>{foodItem}</span>
      <button
        className={`${styles.button} btn btn-info`}
        onClick={() => handleBuyButtonClicked(foodItem)}
      >
        Buy
      </button>
    </li>
  );
};

export default Item;
```



Now we want to add the `input bar` below the heading `Healthy Foods`
so let's do some changes `to add input bar ` 

Let's create a file named `FoodInput.jsx` and do some changes and add it's corresponding `css module` as well and import inside this file as well

```JSX
import styles from "./FoodInput.module.css";

const FoodInput = () => {
  return (
    <input
      className={styles.foodInput}
      type="text"
      placeholder="Enter Items Here"
      )}
    />
  );
};

export default FoodInput;
```

and

go inside the `App.jsx` and import this component to apply the following changes

```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";

function App() {
  // let foodItems = [];
  let foodItems = ["Biryani", "Dal", "Vegetables", "Milk", "Apple"];

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        
        <FoodInput /> //New lines of code
        
        <FoodItems items={foodItems} />
      </Container>
      
      {/* <Container>
        <p>
          Above there is the list of healthy foods that are good for health and
          well being
        </p>
      </Container> */}
      
    </>
  );
}

export default App;
```

Now it will look like this
![[Pasted image 20241024011250.png]]

Add some **CSS** to make it look proper
```CSS
.foodInput {
    width: 100%;
    padding: 5px;
    margin: 10px 0px;
}
```

![[Pasted image 20241024011416.png]]




Now we want to understand `SyntheticBaseEvent` so implement something to see that or `add Event` and print to  see it so that later we can use that 

We are just printing the `event` in this and showcasing that actually this way we can use our events properly

Let's do some changes inside `Item.jsx` file
```JSX
import styles from "./Item.module.css";

const Item = ({ foodItem }) => {
  const handleBuyButtonClicked = (event) => {
    console.log(event)
    console.log (`${foodItem} is bought`)
  }

  return (
    <li className={`${styles["kg-item"]} list-group-item`}>
      <span className={styles["kg-span"]}>{foodItem}</span>
      <button
        className={`${styles.button} btn btn-info`}
        onClick={(event) => handleBuyButtonClicked (event)}
      >
        Buy
      </button>
    </li>
  );
};

export default Item;
```



Now when doing inspect it will return something like this in the console
![[Pasted image 20241023235700.png]]






## onChange


For Better understanding how `onChange` works let's take an example 


![[Pasted image 20241024000756.png]]




![[Pasted image 20241024002443.png]]


What are the changes it is needed to be done so that *if we enter something inside* the *input* bar it will *show every bit of that characters* in the console 


Let's create a file named `FoodInput.jsx` and do some changes and add it's corresponding `css module` as well and import inside this file as well

```JSX
import styles from "./FoodInput.module.css";

const FoodInput = () => {
  return (
    <input
      className={styles.foodInput}
      type="text"
      placeholder="Enter Items Here"
      onChange={(event) => console.log(event.target.value)}
    />
  );
};

export default FoodInput;
```



Make it more modular  inside `FoodInput.jsx`

```JSX
import styles from "./FoodInput.module.css";

const FoodInput = () => {
  const handleBuyButtonChange = (event) => {
    console.log(event.target.value)
  }

  return (
    <input
      className={styles.foodInput}
      type="text"
      placeholder="Enter Items Here"
      onChange={handleBuyButtonChange}
    />
  );
};

export default FoodInput;
```



Let's do some changes inside the file named `FoodInput.jsx` 
```JSX
import styles from "./FoodInput.module.css";

const FoodInput = () => {
  return (
    <input
      className={styles.foodInput}
      type="text"
      placeholder="Enter Items Here"
      onChange={(event) => console.log(event.target.value)}
    />
  );
};

export default FoodInput;
```



![[Pasted image 20241024002629.png]]






Now this is the `App.jsx` file will look like 
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";

function App() {
  // let foodItems = [];
  let foodItems = ["Biryani", "Dal", "Vegetables", "Milk", "Apple"];

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodInput />
        <FoodItems items={foodItems} />
      </Container>
      
      {/* <Container>
        <p>
          Above there is the list of healthy foods that are good for health and
          well being
        </p>
      </Container> */}
    </>
  );
}
  
export default App;
```

and the output also came this way

![[Pasted image 20241024002609.png]]



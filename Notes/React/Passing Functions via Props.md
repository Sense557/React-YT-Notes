
![[Pasted image 20241024003638.png]]


1. **Pass** dynamic **behavior** between components
2. **Enables** upward communication from **child to component**
3. **Commonly used** for **event handling**
4. **Parent** defines a function, **child invokes it**
5. **Enhances** component **interactivity**
6. ***Example***
		`< Button onClick = {handleClick} />`



For understanding this project very well let's take the example of previous concept `Handling Events`

Just to start with 


Let's do some changes inside `FormInput.jsx` 


> [!NOTE] Before
```JSX
import styles from "./FoodInput.module.css";

const FoodInput = () => {
  const handleOnChange = () => {
    console.log(event.target.value);
  };
  return (
    <input
      className={styles.foodInput}
      type="text"
      placeholder="Enter Items Here"
      
      onChange={(event) => handleOnChange}
    />
  );
};

export default FoodInput;
```

Now it will behave like this
![[Pasted image 20241024092440.png]]

To make it more modular do some changes
> [!NOTE] After
```JSX
import styles from "./FoodInput.module.css";

const FoodInput = (handleOnChange) => {
  return (
    <input
      className={styles.foodInput}
      type="text"
      placeholder="Enter Items Here"
      
      onChange={handleOnChange}
    />
  );
};

export default FoodInput;
```

with using `props` keyword
```
import styles from "./FoodInput.module.css";

const FoodInput = (props) => {
  return (
    <input
      className={styles.foodInput}
      type="text"
      placeholder="Enter Items Here"

      onChange={props.handleOnChange}
    />
  );
};

export default FoodInput;
```

without using `props` keyword
```
import styles from "./FoodInput.module.css";

const FoodInput = ({handleOnChange}) => {
  return (
    <input
      className={styles.foodInput}
      type="text"
      placeholder="Enter Items Here"

      onChange={handleOnChange}
    />
  );
};

export default FoodInput;
```


Now after removing the `handleOnChange` we need to define it inside `App.jsx` as parent should handle the child behaviour 

Actually we should neve give access the child for it's behaviour we should give the control of child's behaviour to the parent so that it will be easy to handle. What is fetching the data should handle the behaviour as well. It is believed that the behaviour should always be handled by parent else all the logic will be disturbed in bigger scale

So we are going to define it inside `App.jsx` and pass it to the `<FormInput />` so that it's behaviour will remain as it was
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

//New lines of code
  const handleOnChange = (event) => {
    console.log (event.target.value);
  };
  
  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodInput handleOnChange={handleOnChange}/>
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


Now see we have achieved the previous as it was 
![[Pasted image 20241024092212.png]]



Now the task is  How can we display the entered data changes in inside our app not inside the console

So let's do this

Go to `App.jsx` do some changes
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

  let textToShow = "Food items entered by User"
  const handleOnChange = (event) => {
    console.log (event.target.value);
    textToShow = (event.target.value);
  }

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodInput handleOnChange={handleOnChange}/>
        <p>{textToShow}</p>
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

but not happened as expected it happened the same as previous
so let's find out what we are missing

![[Pasted image 20241024092212.png]]



So the problem is as the value inside `App.jsx` is painted once but not updating after the changes so this is the problem of state

i.e. it means it is `stateless` I mean to say it is painting the state once after changes it is unable to update that changes inside our app

So we need a solution i.e. `State Management`



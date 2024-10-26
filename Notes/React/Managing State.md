
![[Pasted image 20241024094445.png]]


1. **State** represents ***data that changes*** over time
2. **State** is ***local*** and ***private*** to the component
3. **State** changes cause the component to **re-render**
4. **For** functional components, use the ***useState*** hook
5. **React** functions that start with word ***use*** are called ***hooks***
6. **Hooks** should ***only*** be used ***inside components***
7. **parent** components can ***pass state down to children via props***
8. **Lifting state up:** share state between companies by moving it ***to their closest common ancestor***


Here the issue is
If we enter a value inside input bar it should reflect in the highlighted portion down there so what should we do to reflect that changes whenever we are entering the values inside input bar

So we need a solution i.e. `State Management`

![[Pasted image 20241025220857.png]]

Let's solve the issue

It is the first stage of our problem after what is being entered by used nothing is being changes excluding `console`


Let's do some changes
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
    textToShow = event.target.value;
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


![[Pasted image 20241025225507.png]]





Now here something is changing in the console

Let's do some changes

```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";
// import { useState } from "react";

function App() {
  // let foodItems = [];
  let foodItems = ["Biryani", "Dal", "Vegetables", "Milk", "Apple"];

  let textStateArr = useState("Foods entered by user");
  let textToShow = textStateArr[0];
  let setTextState = textStateArr[1];

  console.log (`Current text state value: ${textToShow}`);
  const handleOnChange = (event) => {
    console.log (event.target.value);
    textToShow = event.target.value;
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




![[Pasted image 20241025232128.png]]








Yes now we have achieved what we wanted

Here is the code changes we did inside `App.jsx`
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";

function App() {
  // let foodItems = [];

  let foodItems = ["Biryani", "Dal", "Vegetables", "Milk", "Apple"];
  let textStateArr = useState("Foods entered by user");
  let textToShow = textStateArr[0];
  let setTextState = textStateArr[1];

  console.log (`Current text state value: ${textToShow}`);
  
  const handleOnChange = (event) => {
    console.log (event.target.value);
    setTextState (event.target.value);
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







![[Pasted image 20241025225246.png]]



or we can do something to make it more modular
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";
  
function App() {
  // let foodItems = [];

  let foodItems = ["Biryani", "Dal", "Vegetables", "Milk", "Apple"];

  let textStateArr = useState("Food items entered by User");
  let [textToShow, setTextState] = useState("Food items entered by User");
  console.log(`Current value of textState: ${textToShow}`);

  const handleOnChange = (event) => {
    console.log (event.target.value);
    setTextState  (event.target.value);
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




Let's do some changes and remove `FoodInput` bar 
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";

function App() {
  let [textToShow, setTextState] = useState();
  let [foodItems, setFoodItems] = useState([
    "Biryani",
    "Dal",
    "Vegetables"
  ]);

  let textStateArr = useState("Food items entered by User");

  console.log(`Current value of textState: ${textToShow}`);
  
  const handleOnChange = (event) => {
    console.log(event.target.value);
    setTextState(event.target.value);
  };

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodInput handleOnChange={handleOnChange} />
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


now this will look like this
![[Pasted image 20241026001905.png]]



Now we are going to implement the `enter` button
Let's go inside the `FoodInput.jsx` & do some changes

```JSX
import styles from "./FoodInput.module.css";

const FoodInput = ({handleKeyDown}) => {

  return (
    <input
      className={styles.foodInput}
      type="text"
      placeholder="Enter Items Here"

      onKeyDown={handleKeyDown}
    />
  );
};
  
export default FoodInput;
```


then do some changes inside `App.jsx` to reflect that changes
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";
  
function App() {
  let [textToShow, setTextState] = useState();

  let [foodItems, setFoodItems] = useState([
    "Biryani",
    "Dal",
    "Vegetables"
  ]);

  let textStateArr = useState("Food items entered by User");
  console.log(`Current value of textState: ${textToShow}`);

  const onKeyDown = (event) => {
    console.log(event.target.value);
    setTextState(event.target.value);
  };

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodInput handleKeyDown={onKeyDown} />
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

![[Pasted image 20241026003255.png]]

But here the problem is when we have entered or not we are not getting any indication so we are not aware that `Enter` is pressed or not




```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";
  
function App() {
  let [textToShow, setTextState] = useState();

  let [foodItems, setFoodItems] = useState([
    "Biryani",
    "Dal",
    "Vegetables"
  ]);

  let textStateArr = useState("Food items entered by User");
  console.log(`Current value of textState: ${textToShow}`);

  const onKeyDown = (event) => {
    console.log(event);
    setTextState(event.target.value);
  };

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodInput handleKeyDown={onKeyDown} />
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

![[Pasted image 20241026003539.png]]

On the above we are printing the synthetic events so that we can guess what to do next to implement the `Enter` key properly

Let's go deep down into the events


![[Pasted image 20241026004256.png]]



Now here we can see that a is pressed which is logged inside the key = `a` which is visible inside synthetic events


Now after knowing about the synthetic events we can properly implement the working of `Enter` key

```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";

function App() {
  let [textToShow, setTextState] = useState();

  let [foodItems, setFoodItems] = useState([
    "Biryani",
    "Dal",
    "Vegetables"
  ]);

  let textStateArr = useState("Food items entered by User");
  console.log(`Current value of textState: ${textToShow}`);

  const onKeyDown = (event) => {
    if(event.key === "Enter"){
      let newFoodItem = event.target.value;
      console.log("Food Value Entered is" + newFoodItem);
    }
  };
  
  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodInput handleKeyDown={onKeyDown} />
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





![[Pasted image 20241026005835.png]]


But there is a problem here after entering the user entered value should get added inside the list

```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";

function App() {
  let [foodItems, setFoodItems] = useState([
    "Biryani",
    "Dal",
    "Vegetables"
  ]);

  let textStateArr = useState("Food items entered by User");

  const onKeyDown = (event) => {
    if(event.key === "Enter"){
      let newFoodItem = event.target.value;
      let newItems = [...foodItems, newFoodItem];
      setFoodItems(newItems);
    }
  };

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodInput handleKeyDown={onKeyDown} />
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


![[Pasted image 20241026012014.png]]



But now we need to add the feature that after entry it should be blank
Let's do some changes
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";

function App() {
  let [foodItems, setFoodItems] = useState([
    "Biryani",
    "Dal",
    "Vegetables"
  ]);

  let textStateArr = useState("Food items entered by User");

  const onKeyDown = (event) => {
    if(event.key === "Enter"){
      let newFoodItem = event.target.value;
      let newItems = [...foodItems, newFoodItem];
      setFoodItems(newItems);
      event.target.value = "";
    }
  };

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <ErrorMessage items={foodItems} />
        <FoodInput handleKeyDown={onKeyDown} />
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






Now the task is to achieve it anyway
![[Pasted image 20241026083441.png]]
Here the code changes we need to do
```JSX
import FoodItems from "./components/FoodItems";
import ErrorMessage from "./components/ErrorMessage";
import React, { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
import "./App.css";
import Container from "./components/Container";
import FoodInput from "./components/FoodInput";

function App() {
  let [foodItems, setFoodItems] = useState([]);
  let textStateArr = useState("Food items entered by User");

  const onKeyDown = (event) => {
    if(event.key === "Enter"){
      let newFoodItem = event.target.value;
      let newItems = [...foodItems, newFoodItem];
      setFoodItems(newItems);
      event.target.value = "";
    }
  };

  return (
    <>
      <Container>
        <h1 className="food-heading">Healthy Foods</h1>
        <FoodInput handleKeyDown={onKeyDown} />
        <ErrorMessage items={foodItems} />
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


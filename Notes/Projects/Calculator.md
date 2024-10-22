
![[Pasted image 20241022212856.png]]



> [!NOTE] Prerequisites
> >React (Vite Project) + JS
> Bootstrap


**Let's Start Our Project**

Create a folder `Projects`

Create Vite Project using this command `npm create vite@latest`

Project Name : `4-calculator-version-one`

Select a framework : `React`

Select a variant : `JavaScript`

then run this command one after another
```
  cd 4-calculator-version-one
  npm install
  npm run dev
```

Now our vite project is **Ready**

Now let's install Bootstrap using this command  `npm i bootstrap@5.3.3`

Import Bootstrap inside `Main.jsx` file  using the below line of code
```
import 'bootstrap/dist/css/bootstrap.min.css'
```


Now run the server using this command  `npm run dev`

the page will look like this

![[Pasted image 20241020130126.png]]


Now let's do some **Cleanup** work
- delete `index.css`
- clear `App.css`
- clear `App.jsx` 
- clear `main.jsx`

now do some changes in `App.jsx`
```JSX
import React from "react"
function App() {
  return (
    <> </>
  )
}
  
export default App
```


now do some changes inside `main.jsx`
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



Now everything is **all set**

Let's start our project ***Calculator***

Before that let's convert the `App.css` to `App.module.css` by *renaming* to modularize so that no need to edit at last
then import that `App.module.css` inside `App.jsx`

Let's do some changes inside `App.jsx`
```JSX
import React from "react"
import styles from "./App.module.css"

function App() {
  return (
    <div id="calculator">
      <input id="display" type="text" />
      <div id="buttons-container">
        <button>C</button>
        <button>C</button>
        <button>C</button>
        <button>C</button>
      </div>
    </div>
  )
}

export default App;
```


Why not directly we inject **CSS** Module inside `App.jsx` i.e. let's do some changes like this 
```JSX
import React from "react";
import styles from "./App.module.css";

function App() {
  return (
    <div className={styles.calculator}>
      <input id="display" type="text" />
      <div id="buttons-container">
        <button>C</button>
        <button>1</button>
        <button>2</button>
        <button>+</button>
      </div>
    </div>
  );
}

export default App;
```


do some changes inside `App.module.css` to ensure that the **CSS** module is attached properly
```CSS
.calculator {
  background-color: yellow;
}
```


Yes, this is the changes we wanted to see 
It is working great
![[Pasted image 20241022220619.png]]


Now add some **CSS** to give it a normal `Calculator` look
do some changes inside `App.module.css` 
```CSS
.calculator {
  border: 1px solid rgba(163, 153, 153);
  width: 200px;
  border-radius: 5px;
}

.display {
  margin: 10px;
  font-size: 25px;
  width: 175px;
}
  
.buttonContainer {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
  
.button {
  width: 45px;
  height: 45px;
  margin: 3px;
}
```

Inside `App.module.css` use the **camelCase** format

and do some changes inside `App.jsx` to import the changes we made inside `App.module.jsx` file
```JSX
import React from "react";
import styles from "./App.module.css";

function App() {
  return (
    <div className={styles.calculator}>
      <input className={styles.display} type="text" />
      <div className={styles.buttonContainer}>
        <button className={styles.button}>C</button>
        <button className={styles.button}>1</button>
        <button className={styles.button}>2</button>
        <button className={styles.button}>+</button>
      </div>
    </div>
  );
}

export default App;
```



Now Calculator UI looks like this
![[Pasted image 20241022223517.png]]


### Display.jsx

Let's Modularize the **CSS** and the codes present inside `App.jsx` file also 

create a folder called `components` inside which we will create our `components`

let's create `Display.jsx` file  and do some changes i.e. copy the code from `App.jsx` 
```JSX
const Display = () => {
  return <input className={styles.display} type="text" />;
};

export default Display;
```

### Display.module.css

let's create `Display.module.css` file and do some changes
```CSS
.display {
  margin: 10px;
  font-size: 25px;
  width: 175px;
}
```

Use **camelCase** Formatting inside `module.css` file

after that import `Display` inside `Display.jsx` file
```JSX
import styles from "./Display.module.css"

const Display = () => {
  return <input className={styles.display} type="text" />;
};

export default Display;
```


Then **import** Display component inside the `App.jsx`  and then it looks like this
```JSX
import React from "react";
import styles from "./App.module.css";
import Display from "./components/Display";

function App() {
  return (
    <div className={styles.calculator}>
      <Display />
        <div className={styles.buttonContainer}>
        <button className={styles.button}>C</button>
        <button className={styles.button}>1</button>
        <button className={styles.button}>2</button>
        <button className={styles.button}>+</button>
      </div>
    </div>
  );
}

export default App;
```



### ButtonsContainer.jsx
then let's modularize the `Buttons container` 

let's create a file `ButtonsContainer.jsx` file inside which we will copy the whole section of the Button from the file `App.jsx` and paste it there 

let's do some changes
```JSX
const ButtonsContainer = () => {
  return (
    <div className={styles.buttonContainer}>
      <button className={styles.button}>C</button>
      <button className={styles.button}>1</button>
      <button className={styles.button}>2</button>
      <button className={styles.button}>+</button>
    </div>
  );
};
  
export default ButtonsContainer;
```


### ButtonsContainer.module.css
let's create `ButtonsContainer.module.css` file inside which we are going to keep button sections **CSS** to modularize it 

we are going to copy that code from the `App.css` and going to paste it here

let's do some changes
```CSS
.buttonContainer {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.button {
  width: 45px;
  height: 45px;
  margin: 3px;
}
```


after pasting `import` this module inside the `ButtonsContainer.jsx`
let's do some changes
```JSX
import styles from "./ButtonsContainer.module.css"

const ButtonsContainer = () => {
  return (
    <div className={styles.buttonContainer}>
      <button className={styles.button}>C</button>
      <button className={styles.button}>1</button>
      <button className={styles.button}>2</button>
      <button className={styles.button}>+</button>
    </div>
  );
};

export default ButtonsContainer;
```


If you see we have done nothing more than adjusting the **CSS** here so we need to do more thing for this `ButtonsContainer.jsx` file 

using `map method` we can map the *buttons* of the calculator 

let's do some changes inside `ButtonsContainer.jsx` file
```JSX
import styles from "./ButtonsContainer.module.css";

const ButtonsContainer = () => {
  const buttonNames = [
    "C",
    "1",
    "2",
    "+",
    "3",
    "4",
    "-",
    "5",
    "6",
    "*",
    "7",
    "8",
    "/",
    "=",
    "9",
    "0",
    ".",
  ];

  return (
    <div className={styles.buttonContainer}>
      {buttonNames.map((buttonName) => (
        <button className={styles.button}>{buttonName}</button>
      ))}
    </div>
  );
};

export default ButtonsContainer;
```


Now the UI will look like this
![[Pasted image 20241022235156.png]]
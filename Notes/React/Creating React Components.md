10. File Extensions
11. Class Vs Functional components
12. What is JSX 
13. Exporting component
14. Other Important points
15. Dynamic Components
16. Reusable Components


## File Extensions
.JS
- Stands for JavaScript
- Contains regular JavaScript Code
- Used for general logic and components

.JSX
-  Stands for JavaScript XML
- Combine JavaScript with HTML-like tags
- Makes it easier to design UI components


## Class vs Functional components
#### Class Components
- *Stateful :* Can manage state
- *Lifecycle :* Access to lifecycle methods
- *Verbose :* More boilerplate code
- Not preferred anymore

#### Functional Components
- Initially *stateless* 
- *Can use hooks* for state & effects
- *Simpler and more concise*
- More Popular


## What is JSX
1. *Definition :* JSX determines how UI will look whenever the component is used 
2. *Not HTML :* Though it *resembles HTML*, You're actually writing JSX, which stands for JavaScript XML
3. *Conversion :* *JSX gets converted to regular JavaScript*
4. Babeljs.io/repel is a tool that allows you to see how *JSX is transformed into JavaScript*


## Exporting Components 
1. **Enables** the use of components in *other parts*
2. **Default Export :** *Allows exporting a single component* as the default from a nodule
3. **Named Export :** Allows *exporting multiple times* from a module
4. **Importing :** To use an exported component you need to *import it in the destination file* using import syntax


## Step by Step guide

Create `KgButton.jsx`
```JSX
function KgButton () {
  return <button>Like this Video</button>
}

export default KgButton;
```

Now tell me where is the button as after creating the `KgButton` still it is *not visible in our app page* ?
- As it is not being used anywhere *only created*

So to use it what should I do ?
- Go to `App.jsx` file and do some changes
```JSX
function App(){
  return <h1>My Name is Shakti</h1>
}

export default App;
```
- Previously this was it now do some changes

```JSX
function App(){
  return (
    <div>
      <h1>My Name is Shakti</h1>
      <button>Subscribe</button>
    </div>
  );
}

export default App;
```
After these changes the button became visible

![[{CAC20AB9-A713-4840-92DD-866ACEA9B84A}.png]]

Now do some changes again in `App.jsx`  file so that we can use our created `KgButton` here in `App.jsx`

```JSX
function App(){
  return (
    <div>
      <h1>My Name is Shakti</h1>
      <KgButton></KgButton>
    </div>
  );
}

export default App;
```

But after doing this all page went blank ? What happened ?

![[Pasted image 20241019223013.png]]

So, we need to do *import* the component else our component will not work here in `App.jsx` file.

So, let's do some changes

```JSX
import KgButton from "./KgButton";

function App(){
  return (
    <div>
      <h1>My Name is Shakti</h1>
      <KgButton></KgButton>
    </div>
  );
}

export default App;

```

After `import` *save* the file `App.jsx` then it will start rendering in the webpage like this

![[Pasted image 20241019223638.png]]


---
## Note

> [!Warning] Old Method Export Vs New Method Export
```JSX
//Old Method
function KgButton () {
  return <button>Like this Video</button>
}

export default KgButton;
```

```JSX
//New Method
export default function KgButton () {
  return <button>Like this Video</button>
}
```

But `new Method` is *not acceptable* everywhere. So, It is recommended to use the `old method`

---
## Note 

> [!IMPORTANT] Multiple Named Export
```JSX
//Inside a Single file Component

export function 
SideBar () { 
	... 
}

export function 
CheckBox () { 
	... 
}
```

It is not recommended to create multiple component inside a single component file and export like in the above code snippet


---
## Note
> [!NOTE] Named Export
> If you are doing `export`  components this way like this from `KgButton.jsx` file
> 
> ```JSX
> export function KgButton () {
  return <button>Like this Video</button>
}
> ```
> then you need to import like this in `App.jsx` file
```JSX
import {KgButton} from "./KgButton";

function App(){
  return (
    <div>
      <h1>My Name is Shakti</h1>
      <KgButton></KgButton>
    </div>
  );
}
export default App;
```

It means you need to keep the component inside `curly braces` while doing named export

---
## Note

> [!NOTE] Named Export & One Default Export
> ```
> export function 
> Avatar () {
> 	...
> }
> 
> export default function
> FriendsList(){
> 	...
> }
> ```

---


## Other Important Points
1. **Naming :** *Must be capitalized* lowercase for default HTML
2. **HTML :** Unlike Vanilla JS where you can't directly write HTML, in React *you can embed HTML-like syntax using JSX*
3. **CSS :** In React, *CSS can be directly imported into component files*, allowing for modular and component specific styling


## Dynamic Components
1. **Dynamic  Content:** *JSX allows* the creation of *dynamic* and interactive UI components
2. **JavaScript Expressions:** Using *{}*, we can *embed any JS expression directly within JSX*, this includes variables function-calls and more


## Example
let's create `Hello.jsx` file i.e. Component

```JSX
function Hello () {
  return (
    <h3>Hello, This is the future speaking;</h3>
  );
}

export default Hello;
```

import it inside the `App.jsx` file

```JSX
// import {KgButton} from "./KgButton";

import Hello from "./Hello";

function App(){
  return (
    <div>
      <h1>My Name is Shakti</h1>
      <Hello></Hello>
    </div>
  );
}

export default App;
```

``` JSX
function Hello () {
  let myName = "Shakti";
  let fullName = () => {
    return "Shakti Meher";
  }
  let number = 456;

  return (
    <p>Message:{number} I am {myName} and my full name is {fullName()} </p>
  );
}

export default Hello;
```


## Reusable Components
1. **Modularity :** Components are modular allowing for *easy reuse across different parts* of an application
2. **Consistency:** Reusing components ensures *UI consistency* and reduces the chance of discrepancies 
3. **Efficiency:** Reduces development time and effort by *avoiding duplication of code*
4. **Maintainability:** *Changes* made to a reused component *reflect everywhere* it's used, simplifying updates and bug fixes


## Example
Create a file `Random.jsx` 
```JSX
function Random () {
  let number = Math.random()*10;
  return (
    <h1>Random Number is: {number}</h1>
  );
}

export default Random;
```

and import inside `App.jsx`  Else it will not work so keep that in mind
```JSX
// import {KgButton} from "./KgButton";

import Hello from "./Hello";
import Random from "./Random"

function App(){
  return (
    <div>
      <h1>My Name is Shakti</h1>
      <Hello></Hello>
      <Random></Random>
    </div>
  );
}

export default App;
```

Now the page looks like this
![[Pasted image 20241020090546.png]]

Now the task to **achieve the round number** How to achieve that
let's do some changes in `Random.jsx` file

```JSX
function Random () {
  let number = Math.random()*10;
  return (
    <h1>Random Number is: {Math.round(number)}</h1>
  );
}
  
export default Random;
```

Now the page looks like this
![[Pasted image 20241020090844.png]]

Now the task to achieve **multiple Random Number should display** on this page How to do that ?

let's do some changes inside `App.jsx` file
```JSX
// import {KgButton} from "./KgButton";

import Hello from "./Hello";
import Random from "./Random"

function App(){
  return (
    <div>
      <h1>My Name is Shakti</h1>
      <Hello></Hello>
      <Random></Random>
      <Random></Random>
      <Random></Random>
      <Random></Random>
      <Random></Random>
    </div>
  );
}

export default App;
```

Now the page look like this
![[Pasted image 20241020091210.png]]


Now the task to `set background color` How to do that ?
```JSX
function Random () {
  let number = Math.random()*100;
  return (
    <h1 style={{'background-color': '#776690'}}>Random Number is: {Math.round(number)}</h1>
  );
}

export default Random;
```

Now page will look like this
![[Pasted image 20241020105923.png]]

---

> [!Warning] Note
> If you are importing a component remember you should use open and close format else use self closing format
> 
> **Example-**
```JSX
<Hello/>

//OR

<Hello></Hello>
```


## Creating React Components Revision
10. File Extensions
11. Class Vs Functional components
12. What is JSX 
13. Exporting component
14. Other Important points
15. Dynamic Components
16. Reusable Components


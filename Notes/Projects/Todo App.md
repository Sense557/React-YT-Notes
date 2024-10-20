 
> [!NOTE] Prerequisites
> >React (Vite Project) + JS
> Bootstrap


**Let's Start Our Project**

Create a folder `Projects`

Create Vite Project using this command `npm create vite@latest`

Project Name : `1-todo-app-version-one`

Select a framework : `React`

Select a variant : `JavaScript`

then run this command one after another
```
  cd 1-todo-app-version-one
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
- delete `App.css`
- clear `App.jsx`

Do some changes inside `App.jsx`
```JSX
function App (){
  return <center>TODO App</center>
}

export default App;
```

Why this `center` tag -> Because we want everything in the center



Now the page looks like this
![[Pasted image 20241020131810.png]]

Now add some buttons and input tags to match that **UI** we are working for
```JSX
function App() {
  return (
    <center class="todo-container">
      <h1>TODO App</h1>
      <div class="container text-center">
        <div class="row">
          <div class="col-6"><input type="text" placeholder="Enter Text Here" /></div>
          <div class="col-4"><input type="date" /></div>
          <div class="col-2"><button type="button" class="btn btn-success">Add</button></div>
        </div>

        <div class="row">
          <div class="col-6">Buy Milk</div>
          <div class="col-4">04/10/2023</div>
          <div class="col-2"><button type="button" class="btn btn-danger">Danger</button></div>
        </div>
        
        <div class="row">
          <div class="col-6">Go To College</div>
          <div class="col-4">04/10/2023</div>
          <div class="col-2"><button type="button" class="btn btn-danger">Danger</button></div>
        </div>
      </div>
    </center>
  );
}

export default App;
```

Now Page will look like this
![[Pasted image 20241020183011.png]]


Ok see this is it But the thing is we have *hard-coded* all the JSX part i.e. *not modular*.

So to make the components modular we need to do some changes *to make our components modular*

Now if we look our UI in more detail then we can see that it has *3 major sections*
1. App Name Section
2. Add Section
3. Delete Section

So, *let's create components*

## AppName 

==Let's go for **AppName Component**==

Create a folder named **components** inside **src** folder and
Create a file named **AppName.jsx** inside **components** folder i.e. Folder structure look like this .`src/components/AppName.jsx`

Inside `AppName.jsx` do some changes and export it
```JSX
function AppName (){
  return <h1>Todo React App</h1>
}

export default AppName;
```



Inside `App.jsx` do some changes as we have to import the `<AppName />` component inside `App.jsx` else it will not work 
```JSX
import AppName from "./components/AppName";

function App() {
  return (
    <center class="todo-container">
    
      <AppName />
      
      <div class="container text-center">
        <div class="row">
          <div class="col-6"><input type="text" placeholder="Enter Text Here" /></div>
          <div class="col-4"><input type="date" /></div>
          <div class="col-2"><button type="button" class="btn btn-success">Add</button></div>
        </div>

        <div class="row">
          <div class="col-6">Buy Milk</div>
          <div class="col-4">04/10/2023</div>
          <div class="col-2"><button type="button" class="btn btn-danger">Danger</button></div>
        </div>

        <div class="row">
          <div class="col-6">Go To College</div>
          <div class="col-4">04/10/2023</div>
          <div class="col-2"><button type="button" class="btn btn-danger">Danger</button></div>
        </div>
      </div>
    </center>
  );
}

export default App;
```



## AddTodo Component

==Let's go for **AppTodo Component==

Create a file named `AddTodo.jsx` inside **components** folder 

Do some necessary changes
```JSX
function AddTodo (){

  return (
    <div class="container text-center">
      <div class="row">
        <div class="col-6"><input type="text" placeholder="Enter Text Here" /></div>
        <div class="col-4"><input type="date" /></div>
        <div class="col-2"><button type="button" class="btn btn-success">Add</button></div>
      </div>
    </div>
  );
}

export default AddTodo;
```


What just we did here we just copied that *Add Section* part from the `App.jsx` and make another component `AddTodo.jsx` inside which we pasted that section code **simple**

After which we exported and imported that inside `App.jsx` file else it will not work

so let's do changes inside `App.jsx`
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";

function App() {
  return (
    <center class="todo-container">
      <AppName />
      <AddTodo />

      <div class="container text-center">
        <div class="row">
          <div class="col-6">Buy Milk</div>
          <div class="col-4">04/10/2023</div>
          <div class="col-2"><button type="button" class="btn btn-danger">Danger</button></div>
        </div>
        
        <div class="row">
          <div class="col-6">Go To College</div>
          <div class="col-4">04/10/2023</div>
          <div class="col-2"><button type="button" class="btn btn-danger">Danger</button></div>
        </div>
      </div>
    </center>
  );
}

export default App;
```


## TodoItem1

==Let's go for **TodoItem1 Component**==

Create a file named `TodoItem1.jsx` inside **components** folder 

Do some changes
```JSX
function TodoItem1 () {

  let todoName = 'Buy Milk';
  let todoDate = '04/10/2023';
  return (
    <div class="container text-center">
      <div class="row">
        <div class="col-6">{todoName}</div>
        <div class="col-4">{todoDate}</div>
        <div class="col-2"><button type="button" class="btn btn-danger">Danger</button></div>
      </div>
    </div>
  );
}

export default TodoItem1;
```


What just we did here we just copied that *TodoItem Section / Delete Section* part from the `App.jsx` and make another component `TodoItem1.jsx` inside which we pasted that section code **simple**

And here we have created some variables like `todoName` & `todoDate` so that we don't have to hard-code the variable but we can do much more dynamic thing but till not we learned this much

so after creating the variable we are **using as placeholder** in their places **to make dynamic** where we wanted our data to be placed

After which we exported and imported that inside `App.jsx` file else it will not work

so let's do changes inside `App.jsx`

```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItem1 from "./components/TodoItem";

function App() {
  return (
    <center class="todo-container">
      <AppName />
      <AddTodo />
      <TodoItem1 />
      
      <div class="container text-center">
        <div class="row">
          <div class="col-6">Go To College</div>
          <div class="col-4">04/10/2023</div>
          <div class="col-2"><button type="button" class="btn btn-danger">Danger</button></div>
        </div>
      </div>
    </center>
  );
}

export default App;
```



## TodoItem2

==Let's go for **TodoItem2 Component**==

Create a file named `TodoItem2.jsx` inside **components** folder 

Do some changes
```JSX
function TodoItem2 () {

  let todoName = 'Go to College';
  let todoDate = '04/10/2023';
  return (
    <div class="container text-center">
      <div class="row">
        <div class="col-6">{todoName}</div>
        <div class="col-4">{todoDate}</div>
        <div class="col-2"><button type="button" class="btn btn-danger">Danger</button></div>
      </div>
    </div>
  );
}

export default TodoItem1;
```


What just we did here we just copied that *TodoItem Section / Delete Section* part from the `App.jsx` and make another component `TodoItem2.jsx` inside which we pasted that section code **simple**

And here we have created some variables like `todoName` & `todoDate` so that we don't have to hard-code the variable but we can do much more dynamic thing but till not we learned this much

so after creating the variable we are **using as placeholder** in their places **to make dynamic** where we wanted our data to be placed

After which we exported and imported that inside `App.jsx` file else it will not work

so let's do changes inside `App.jsx`

```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItem1 from "./components/TodoItem1";
import TodoItem2 from "./components/TodoItem2";

function App() {
  return (
    <center class="todo-container">
      <AppName />
      <AddTodo />
      <TodoItem1 />
      <TodoItem2 />
    </center>
  );
}

export default App;
```


## Add Some CSS
To make the App UI look good we are going to add some **CSS**

First create a file named `Index.css`

import it inside `App.jsx` like this
```JSX
import "./Index.css";
```

Let's start adding **CSS**
```JSX
/* .todo-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* min-height: 100vh; This will center it vertically */
} */

  
.todo-container h1 {
  font-size: 45px;
  font-weight: 700;
  margin: 10px;
  margin-bottom: 25px;
}

input {
  width: 100%;
}
```

But when we are going to add some css using in the button sections it is not happening so we are adding some `class` i.e. `item-container` ,  `kg-button` & `kg-row`

`item-container` - inside which all `item1` & `item2` will be present 
`kg-row` - *in the row*
`kg-button` -  *in the button* 

Let's add these classes in their respective places so that we can add **CSS**

#### App.jsx
do some changes
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItem1 from "./components/TodoItem1";
import TodoItem2 from "./components/TodoItem2";
import "./Index.css";
  
function App() {
  return (
    <center className="todo-container">
      <AppName />
      <AddTodo />
      <div className="items-container">
        <TodoItem1 />
        <TodoItem2 />
      </div>
    </center>
  );
}
  
export default App;
```


#### AddTodo.jsx
Let's do some changes
```JSX
function AddTodo (){
  return (
    <div class="container">
      <div class="row kg-row">
        <div class="col-6"><input type="text" placeholder="Enter Text Here" /></div>
        <div class="col-4"><input type="date" /></div>
        <div class="col-2"><button type="button" class="btn btn-success kg-button">Add</button></div>
      </div>
    </div>
  );
}

export default AddTodo;
```


#### TodoItem1
Let's do some changes
```JSX
function TodoItem1 () {
  let todoName = 'Buy Milk';
  let todoDate = '04/10/2023';

  return (
    <div class="container">
      <div class="row kg-row">
        <div class="col-6">{todoName}</div>
        <div class="col-4">{todoDate}</div>
        <div class="col-2"><button type="button" class="btn btn-danger kg-button">Danger</button></div>
      </div>
    </div>
  );
}

export default TodoItem1;
```



#### TodoItem2
Let's do some changes
```JSX
function TodoItem1 () {
  let todoName = 'Go to College';
  let todoDate = '04/10/2023';
  
  return (
    <div class="container">
      <div class="row kg-row">
        <div class="col-6">{todoName}</div>
        <div class="col-4">{todoDate}</div>
        <div class="col-2"><button type="button" class="btn btn-danger kg-button">Danger</button></div>
      </div>
    </div>
  );
}

export default TodoItem1;
```


#### Index.css
Let's add some **CSS**  to the classes after adding some classes 
```CSS
/* .todo-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* min-height: 100vh; This will center it vertically */
} */

.todo-container h1 {
  font-size: 45px;
  font-weight: 700;
  margin: 10px;
  margin-bottom: 25px;
}

input {
  width: 100%;
}
  
.items-container {
  text-align: left;
}

.kg-button {
  min-width: 80px;
}

.kg-row {
  margin: 10px 5px;
}
```

Now the page look like this after adding some CSS properties
![[Pasted image 20241020211051.png]]

---







![[Pasted image 20241020130815.png]]



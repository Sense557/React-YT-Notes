![[Pasted image 20241020130815.png]]


Here in the `1-todo-app-version-one` we have made some mistakes. Let's figure it out and ***try to resolve that issues***

In this project `1-todo-app-version-one` we have made **`TodoItem1.jsx`** & **`TodoItem2.jsx`** file inside `component` folder

So we need to do some **cleanup** there and we have *hard-coded* the values so need to do something for that also


#### TodoItem.jsx
First we need to **create** and copied the data of `TodoItem1.jsx` to `TodoItem.jsx`
Inside `TodoItem.jsx` do some changes

#Before 
```JSX
function TodoItem () {
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

export default TodoItem;
```

Now using the `De-Structuring Method` we can do some changes like ***passing the date via props*** 

See the changes we made

#After
```JSX
function TodoItem({ todoName, todoDate }) {
  return (
    <div class="container">
      <div class="row kg-row">
        <div class="col-6">{todoName}</div>
        <div class="col-4">{todoDate}</div>
        <div class="col-2">
          <button type="button" class="btn btn-danger kg-button">
            Danger
          </button>
        </div>
      </div>
    </div>
  );
}

export default TodoItem;
```


After changes we need to **import** that `Item.jsx` in the `App.jsx` and pass the ***data via props***

do some change
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItem from "./components/TodoItem";
import "./Index.css";
  
function App() {
  return (
    <center className="todo-container">
      <AppName />
      <AddTodo />
      <div className="items-container">
        <TodoItem todoName="Buy Milk" todoDate="04/10/2023" />
        <TodoItem todoName="Go to College" todoDate="04/10/2023" />
      </div>
    </center>
  );
}

export default App;
```


still the page looks like this
![[Pasted image 20241022090625.png]]


Now there is one more thing we can do i.e. we can make a component of `item-container` and the data is still `hard-coded` need some changes

#### Create objects
Let's create `todoItems` object and define the ***data*** like this
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItem from "./components/TodoItem";
import "./Index.css";
  
function App() {
  const todoItems = [
    {
      name: "Buy Milk",
      dueDate: "04/10/2023",
    },
    {
      name: "Go to College",
      dueDate: "04/10/2023",
    },
     {
      name: "Like this video",
      dueDate: "Right Now",
    },
  ];
  
  return (
    <center className="todo-container">
      <AppName />
      <AddTodo />
      <div className="items-container">
        <TodoItem todoName="Buy Milk" todoDate="04/10/2023" />
        <TodoItem todoName="Go to College" todoDate="04/10/2023" />
      </div>
    </center>
  );
}
  
export default App;
```


and `pass` it to the `TodoItem`
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItems from "./components/TodoItems";
import "./Index.css";

function App() {
  const todoItems = [
    {
      name: "Buy Milk",
      dueDate: "04/10/2023",
    },
    {
      name: "Go to College",
      dueDate: "04/10/2023",
    },
    {
      name: "Like this video",
      dueDate: "Right Now",
    },
  ];

  return (
    <center className="todo-container">
      <AppName />
      <AddTodo />
      <TodoItems todoItems={todoItems} />
    </center>
  );
}

export default App;
```




#### TodoItems.jsx
Let's create `TodoItems.jsx` file inside **components** folder
Do some changes


> [!NOTE] Before
```JSX
import TodoItem from "./TodoItem";

const TodoItems = ({ todoItems }) => {
  return (
    <div className="items-container">
      <TodoItem todoName="Buy Milk" todoDate="04/10/2023" />
      <TodoItem todoName="Go to College" todoDate="04/10/2023" />
    </div>
  );
};

export default TodoItems;
```



> [!Success] After
```JSX
import TodoItem from "./TodoItem";

const TodoItems = ({ todoItems }) => {
  return (
    <div className="items-container">
      {todoItems.map((item) => (
        <TodoItem todoName={item.name} todoDate={item.dueDate} />
      ))}
    </div>
  );
};

export default TodoItems;
```

Using **map method** we are making it *more efficient* & *modular*

#### Replace the Hard-coded values
inside the `App.jsx` do some changes to replace the *hard-coded* values 
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItems from "./components/TodoItems";
import "./Index.css";

function App() {
  const todoItems = [
    {
      name: "Buy Milk",
      dueDate: "04/10/2023",
    },
    {
      name: "Go to College",
      dueDate: "04/10/2023",
    },
    {
      name: "Like this video",
      dueDate: "Right Now",
    },
  ];

  return (
    <center className="todo-container">
      <AppName />
      <AddTodo />
      <TodoItems todoItems={todoItems} />
    </center>
  );
}

export default App;
```





One more thing 

Let's *modularize* the **CSS** part

Here the original **CSS** look like `Before` modularization
```CSS
/* .todo-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* min-height: 100vh; This will center it vertically */
} */

.todo-container h1{
  font-size: 45px;
  font-weight: 700;
  margin: 10px;
  margin-bottom: 25px;
}

.items-container {
  text-align: left;
}

input {
  width: 100%;
}

.kg-button {
  min-width: 80px;
}

.kg-row {
  margin: 10px 5px;
}
```


Let's apply **CSS Module** 

So we need to create the file for the supporting `.jsx` files respectively

`AppName.module.css` for `AppName.jsx`

inside `AppName.module.css` do some changes
```JSX
.todoHeading{
  font-size: 45px;
  font-weight: 700;
  margin: 10px;
  margin-bottom: 25px;
}
```

Here in the `AppName.module.css` file use the **camelCase** Format 

Now **import** that `AppName.module.css` inside the `AppName.jsx` file
#Before 
```CSS
function AppName (){
  return <h1 className="todo-container">Todo React App</h1>
}

export default AppName;
```



#After 
```JSX
import styles from "./AppName.module.css";
function AppName (){
  return <h1 className={styles.todoHeading}>Todo App</h1>
}

export default AppName;
```


After adding that `code` in the `AppName.module.css` file remove that code from the `App.css` file. Now the `App.css` looks like this
```
.items-container {
  text-align: left;
}

input {
  width: 100%;
}

.kg-button {
  min-width: 80px;
}

.kg-row {
  margin: 10px 5px;
}
```


> [!NOTE] NOTE
> We should not modularize the CSS code which is being used inside many files let it be there globally present as we doing modularization have to keep that in multiple file which is not a good idea So....


Let's create one more modular file  for the **CSS**  `item-container` i.e. for `TodoItems.jsx` which is being used inside

So, create file named `TodoItems.module.css`  

do some changes inside that file
```CSS
.itemsContainer {
  text-align: left;
}
```

Using that **CSS** in **camelCase Format**

let's import that inside `TodoItems.jsx` file

#Before 
```CSS
import TodoItem from "./TodoItem";

const TodoItems = ({ todoItems }) => {
  return (
    <div className="items-container">
      {todoItems.map((item) => (
        <TodoItem todoName={item.name} todoDate={item.dueDate} />
      ))}
    </div>
  );
};

export default TodoItems;
```



#After
```JSX
import TodoItem from "./TodoItem";
import styles from "./TodoItems.module.css"

const TodoItems = ({ todoItems }) => {
  return (
    <div className={styles.itemsContainer}>
      {todoItems.map((item) => (
        <TodoItem todoName={item.name} todoDate={item.dueDate} />
      ))}
    </div>
  );
};

export default TodoItems;
```


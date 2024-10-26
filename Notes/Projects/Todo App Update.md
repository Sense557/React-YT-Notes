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



---

Let's add some state management

Let's add some changes inside `App.jsx`
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItems from "./components/TodoItems";
import "./App.css";
import { useState } from "react";

function App() {
  const initialTodoItems = [
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
      dueDate: "right now",
    },
  ];
  
  let [todoItems, setTodoItems] = useState (initialTodoItems);

  const handleNewItem = (itemName, itemDate) => {
    console.log(`New Item added: ${itemName} Date: ${itemDate}`);
  };

  return (
    <center className="todo-container">
      <AppName />
      <AddTodo onNewItem={handleNewItem}/>
      <TodoItems todoItems={todoItems}/>
    </center>
  );
}

export default App;
```


Let's add some changes inside `AddTodo.jsx` file
```JSX
function AddTodo({ onNewItem }) {
  return (
    <div class="container text-center">
      <div class="row kg-row">
        <div class="col-6">
          <input type="text" placeholder="Enter Text Here" />
        </div>
        <div class="col-4">
          <input type="date" />
        </div>
        <div class="col-2">
          <button
            type="button"
            class="btn btn-success kg-button"
            onClick={() => onNewItem("a", "b")}
          >
            Add
          </button>
        </div>
      </div>
    </div>
  );
}

export default AddTodo;
```

See the changes we have made
![[Pasted image 20241026171636.png]]


Let's check if our stitching is going well or not inside `AddTodo.jsx`

```JSX
import { useState } from "react";

function AddTodo({ onNewItem }) {

  const [todoName, setTodoName] = useState();
  const [todoDate, setTodoDate] = useState();

  const handleNameChange = (event) => {
    console.log(event);
  }

  const handleDateChange = (event) => {
    console.log(event);
  }

  return (
    <div class="container text-center">
      <div class="row kg-row">
        <div class="col-6">
          <input type="text" placeholder="Enter Text Here" onChange={handleNameChange} />
        </div>
        <div class="col-4">
          <input type="date" onChange={handleDateChange}/>
        </div>
        <div class="col-2">
          <button
            type="button"
            class="btn btn-success kg-button"
            onClick={() => onNewItem("a", "b")}
          >
            Add
          </button>
        </div>
      </div>
    </div>
  );
}

export default AddTodo;
```
![[Pasted image 20241026175236.png]]



Now print the value what the user is entering inside input place inside `AddTodo.jsx`
```JSX
import { useState } from "react";

function AddTodo({ onNewItem }) {

  const [todoName, setTodoName] = useState();
  const [todoDate, setTodoDate] = useState();

  const handleNameChange = (event) => {
    console.log(event.target.value);
  }

  const handleDateChange = (event) => {
    console.log(event.target.value);
  }

  return (
    <div class="container text-center">
      <div class="row kg-row">
        <div class="col-6">
          <input type="text" placeholder="Enter Text Here" onChange={handleNameChange} />
        </div>
        <div class="col-4">
          <input type="date" onChange={handleDateChange}/>
        </div>
        <div class="col-2">
          <button
            type="button"
            class="btn btn-success kg-button"
            onClick={() => onNewItem("a", "b")}
          >
            Add
          </button>
        </div>
      </div>
    </div>
  );
}

export default AddTodo;
```


![[Pasted image 20241026174817.png]]


## Add Functionality


Let's ***Set*** the values user entering  inside `AddTodo.jsx`
```JSX
import { useState } from "react";

function AddTodo({ onNewItem }) {
  const [todoName, setTodoName] = useState();
  const [dueDate, setTodoDate] = useState();

  const handleNameChange = (event) => {
    setTodoName(event.target.value);
  };

  const handleDateChange = (event) => {
    setTodoDate(event.target.value);
  };

  const handleAddButtonClicked = () => {
    onNewItem(todoName, dueDate);
  };

  return (
    <div class="container text-center">
      <div class="row kg-row">
        <div class="col-6">
          <input
            type="text"
            placeholder="Enter Text Here"
            onChange={handleNameChange}
          />
        </div>
        <div class="col-4">
          <input type="date" 
          onChange={handleDateChange} />
        </div>
        <div class="col-2">
          <button
            type="button"
            class="btn btn-success kg-button"
            onClick={handleAddButtonClicked}
          >
            Add
          </button>
        </div>
      </div>
    </div>
  );
}
  
export default AddTodo;
```

![[Pasted image 20241026180910.png]]




After setting the values the input field should be blank
Let's do it inside `AddTodo.jsx`

```JSX
import { useState } from "react";

function AddTodo({ onNewItem }) {
  const [todoName, setTodoName] = useState();
  const [dueDate, setDueDate] = useState();

  const handleNameChange = (event) => {
    setTodoName(event.target.value);
  };

  const handleDateChange = (event) => {
    setDueDate(event.target.value);
  };


  const handleAddButtonClicked = () => {
    onNewItem(todoName, dueDate);    
    setTodoName("");
    setDueDate("");
  };

  return (
    <div class="container text-center">
      <div class="row kg-row">
        <div class="col-6">
          <input
            type="text"
            value={todoName}
            placeholder="Enter Text Here"
            onChange={handleNameChange}
          />
        </div>
        <div class="col-4">
          <input type="date"
          value={dueDate}
          onChange={handleDateChange} />
        </div>
        <div class="col-2">
          <button
            type="button"
            class="btn btn-success kg-button"
            onClick={handleAddButtonClicked}
          >
            Add
          </button>
        </div>
      </div>
    </div>
  );
}

export default AddTodo;
```

![[Pasted image 20241026182839.png]]




Now` let's add the Items entered by user in the list `
Let's do some changes inside  `App.jsx` file
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItems from "./components/TodoItems";
import "./App.css";
import { useState } from "react";

function App() {
  const initialTodoItems = [
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
      dueDate: "right now",
    },
  ];

  let [todoItems, setTodoItems] = useState(initialTodoItems);

  const handleNewItem = (itemName, itemDate) => {
    console.log(`New Item added: ${itemName} Date: ${itemDate}`);
    const newTodoItems = [
      ...todoItems,
      {
        name: itemName,
        dueDate: itemDate,
      },
    ];
    setTodoItems(newTodoItems);
  };

  return (
    <center className="todo-container">
      <AppName />
      <AddTodo onNewItem={handleNewItem} />
      <TodoItems todoItems={todoItems} />
    </center>
  );
}

export default App;
```


![[Pasted image 20241026194617.png]]


## Welcome Message

Let's add a `Welcome Message` 
Let's create a welcome component  i.e. `WelcomeMessage.jsx` after creation or changes import it inside  `App.jsx` file

Let's do some changes
```JSX
const WelcomeMessage = () => {
  return (
    <p>Enjoy your day</p>
  );
}

export default WelcomeMessage;
```


Let's import it inside `App.jsx` so that ***Welcome Message*** will be visible
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItems from "./components/TodoItems";
import WelcomeMessage from "./WelcomeMessage";
import "./App.css";
import { useState } from "react";

function App() {
  const initialTodoItems = [
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
      dueDate: "right now",
    },
  ];
  let [todoItems, setTodoItems] = useState(initialTodoItems);

  const handleNewItem = (itemName, itemDate) => {
    console.log(`New Item added: ${itemName} Date: ${itemDate}`);
    const newTodoItems = [
      ...todoItems,
      {
        name: itemName,
        dueDate: itemDate,
      },
    ];
    setTodoItems(newTodoItems);
  };

  return (
    <center className="todo-container">
      <AppName />
      <AddTodo onNewItem={handleNewItem} />
      <WelcomeMessage />
      <TodoItems todoItems={todoItems} />
    </center>
  );
}

export default App;
```


![[Pasted image 20241026195954.png]]



Let's add some logic so that it will be dynamic i.e. if items not there it will be visible else not 

Let's do some changes inside `App.jsx` file
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItems from "./components/TodoItems";
import WelcomeMessage from "./WelcomeMessage";
import "./App.css";
import { useState } from "react";

function App() {
  const initialTodoItems = [];
  let [todoItems, setTodoItems] = useState(initialTodoItems);

  const handleNewItem = (itemName, itemDate) => {
    console.log(`New Item added: ${itemName} Date: ${itemDate}`);
    const newTodoItems = [
      ...todoItems,
      {
        name: itemName,
        dueDate: itemDate,
      },
    ];
    setTodoItems(newTodoItems);
  };

  return (
    <center className="todo-container">
      <AppName />
      <AddTodo onNewItem={handleNewItem} />
      {todoItems.length === 0 && <WelcomeMessage />}
      <TodoItems todoItems={todoItems} />
    </center>
  );
}

export default App;
```


![[Pasted image 20241026200610.png]]



![[Pasted image 20241026200551.png]]



Let's add some styling to the `Welcome message` so the it will look good

Let's create a file named `Welcome.module.css` file inside which we are going to add some **CSS**

Let's do some changes inside `WelcomeMessage.module.css` file
```JSX
.welcome {
  font-size: 30px;
  margin-top: 50px;
  font-weight: 600;
}
```


Let's do some change inside `WelcomeMessage.jsx` also (importing and some minor changes)
```JSX
import styles from "./WelcomeMessage.module.css"

const WelcomeMessage = () => {
  return (
    <p className={styles.welcome}>Enjoy your day</p>
  );
}

export default WelcomeMessage;
```



![[Pasted image 20241026201944.png]]

![[Pasted image 20241026200551.png]]



## Delete Functionality
Let's add the delete functionality

so for that we need do some changes inside `App.jsx` as parent is ***App*** having the list items so it must have the `delete handler` first which then will passed to it's child where `Delete` button is defined (Delete button is defined inside `TodoItem.jsx`)

Let's go inside `App.jsx` and do some changes
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItems from "./components/TodoItems";
import WelcomeMessage from "./WelcomeMessage";
import "./App.css";
import { useState } from "react";

function App() {
  const initialTodoItems = [];

  let [todoItems, setTodoItems] = useState(initialTodoItems);

  const handleNewItem = (itemName, itemDate) => {
    console.log(`New Item added: ${itemName} Date: ${itemDate}`);
    const newTodoItems = [
      ...todoItems,
      {
        name: itemName,
        dueDate: itemDate,
      },
    ];
    setTodoItems(newTodoItems);
  };

  const handleDeleteItem = (itemName) => {
    console.log(`Item deleted: ${itemName}`);
  };
  
  return (
    <center className="todo-container">
      <AppName />
      <AddTodo onNewItem={handleNewItem} />
      {todoItems.length === 0 && <WelcomeMessage />}
      <TodoItems todoItems={todoItems} onDeleteClick={handleDeleteItem} />
    </center>
  );
}

export default App;
```


then go inside `TodoItems.jsx` and do some changes so that it can pass the delete functionality to it's child `TodoItem.jsx`

```JSX
import TodoItem from "./TodoItem";

const TodoItems = ({ todoItems, onDeleteClick }) => {
  return (
    <div className="items-container">
      {todoItems.map((item) => (
        <TodoItem
          todoName={item.name}
          todoDate={item.dueDate}
          onDeleteClick ={onDeleteClick}
        />
      ))}
    </div>
  );
};

export default TodoItems;
```


then go inside `TodoItems.jsx` and do some changes so that it can pass the delete functionality to it's child `TodoItem.jsx`
```JSX
function TodoItem({ todoName, todoDate, onDeleteClick }) {
  return (
    <div class="container">
      <div class="row kg-row">
        <div class="col-6">{todoName}</div>
        <div class="col-4">{todoDate}</div>
        <div class="col-2">
          <button
            type="button"
            className="btn btn-danger kg-button"
            onClick={() => onDeleteClick(todoName)}
          >
            Delete
          </button>
        </div>
      </div>
    </div>
  );
}

export default TodoItem;
```



![[Pasted image 20241026204807.png]]




Now we came to know that our `stitching` working fine so now we can implement the logic to delete an item


Let's do some changes inside `App.jsx`
```JSX
import AppName from "./components/AppName";
import AddTodo from "./components/AddTodo";
import TodoItems from "./components/TodoItems";
import WelcomeMessage from "./WelcomeMessage";
import "./App.css";
import { useState } from "react";

function App() {
  const initialTodoItems = [];

  let [todoItems, setTodoItems] = useState(initialTodoItems);

  const handleNewItem = (itemName, itemDate) => {
    console.log(`New Item added: ${itemName} Date: ${itemDate}`);
    const newTodoItems = [
      ...todoItems,
      {
        name: itemName,
        dueDate: itemDate,
      },
    ];
    setTodoItems(newTodoItems);
  };

  const handleDeleteItem = (todoItemName) => {
    const newTodoItems = todoItems.filter((item) => item.name !== todoItemName);
    setTodoItems(newTodoItems);
    console.log(`Item deleted: ${todoItemName});
  };

  return (
    <center className="todo-container">
      <AppName />
      <AddTodo onNewItem={handleNewItem} />
      {todoItems.length === 0 && <WelcomeMessage />}
      <TodoItems todoItems={todoItems} onDeleteClick={handleDeleteItem} />
    </center>
  );
}

export default App;
```



![[Pasted image 20241026210913.png]]



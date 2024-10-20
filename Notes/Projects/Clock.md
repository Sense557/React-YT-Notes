
![[Pasted image 20241020222340.png]]


Let's first do some cleanup i.e.
- Delete `index.css`
- Create `Index.css`
- do some changes inside `main.jsx`
- do some changes inside `App.jsx`

inside `main.jsx`
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

inside `App.jsx`
```JSX
import React from 'react'
import './Index.css'

function App() {
  return (
    <div>
      <h1>Bharat Clock</h1>
      <p>This is the clock that shows the time in Bharat at all times</p>
      <p>This is the current time: 26/10/2023 10:38:17 AM</p>
    </div>
  )
}

export default App
```



==Let's make components to modularize the app==

Why Because we don't need hard-corded values and to avoid repetition of works 

It has *3 components* i.e. 3 sections
1. **Clock Heading**
2. **Clock Slogan**
3. **Current Time**

Let's first Create the folder *components* inside the *src* folder
i.e.  `src/components`

Inside which create *components* respectively as shown below

`src/components/ClockHeading.jsx`
`src/components/ClockSlogan.jsx`
`src/components/CurrentTime.jsx`

#### ClockHeading.jsx

Let's first create `ClockHeading.jsx` inside *components* folder
Do some changes like coping the data from and pasting here
```JSX
let ClockHeading = () => {
  return <h1>Bharat Clock</h1>
}

export default ClockHeading;
```

**why arrow function being used here just to showcase that this way also possible**


and import this component inside `App.jsx`
```JSX
import React from 'react'
import './Index.css'
import ClockHeading from './components/ClockHeading'

function App() {
  return (
    <div>
      <ClockHeading />
      
      <p>This is the clock that shows the time in Bharat at all times</p>
      <p>This is the current time: 26/10/2023 10:38:17 AM</p>
    
    </div>
  )
}

export default App
```



#### ClockSlogan.jsx

Inside this file do some changes
```JSX
let ClockSlogan = () => {
  return <p>This is the clock that shows the time in Bharat at all times</p>
}

export default ClockSlogan;
```

**why arrow function being used here just to showcase that this way also possible**

export it in `App.jsx` file 
```JSX
import React from 'react'
import './Index.css'
import ClockHeading from './components/ClockHeading'
import ClockSlogan from './components/ClockSlogan'


function App() {
  return (
    <div>
      <ClockHeading />
      <ClockSlogan />
      
      <p>This is the current time: 26/10/2023 10:38:17 AM</p>
    
    </div>
  )
}

export default App
```




#### CurrentTime.jsx

Let's do some changes inside `CurrentTime.jsx`
```JSX
let CurrentTime = () => {
  return <p>This is the current time: 26/10/2023 10:38:17 AM</p>
}

export default CurrentTime;
```

**why arrow function being used here just to showcase that this way also possible**

Import it inside `App.jsx` file
```JSX
import React from 'react'
import './Index.css'
import ClockHeading from './components/ClockHeading'
import ClockSlogan from './components/ClockSlogan'
import CurrentTime from './components/CurrentTime'

function App() {
  return (
    <div>
      <ClockHeading />
      <ClockSlogan />
      <CurrentTime />
    </div>
  )
}

export default App
```


After **modularization** `App.jsx` look like this
```JSX
import React from 'react'
import './Index.css'
import ClockHeading from './components/ClockHeading'
import ClockSlogan from './components/ClockSlogan'
import CurrentTime from './components/CurrentTime'

function App() {
  return (
    <div>
      <ClockHeading />
      <ClockSlogan />
      <CurrentTime />
    </div>
  )
}

export default App
```


Now the page looks like this
![[Pasted image 20241020231420.png]]





To align all these items to center use `<center></center>` tag in the `App.jsx` in-place of `<div></div>` tag
```JSX
import React from 'react'
import './Index.css'
import ClockHeading from './components/ClockHeading'
import ClockSlogan from './components/ClockSlogan'
import CurrentTime from './components/CurrentTime'

function App() {
  return (
    <center>
      <ClockHeading />
      <ClockSlogan />
      <CurrentTime />
    </center>
  )
}

export default App
```


Now the page looks like this
![[Pasted image 20241020231506.png]]



Let's *install bootstrap*
```
npm i bootstrap@5.3.3
```


Let's *import bootstrap* inside `main.jsx`
```
import 'bootstrap/dist/css/bootstrap.min.css'
```


do some changes inside `main.jsx`
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



#### CurrentTime.jsx
Do some changes to `avoid putting hard-corded values`
```JSX
let CurrentTime = () => {

  let time = new Date();
  
  return <p>This is the current time: {time.toLocaleDateString ()} - {time.toLocaleTimeString()} </p>
}

export default CurrentTime;
```


Now the page will look like this
![[Pasted image 20241020233410.png]]



Now Let's apply some **Bootstrap CSS**
#### ClockHeading.jsx
```JSX
let ClockHeading = () => {
  return <h1 className="fw-bolder">Bharat Clock</h1>
}

export default ClockHeading;
```


#### ClockSlogan.jsx
```JSX
let ClockSlogan = () => {
  return <p className="lead">This is the clock that shows the time in Bharat at all times</p>
}

export default ClockSlogan;
```


#### CurrentTime.jsx
```JSX
let CurrentTime = () => {

  let time = new Date();
  return <p className="lead">This is the current time: {time.toLocaleDateString ()} - {time.toLocaleTimeString()} </p>
}

export default CurrentTime;
```





After **Bootstrap CSS Application** page looks like this
![[Pasted image 20241020233827.png]]



















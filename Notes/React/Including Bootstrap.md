1. **Responsive :** *Mobile-first* design for all device sizes
2. **Components :** *Pre-styled elements* like buttons and navbars
3. **Customizable :** *Modify* default styles as needed
4. **Cross-Browser :** *Consistent* look across browsers
5. **Open-Source :** *Free* with community support


1. Install :
```
npm i bootstrap@5.3.3
```

2. Import : inside `main.jsx` file
```JSX
import "bootstrap/dist/css/bootstrap.min.css";
```

Do some changes inside `App.jsx` file
```JSX
import './App.css'

function App() {
  return (
    <div>
      <button type="button" class="btn btn-primary">Primary</button>
      <button type="button" class="btn btn-secondary">Secondary</button>
      <button type="button" class="btn btn-success">Success</button>
      <button type="button" class="btn btn-danger">Danger</button>
      <button type="button" class="btn btn-warning">Warning</button>
      <button type="button" class="btn btn-info">Info</button>
      <button type="button" class="btn btn-light">Light</button>
      <button type="button" class="btn btn-dark">Dark</button>

      <button type="button" class="btn btn-link">Link</button>
    </div>
  )
}
  
export default App
```


What did I do in the previous code is that imported button components from bootstrap and pasted here


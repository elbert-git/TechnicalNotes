# React-JS

A way to build reactive web UI with components(like prefabs in unity)

---

* topics i wa want to learn next
  * global state managers like redux
  * cool ass animations

---

# **Intuition of a ReactJS web-app**

===================================================================

When calling the npx create-react-app. It creates an html and a bunch of scripts that connect to it.

React will connect to the <Body/> and render in your components there. Creating a single page application.

A react app is just a tree of components with JS functionalities

#### JSX

Essentially javascript but recognizing html elements

```
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

# **Setup**

===================================================================

Make sure node is installed in the terminal

```
npx create-react-app <name-of-react-app>
```

the name of the project must be one word, spaces replaced with dashes

this creates a basic react boiler-plate project.

### Initializing a react-js file

use this to prep a javascript file to use basic react components

```
import React from 'react';
import ReactDOM from 'react-dom';
```

### Running a live server

```
npm start
```

---

# **Components**

===================================================================

Below is a basic react-component.js file

**remember "export default" to allow the function to be imported to other files**

```
import React from 'react';
import ReactDom from 'react-dom';

export default function componentName(){
  return(
    <div>
      <h1>Hello World</h1>
    </div>
  )
}
```

* Importing react classes

You see that you import the react and react-dom classes to create react components

* creating a component

Literally just creating a function that returns a div.

you can only return one div. but that div can nest a whole tree of divs

keep in mind you need "export default" to make the function "public" (so to speak) so that you can import the component from other files

* Using the component

After creating the component. you can import the js file into another file

and use the prop like a new html tag

```
import React from 'react';
import ReactDom from 'react-dom';

export default function componentName(){
  return(
    <div>
      <h1>Hello World</h1>
    </div>
  )
}
```

## Creating Function Components

These are slightly simpler components. but also the faster way to create them. And they cover most of your functionalities.

**remember "export default" to allow the function to be imported to other files**

```
import React from 'react';
import ReactDom from 'react-dom';

export default function ComponentName() {
  return (
    <div>
      html goes here {expressions in curly brackets}
    </div>
  )
}
```

## Class Components

These are components with the whole power of a JS class.

Use this for more complex elements.

```
class ComponentName extends React.Component {
  render() {
    return (
      <div>
        <h1>html go here</h1>
      </div>
    )
  }
}
```

# **Styling**

===================================================================

you have global styling like you normally do.

just make sure you wrap all your elements in larger component. this component will imprt the styule

```
//in main app.js

function App(){
  return <div>
    <MainParent> {//<--- import style to this component}
      {//children}
    </MainParent>
  </app>
}
```

# **Props**

===================================================================

props are like onStart() variables.

html has attributes like

```
<div attributeName="value">
  hello
</div>
```

you can create custom attributes called props

```
<customReactComponent propName=value />
```

you can process the props in code to render diff html elements

```
import React from 'react';
import ReactDom from 'react-dom';

export default function customReactComponent (prop) {
  return (
    <div>
      here is the prop {prop.propName}
    </div>
  )
}
```

* remember set prop as argument

### Data flows down

you define the state as high into the component tree as you need.

but pass the props down component to component.

# **useState**()

===================================================================

#### what are states

essentially dynamic variables that can change data. props are usually more static. used for more on start variables

#### how to use states

```
import React from 'react';
import {useState} from 'react';
import ReactDom from 'react-dom';

export default function customReactComponent () {
  // create state here
  const [datas, setData] = useState(() => data);

  // set state (change state)
  setVarArryayName(() => data);

  return (
    <div>
      here is the prop {prop.propName}
    </div>
  )
}
```

* import the useState class
* create the state variable and state variable editing fucntion
* use or change the prop
* i dont know why but when creating and changing states just use arrow fucntions to return the data.

  just do it.

## Some important things to note

* don't edit a state directly. create a new data then set that data

### setState() is an async function!

by the time you console.log() after a setState the data probably isn't updated. To check data updates. useEffect to log the state every time the chat Data changes

# **useEffect**()

===================================================================

allows functions to run. when an state array is changed

### how to use

```
useEffect(() => {
  // function or code goes here
},[dependent array])
```

the code block will run everytime inputted array is changed

### onStart function (kinda)

```
useEffect(() => {
  // function or code goes here
},[])
```

you can put an empty array (meaning that it will never change/update). so that it will only run once on start and never again.

# **useRef**()

===================================================================

this is how you reference other elements in the dom

in html you would directly reference from the dom.

but here you need to use useRef()

### how to use

```
import React from 'react';
import ReactDom from 'react-dom';
import {useRef} from 'react';

export default function customReactComponent (prop) {
  const varForElementName = useRef();

  return (
    <div ref={varForElementName}>
      here is the prop {prop.propName} 
    </div>
  )
}
```

* you import useRef from react
* create a var and set it to useRef()
* in the element you want it to reference
  * give an attribute ref with the value of the variable name

### useRef() through children

```
import React from 'react';
import ReactDom from 'react-dom';
import {useRef} from 'react';

export default function customReactComponent (prop) {
  const varForElementName = useRef();

  return (
    <div >
      <parent refHook={varForElementName}/>
    </div>
  )
}
```

```
import React from 'react';
import ReactDom from 'react-dom';
import {useRef} from 'react';

export default function customReactComponent (prop) {
  return (
    <div ref={prop.refHook}></div>
  )
}
```

# **useContext**()

===================================================================

Instead of passing one prop from one child to the other.

you can set a context where all of children elements gets access to one variable

### In parent

```
// create a context outside of the function component
export const ContextData = React.createContext();

export default function ContextProvider ({children}) {
  // put context handling code here
  return m
    <ContextData.Provider value={props to pass down}>
      {children}
    </ContextData.Provider>
  )
}
```

* outside of component fucntion. just create a context object.
* then create a new element that wraps over the children you want to pass down. which is the context variable name with ".Provider". also pass down the data to the "value" attribute.

### In child

```
import React, {useContext} from 'react'; // import react and use context hook
import {ContextData} from '../path/to/contextCreatedFile'; // import context

class ComponentName extends React.Component {
  const contextData = useContext(ContextData);
  render() {
    return (
      <div>
        {contextData}
      </div>
    )
  }
}
```

### Creating a context component

This is literally just declutter and streamline how contexts are written

```
import React from 'react';
import ReactDom from 'react-dom';
import {useContext} from 'react';

export const Context = React.createContext();

export function useCreatedContext(){
  return useContext(Context);
}

export default function ContextProvider ({children}) {
  // put context handling code here
  return (
    <Context.Provider value={props to pass down}>
      {children}
    </Context.Provider>
  )
}
```

* create a new component and setup the context.
* you can use {children to render children}
* use this component to handle setting/updating the theme
* create new public/exported function to allow other js files to get context data.

### Updating context data

use useState and pass the data and setData functions through the context.

* in parent component

```
export default function ParentComponent() {
  const [val, setVal] = useState();

  return (
    <Context.Provider value={[val, setVal]}>
      <childComponent/>
    </Context.Provider>
  );
}
```

* in child component

```
export default function childComponent(){
  const [val, setVal] = useContext(Context);

  return (
    <div></div>
  );
};
```

# **List**

===================================================================

you can loop over a json/array to display a lot of data.

### the map functions

```
return(
 array.map(obj => {
 return <div attribute=obj.value propName=obj.value key=uniqueid/>};
)
```

### unique keys

when using the map array. react needs unique id to all the elements. this lets react know which element has changed so that it can only render that element. it also just prevents weird bugs.

simplest way is to just add an index to the arrray object. but this isnt ideal for many situations

you can use the **uuid package** from npm to easily solve this issue

1. **first install uuid**

```
npm install uuid --save-dev
```

2. **import to the file that creates desired array to be mapped over.**

this will allow you to create new unique ids with a simple func

```
import React from 'react';
import ReactDom from 'react-dom';
import { v4 as uuidv4 } from 'uuid';

return(
 array.map(obj => {
 return <div attribute=obj.value propName=obj.value key={uuidv4()}/>};
)
```

# **Events**

===================================================================

You need to create your own custom react hooks to use events outside of React

### Creating your own hook for your custom events

# **Routing**

===================================================================

source

<https://www.youtube.com/watch?v=Jppuj6M1sJ4>

### installation

```
npm install react-router-dom --save-dev
```

### Import

```
import {BrowserRouter, Routes, Route, Link} from "react-router-dom";
```

### Basic usage

```
import React from 'react';
import ReactDom from 'react-dom';
import {BrowserRouter, Routes, Route, Link} from "react-router-dom";

export default function ParentComponent (prop) {
  return (
    <BrowserRouter>
      <Link to="/path" >link to path</Link>
      <Routes>
        <Route path="/" element={<Home/>}/>
        <Route path="/about" element={<About/>}/>
        <Route path="/contact" element={<Contact/>}/>
        <Route path="*" element={<MissingPage/>}/>
      </Routes>
    </BrowserRouter>
  )
}
```

* 3 nested compnentes
  * BrowserRouter > Routes> Route(your individual route)
* Routes go in this format

  ```
  <Route path="/" element={<elementName/>}/>
  
  ```
* default page for broken/missing routes

  ```
  <Route path="*" element={<MissingPage/>}/>
  
  ```
* Linking

  ```
  <Link to="/path" >link to path</Link>
  
  ```
* do note that only things within the <routes> tag update when you change routes

### Redirecting

many times you will want to switch pages by script

```
import {useNavigate} from 'react-router-dom';
let navigate = useNavigate(); // this returns teh navigate func
navigate('/path');
```

### Scroll 0

when you change routes in react. most of the time you want the scroll to be reset to the top.

just put a use effect on the component loaded that resets scroll to the top.

```
window.scroll(0,0);
```

### Url Parameters

you can encode data in the url

in BrowserRouter

```
import React from 'react';
import ReactDom from 'react-dom';
import {BrowserRouter, Routes, Route, Link} from "react-router-dom";

export default function ParentComponent (prop) {
  return (
    <BrowserRouter>
      <Link to="/path" >link to path</Link>
      <Routes>
        <Route path="/" element={<Home/>}/>
        <Route path="/Profile/:userID" element={<userProfile/>}/
      <Routes>
    <BrowserRouter>
  )
}
```

* add a route where the path has a ":" that denotes the variableName for the paramenter

in component

```
import React, {useParams} from 'react';
import ReactDom from 'react-dom';

export default function componentName(){
  const URLparameters = useParams();
 
  return(
    <div>
      <h1>Hello {param.userID}</h1>
    </div>
  )
}
```

* import the useParam() hook
* use the fucn to return url parameters object.
  * that object will contain your url parameters

### Nesting Routes

```
import React from 'react';
import ReactDom from 'react-dom';
import {BrowserRouter, Routes, Route, Link} from "react-router-dom";

export default function ParentComponent (prop) {
  return (
    <BrowserRouter>
      <Link to="/path" >link to path</Link>
      <Routes>
        <Route path="/" element={<Home/>}/>
        <Route path="/books/*" element={<userProfile/>}>
          <Route path="book-title" element={<bookTitlePage>}/>
        </Route>
      <Routes>
    <BrowserRouter>
  )
}
```

* add a route tag as child of one of the routes
* put a '/\*' in front of the parent route path attribue
* the child route tag path is relative to the parent route tag

#### The <outlet> tag

controls where the nested routes will inject the children components

```
import React from 'react';
import ReactDom from 'react-dom';
import {Outlet} from "react-router-dom";

export default function bookTitlePage(){
  return(
    <div>
      {// nested routes children will appear below}
      <Outlet/>
    </div>
  )
}
```

### Private Routes

essentially creating a new component. where it will conditionally render an outlet or rendersomething else or redirect to somewhere else

```
import React from 'react';
import ReactDom from 'react-dom';
import {BrowserRouter, Routes, Route, Link} from "react-router-dom";

export default function ParentComponent (prop) {
  return (
    <BrowserRouter>
      <Link to="/path" >link to path</Link>
      <Routes>
        <Route path="/" element={<Home/>}/>
        <Route element={<ProtectedRoutes/>}>
          <Route path="book-title" element={<bookTitlePage>}/>
        </Route>
      </Routes>
    </BrowserRouter>
  )
}
```

* create a new route that renders your custom ProtectedRoutes Component
* the children of this route tag are protected routes

```
import React from 'react';
import ReactDom from 'react-dom';
import {Outlet} from "react-router-dom";
import {useContext} from 'react';
import {AuthProvider} from '../pathToProvider';j
import {ErrorPage} from 'ErrorPage';

export default function ProtectedRoutes(){
  const user = useContext(AuthProvider);
  return(
    <div>
      {user ? return<outlet> : return <ErrorPage/>}
    </div>
  )
}
```

* in the protected route component
* use react context hook to get authorisation parameters
* use the auth parameters to conditionally render the outlet

### ❗ Relative resource path issues with routers

set a basename for the BrowserRouter element. set it as the domain's subdirectory.

```
<BrowserRouter basename="/{subdirectory}/"></BrowserRouter>
```

# Other misc links

===================================================================

* deploying to github pages
  * [https://www.youtube.com/watch?v=2hM5viLMJp](https://www.youtube.com/watch?v=2hM5viLMJpA&t=274s)A

# Sources

===================================================================

A lot of this is from the webdev simplified tutorial.

<https://www.youtube.com/watch?v=hQAHSlTtcmY>
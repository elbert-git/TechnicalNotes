# Vue Basics

These are notes from <https://www.vuemastery.com/courses/intro-to-vue-3>

## 1) Setting up the Vue app

### setup

import the vue script in html at the <head/>

```
<!-- Import Vue.js -->
  <script src="https://unpkg.com/vue@3.0.11/dist/vue.global.js">          </script>
```

then make a new JS file

```
const app = Vue.createApp({
    data() {
        return {
            variable: 'value'
        }
    }
})
```

link this to the end of the html and add a new small script tag at the end to mount the app to a chosen element

```
    <!-- Import App -->
    <script src="./main.js"></script>
    <!-- Mount App -->
    <script>
      const mountedApp = app.mount('#app')
    </script>
```

### Basic innerHTML bindings

changing the innerHTML of an element by vue

```
<div class="product-info">
   <h1>{{ product }}</h1>
</div>
```

you can put expressions inside of your tags defined by the data in the vue app

this reacts to changes in the variable in run-time

---

## 2) Connecting Vue to HTML Attributes

Connecting variables to html attributes not just their innerHTML

```
<img v-bind:src="imageURL" alt="">
```

it's just adding a "v-bind" behind the attribute then putting the variable name as the value of the attribute

### Shorthand;

```
<img :src="image"> 
```

\:"attritbutename"

---

## 3) Conditional rendering

if statements to show/hide html elements

```
<p v-if="inventory > 10">In Stock</p>
<p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
<p v-else>Out of Stock</p>
```

use "v-if"=<boolean> toggle visibilty

the boolean can be linked to a variable in the vue app

### v-if or v-show

v-if is for taking and removing the element from dom, not as fast as v-show. used for inserting a new thing or

v-show is just toggling visibility (display:none in css), it's a lot more performant and used for constant toggling.

---

## 4) list/array rendering

You can render attach an array of data to html lists

let's say you have an array of vue created in the vue app

```
const app = Vue.createApp({
    data() {
        return {
            details: ['50% cotton', '30% wool', '20% polyester']
        }
    }
})
```

you can create list automatically processing the data in that array

```
<ul>
  <li v-for="detail in details">{{ detail }}</li>
</ul>
```

---

## 5) Event handling

### In a nutshell

you can attach function at any event emitted

just by adding the attribute

```
v-on:[event type]
```

for example

```
<button class="button" v-on:click="logic to run">Add to Cart</button>
```

### Triggering custom functions

you can trigger function you created in your vue app by

```
<button class="button" v-on:click="createdFunctionName">Add to Cart</button>
```

in the app you define you custom functions as shown

```
const app = Vue.createApp({
  data() {
    return {
      cart: 0,
      ...
    }
  },
  methods: {
    addToCart() {
      this.cart += 1
    }
  }
})
```

note the "this.cart"

you change variables by adding "this", as you need to specify the scope of the variable

### Shorthand

```
<button class="button" @click="addToCart">Add to Cart</button>
```

you can shorten the syntax for "v-on "to "@"

---

## 7) Class and style binding

```
<div :style="{ backgroundColor: variant.color }">
</div>
```

you can just add a v-bind:style=styleObject

you can also add style objects to the app data variables. just by creating style object variable in the app. like so

```
data(){
 return{
  styles: {propertName: value}
 }
}
```

note that the property names are Camel-Case not kebab-case

---

## 8) Computed Properties

This is a bit irrelavant for now.

---

## 9) Components And Props

breaking down the website into modular pieces

### Creating component

1. create js file
2. create the component

```
app.component('component-name', {component-data})
```

this is the empty component template

3. component structure

in the curly brackets is where you put everything

```
app.component('component-name', {
  props: {propName: {var: value}},
  template: '<div>html just becomes a very long string<div>',
  data() {return {variableName: value}},
  methods: {functionName(){//function stuff}},
  computed: {title() {"stringA" + "stringb"}}
})
```

you can put

* template html
  * which is the html of the component
* data()
  * the variables of the component
* method:
  * the fucntions in a component
* computed:
  * the starting computed variables of a component
  * this is for like rare calculations so that the dom doens't have to check these variables all the time

### Importing the component

You import it in the main html, at the end of the body like so. after you import the main app and before you mount the app

```
<body>    
    <!-- Import App -->
    <script src="./main.js"></script>

    <!-- Import Components -->
    <script src="./components/ComponentName.js"></script>

    <!-- Mount App -->
    <script>
      const mountedApp = app.mount('#app')
    </script>
</body>
```

then just use it like a new html tag

```
<component-name><component-name>
```

### Properties(props)

in your component structure you can add you props to the "props " section. this is how you pass down data to children components

```
app.component('product-display', {
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  ...
}
```

you can add a "required: true" to make the property you pass down mandatory

#### using the prop

use "this.propName" in code

---

## 10) Emitting Events

this is how you pass data to parent components

### In Child component

emit a signal to call execute a scripted function. Add a function argument if you need

```
app.component('child-component', {
  methods: emitSignal(){
    this.$emit('signal-name', functionArgument)
    }
  },
}
```

emit a this is how you emit a signal

### in Parent Component

in the html (template section) add a signal listener and assign function to call when a signal is received. You obviously have to had created method in the method section for it

```
app.component('parent-component', {
  template: '
    <child-component @signal-name="SomeFunction"></child-component>
  ',
  methods: someFunction(functionArgument){
    console.log(functionArgument);
    }
  },
}
```
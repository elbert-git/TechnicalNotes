# **-|- Vue JS**

===================================================================

# **General**

It's a web ui library like react. But just.... better. It's pretty flexible and you can create a simple web widget that you just put into an html section. Or you can create full single page apps with it.

# **Creating a Vue widget**

===================================================================

### **Import and setup**

Import vue in header

```
<!-- Import Vue.js -->
<script src="https://unpkg.com/vue@3.0.11/dist/vue.global.js"/>
```

create the mount point. This is the root of the vue app

```
<div id="app">
  <!-- vue html code goes here. or you can put in main object -->
</div>
```

Setup the vue app with a script

```
<!-- Import Js -->
<script src="./main.js"></script>
```

inside the script

```
const app = Vue.createApp({/*you put vue code here*/})
```

Vue widget works by what is inside that object you pass into the createApp function. all data and fucntionaliti is inside that object.

### **Structure of main object**

the main object is like is a full component file. But in an JS object form.

##### Template

The html you want this component to render goes here. It's like a return in react.

```
const app = Vue.createApp({
  template: `
    <div>HTML goes here</div>
  `
});
```

##### Data

This is your component props/state. The current properties of the component. It's a function that returns an object that contains all the datas

```
const app = Vue.createApp({
  Data(){
    return {
      varName: val;
    }
  }
});
```

##### Computed properties

These are properties that are derived from 2 or more other properties. Honestly, this could be a fucntion. But hey it's a thing.

```
const app = Vue.createApp({
  Data(){
    return {
      a: 1,
      b: 2
    }
  },
  computed: {
    sum(){return this.a + this.b}
  }
});
```

##### methods

These are fucntions scoped into the component. ya know this.

```
const app = Vue.createApp({
  methods: {
    someFunc(){
      // do something
      // this is how you change the component data
      this.someVarInThisProp = val ;
    }
  }
});
```

##### props

this are the custom html attributes you can add into your components.

```
const app = Vue.createApp({
  props: {
    propName:{
      type: {typeofvar},
      required: false // put true if required
    }
  }
});
```

### **Javascript data and functions with component HTML**

##### Inputting JS data in innerHTML

```
<div>{{varName}}</div>
<div>{{SomeFuncThatReturnsData()}}</div>
```

##### Inputting JS Data in html attributes

you put \`vbind\`

```
<img :src="varName" :alt="SomeFuncThatReturnsData()"/>
```

##### Conditional rendering

You can use v-if. but this completely mounts and unmounts the element. So this shouldn't be toggled often

```
<div v-if='someBoolean'>Only show this if true </div>
<div v-else-if='someBoolean'>show this if something else</div>
<div v-else>show this if anything else</div>
```

But if you need it to toggle often, use v-show. This just toggles style display: none.

```
<div v-show='someBoolean'>Only show this if true </div>
```

##### Loop rendering

You can render elements with loops

```
<div v-for="(val, index) in someArray">{{val}}<div>
```

The above will render a bunch of divs based on the array

You can do the same with components

```
<component
v-for="(item,index) in arrayName"
:item="item.property"
:key="index"
></component>
```

##### Events and triggering functions

the format is just  @{eventName}

```
<button @click="someFunc()"></button>
```

you can pass arguments like so

```
<button @click="someFunc(arg, $event, this.varName)"></button>
```

You can pass any arbitrary arg. But the event itself will be $event and getting a var from the component data will be this.varName

Below is how you prevent the default event fucntion.

```
<form @submit.prevent="onSubmit"></form>
```

You can also listen for keyboard/mouse input events. More info on that here <https://vuejs.org/guide/essentials/event-handling.html#key-modifiers>

##### Styling in vue

Like in react you use style objects on top of using css classes.

```
<my-component :class="{ display: flex }"></my-component>
```

##### Props

Same like any data. use the colon.

```
<my-component :propName="val"></my-component>
```

### **Components**

##### Creating components

import your component js file into html

```
<script src="./main.js"></script>
```

Inside the component script

```
app.component('MyComponentName',{/*component code goes here*/});
```

Structure is the same way you would the main component

you c an also chain componenet creation like so.

```
app
  .component('ComponentA', {/*component code goes here*/})
  .component('ComponentB', {/*component code goes here*/})
  .component('ComponentC', {/*component code goes here*/})
```

##### Importing components

After you import the component script into the file. 

```
<componenetName/>
```

##### Creating and using props;

create prop

```
app.component({
  props: {
    propName:{
      type: {typeofvar},
      required: false // put true if required
    }
  }
});
```

use prop

```
<my-component :propName="val"></my-component>
```

##### Custom events

events are how child components reach into parent components to communciate.

Creating an event

```
<button @click="$emit('someEvent', arg1, arg2)">click me</button>
```

Making parent listen for events

```
<MyComponent @some-event="callback" />
```

Arguments will automatically be called inputed in.

---

* ~~vue in general~~
* ~~creating a vue widget~~
  * ~~import script and setting up the app~~
  * ~~basic intuition and strucutre~~
  * ~~inside the all important main object;~~
  * ~~html stuff~~
  * ~~components~~
* creating a full spa
  * installation and setup
  * general strcuture differences

Sources and tutorial notes:

Because both spa and widgets are similar. Just differnt strcuture and missing featuers

spa has more featuers and complcation

* app widget
  * <https://www.youtube.com/watch?v=bzlFvd0b65c&list=PLJNLwTPak6dhC5HGSud_mR1Lchhr8mXeT&index=10>
* full spa
  * <https://www.youtube.com/watch?v=ZqgiuPt5QZo>
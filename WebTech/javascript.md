# **Javascript**

---

# **Basics**

===========

# Objects

JSONs basically or a python dictionary

basically an array but you can access by name on top of index

```
let person = {name: "john", age:30};
```

you can access data by dot notation or by square brackets

```
console.log(person.name);
console.log(person['name']);
```

### adding new properties

```
obj.varName = value;
obj['varName'] = value;
```

### deleting properties

```
delete obj.varName;
```

# Ternary Operator

let val = (statement) ? (if true):(if false)

```
let val = 2===2 ? "yes : "no";
console.log(val); // will return yes
```

# **ES6**

---

# let var const

=====================

* ignore var
* just use let to declare variables
* const to declare constants (variables where the value won't change)

```
//declare variables where the value can change
let a = 2;

// declare constant variables where value will not change. 
const pi = 22/7;
```

# Objects

============

### methods in objects

```
let obj = {
  name: "john",
  walk: function() {//walk},
  talk() {// talk}
}
```

# This

=======

literally just a refernce to current object where this is called

this is to be specific in scope when executing code

```
let obj = {
  name: "john",
  getName() {return this.name}
} ;
```

## Binding "this"

```
const obj = {name: "jon", whatIsThis(){console.log this}};
let boundThis = obj.whatIsThis.bind(obj);

// now "this" will always be bound in to the object.
boundThis(); 
```

# Classes

============

essentially object creators. they allow the code to create an object with specifications

```
class person{
  constructior(name){
  this.name = name;
  }

  getName(){
   return name;
  }
}

const john = new person(john);
```

you just class to define how an object is created.

so that you don't have to define it by hand every time.

### The "super" keyword

it's essentially allowing you to call the parent class constructro to help construct a child class

```
class person(){
  constructor(name, age){
    this.name = name;
    this.age = age;
  }
}

class teacher(){
  constructor(name, age, occupation){
    super(name, age)// so that you dont retype the constructor above
    this.occupation = age;
  }
}
```

# Arrow Function

============================

just a tigher fucntion syntax for shorter code. easier to type and read.

```
const square = function(num){return num*num};
const add = (a, b) => {return a+b};
const printTime = () => {console.log(time)};
```

# Modules

================

import and exporting functionalities and data from other js files

literally just making public functions or varibles

### Exporting

```
export const data = 01; 
export default function hello(){console.log("hello")}
export {data as dataVar};
export {data as dataVar, hello};
```

### Importing

```
import {data} from './..';
import hello from './..';
import {dataVar} from './..';
import {dataVar as dataFromFile, hello} from './..';
```

### basically

put export behind funcs/vars to make the importable to other files

export default to mark the main export.

if you do not use use export defautl. import with {object} from '../.';

with export defautl you can omit the curly brackers.

# **ES 2016**

---

# Callbacks

================

essentially functions that are saved to be called in the future

most common example is setTimeout()

```
setTimeout(() => {//this fucntion is saved to be called later}, 1000);
```

# Promises

================

essentially a slight evolution on callbacks

it's a class that accepts 2 callbacks and a fucntion.

1 callback for when the fucntion has an suceeds. another callback for when the fucntion fails.

you decide what are the fail and success conditions

```
const myPromise = new Promise(() => {
  const = Math.floor(Math.random() * 2);
  if(rand === 0){
     resolve(); // call the success path
  }
  else{
    reject(); // call the failure path
  }
});

myPromise().then{console.log("success")}.catch{console.log("failure};
// above will only succeed if number is zero.
```

# Asynchronous Functions

=========================================

functions where you can wait for a slow operation to happen before moving onto the rest of code

```
async function init(){
  download = await fetch('link'); // will wait
  await SlowFunction(); // will wai
  // rest of code runs after awaits
} 

fucntionHere(); // this will run first 
```

* this async function will pause but rest of the app rill run.

### They are also useful for timeouts

letting code wait before executing

```
async function sleep() {
    // code here
    await timeout(3000);  // wait for 3s (3000ms)
    // more code here
}
```
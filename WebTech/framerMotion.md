# **-|- Motion (from Framer)**

===================================================================

Module to help animating html elements that works well with react and react-three-fiber (for 3D stuff).

# **Installation and setup**

===================================================================

##### Installing module into node project

```
npm i framer-motion -save
```

##### Importing module into .js file

```
import {motion} from "framer-motion"
```

# **Basic intuition**

===================================================================

##### Creating a motion component

Instead of using default html divs, use motion's elements

```
<motion.div/> // not <div/>
```

##### The "animate" property

at it's simplest you can just put an entrance animation like so

```
<motion.div
animate={{x: 100}} // will move element by 100px on enter
>
  {children}
</motion.div>
```

The animate property will be like the current animation state. You can put different css style objects in there to change it's state

You can also useState() to sync the div's animation state to property

##### Mental model

It's not keyframe animation. It's all about changing div animation states

# **Motion Animation Properties**

===================================================================

Theres are the html attributes you put in the motion elements

### **Initial**

Creates an initial on mount state that you can transition into your default position

```
<motion.div
intial={{y: -10}} // start element 10 px up on start
animate={{y: 0}} // will animate element to default position start
>
  {children}
</motion.div>
```

### **whileHover, whileTap**

Just like .className:hover. A hovering/click animation state

```
<motion.div
whileHover={{scale: 1.1}} // :hover
whileTap={{scale: 0.9}} // :tap/click
>
  {children}
</motion.div>
```

### **Transition**

this handles all the css timing variables. Like duration, delays and animation curves

```
<motion.div
intial={{y: -10}} // start element 10 px up on start
animate={{y: 0}} // will animate element to default position start
transition={{
  delay: 1, //delays anim by 1 second
  type: "spring", // anim curve type
  duration: 2 // length of animation
}}
>
  {children}
</motion.div>
```

##### Controlling children timings

* delaying children

```
<motion.div
intial={{y: -10}}
animate={{y: 0}} 
transition={{
  delayChildren: 1, //delays children animations
  staggerDirection: -1 // 1 ascending order, -1 descending
}}
>
  {children}
</motion.div>
```

* staggering children

```
<motion.div
intial={{y: -10}}
animate={{y: 0}} 
transition={{
  staggerChildren: 0.1, //staggers children animations
}}
>
  {children}
</motion.div>
```

* When?

```
<motion.div
intial={{y: -10}}
animate={{y: 0}} 
transition={{
  when: "afterChildren" // animations happen after children
  // "beforeChildren" is the opposite
}}
>
  {children}
</motion.div>
```

# **Variants**

==================================================================

Essentially re-useable animation sets. It's a object collection of css states. These states can be plugged in to elements to re-use animation sets throughout code base.

##### Creating variants

Just creat an object. Each sub-object is an animation state.

```
const variantCollection = {
  hidden: {
    y: -1
  }
  visible: {
    y: 0
    transition: {transition variables}
  }
  exit: {
    y:1
  }
}
```

##### Setting variants

Set the variants html attribute. Then pass in animation states as strings the correspond to the variant's sub-object.

```
<motion.div
variants={variantCollection}
intial="hidden"
animate="visible"
>
  {children}
</motion.div>
```

# **📒Keyframes**

==================================================================

* setting keyframes

```
<motion.div
  animate={{ x: [0, 100, 0] }} // just have an array of keyframes
/>
```

* looping controls

Change it in the transition object

```
```

# **📒Enter/Exit animations**

===================================================================

# **📒Transitioning between routes**

===================================================================

# **📒useCycle**

===================================================================

# **📒Dragging**

===================================================================
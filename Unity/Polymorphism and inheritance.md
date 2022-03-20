* using parent or child version of variables and fucntiosn

> # Unity polymorphism/inheritance

# what?

Basically you can create classes that derives functions and behaviours from the parent.

like creating a base interactable class then, creating puzzle interactable class, pickup interactble class.

or creating an animal class then creating dog, cat, ant class.

# How?

```
public class ClassName : ParentClassName
{
    public Start()
    {
        // code
    }
}
```

that's it. just mark the parent class after the declaring the class.

# Accessing parent/child version of data or functions

usually only the child class is accessed by default when you refer to the class instance.

but sometimes you cant to access the parent's instead;

to access the parent's version. just use base

```
base.FunctionName();
base.variableName();
```

# Inheriting MonoBehaviour

most of the time in unity projects you just want to inherit monobehaviors

including the parent's start and update functions.

you can do that by

```
public class ClassName : ParentClassName
{
    public Start()
    {
        base.Start(); //this executes parent's start func
    }

    public Update()
    {
        base.Update(); //this executes parent's Update func
    }
}
```

# Overriding functions

maybe you want a function derived in the parent class. to be called different in all the children.

first you need to make the parent function overridable

```
public virtual void FunctionName(){
  // code here
}
```

just make it public and virtual in the function declaration.

in the child class, to override do this

```
public override void FunctionName(){
  // code here this overrides the parent's function.
}
```
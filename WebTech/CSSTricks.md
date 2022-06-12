# **-|- CSS tricks**

===================================================================

My common css classes

```
/* -------------  My css Stuff */
/* debug */
.debugRedLine              {outline: solid 3px rgba(255, 0, 0, 0.3);}

/* removing default spacings */
*                          {padding: 0;margin: 0;}

/* flex Classes */
.flex                      {display: flex}
.flexColumn                {flex-direction: column;}
/* justify */
.flexJustifyCenter         {justify-content: center;}
.flexJustifyStart          {justify-content: flex-start;}
.flexJustifyEnd            {justify-content: flex-end;}
.flexJustifyBetween        {justify-content: space-between;}
.flexJustifyAround         {justify-content: space-around;}
.flexJustifyEvenly         {justify-content: space-evenly;}
/* alignment */
.flexAlignCenter           {align-items: center;}
.flexAlignStart            {align-items: flex-start;}
.flexAlignEnd              {align-items: flex-end;}
.flexAlignStretch          {align-items: stretch;}
.flexAlignBaseline         {align-items: baseline;}
/* flex-grow */
.flexGrow                  {flex-grow: 1;}

/* sizing divs */
.fillWidth                 {width: 100%;}
.fillHeight                {height: 100%;}
.hugHeight                 {height: fit-content;}
.hugWidth                  {width: fit-content;}

/* spacings */
.padding                   {padding: 1em;}
.paddingHalf               {padding: 0.5em;}
.margin                    {margin: 1em;}

/* visibility */
.hide                      {display: none;}
.fadeOut                   {opacity: 0;}

/* layering over */
.overlay                   {position: absolute;top: 0;left: 0;}
```

## Selectors

**To select children**

```
#.parentClass/id > #.childrenClass/ID
```

**To select based on state**

.elementSelected : status

```
div :: hover
div :: active
div :: focus
```

# **CSS Grid**

===================================================================

### **Generally**

Dividing a <div/> into a grid to place it's children

🌐 <https://css-tricks.com/snippets/css/complete-guide-grid/>

### Grid vs flexbox

flexbox is more *flex*ible. The layout reacts to number of children and their sizes. Think of the pinterest laytout. Grid is a lot more static and defined. The parent div defines the layour rather than the children

##### Using grid and flexbox

Most of the time you layout sections of a site with grid. Then inside each section is laid out by flex box.

### **Usage**

##### Making a grid

in html

```
<div class="parentContainer">
  <div class="childElement"/>
  <div class="childElement"/>
  <div class="childElement"/>
</div>
```

in css put below

```
.parentContainer{
  display: grid;
}
```

##### Setting rows and columns

every measurement is one extra cell

```
.parentContainer{
  display: grid;
  grid-template-columns: 1fr 3fr 1fr; //defines width of columns
  grid template rows: 50px auto 70px; // define heigth of rows
}
```

Handling gaps between grid cells

```
.parentContainer{
  display: grid;
  grid-template-columns: 1fr 3fr 1fr; //defines width of columns
  grid template rows: 50px auto 70px; // define heigth of rows
 
  /*setting grid*/
  gap: {row-gap} {column gap}
  column-gap: 10px;
  row-gap: 1em;
}
```

##### Placing children in the the rows and columns

```
/*define where grid children goes*/
.parentContainer{
  display: grid;
  grid-template-areas: 
  "topbar  topbar   topbar"
  "ads     content  sidebar"
  "footer  footer   footer"
}

/*label children classes*/
.header{grid-area: topbar;}
.aside{grid-area: ads;}
.article{grid-area: content;}
.nav{grid-area: footer;}
.footer{grid-area: footer;}
```

### **Aligning and Justify children**

* in parent (applies to all cells)

```
.parentContainer{
  display: grid;
  grid-template-columns: 1fr 3fr 1fr; //defines width of columns
  grid template rows: 50px auto 70px; // define heigth of rows
 
  align-content: /*works just like flexbox but in children class*/
  justify-content: /*works just like flexbox but in children class*/
}
```

* in children (applies to one children class)

```
.childrenClass{
  align-self: /*works just like flexbox but in children class*/
  justify-self: /*works just like flexbox but in children class*/
}
```

### **Handling sub-grids**
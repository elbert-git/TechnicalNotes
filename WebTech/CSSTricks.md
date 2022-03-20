# CSS tricks

My personal CSS cheatsheet

```
/* utility */
html, body {
	 margin: 0;
	 height: 100%;
	 font-size:1.2em;
	 overflow-x:hidden;
}
.center-child{
	display: flex;
	align-items: center;
	justify-content:center;
	 
	flex-direction: column;
}
.center-text{
	text-align:center;
}
.zero-margin{
	margin: 0;
}
.zero-padding{
	padding: 0;
}
.full-width{
	width: 100%;
}
.full-height{
	height: 100%;
}
.layer-over{
	position: absolute;
	left:0;
	top:0;
	height:100%;
	width: 100%;
}
.redborder{
	border-color: rgba(255, 0, 0, 0.5);
	border-style: solid;
	border-width: 3px;
}
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
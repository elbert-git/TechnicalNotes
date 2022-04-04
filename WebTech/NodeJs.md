# **-=| Node JS |=-**

===================================================================

### In general 

A runtime development for javascript. Allows javascript to run on an OS like windows/linux/mac

instead of just a browser. Allows server programs to be written in javascript

# **Installation**

===================================================================

### Arch

```
sudo pacman -S npm
```

### Ubuntu/Debian

```
sudo apt-get install npm
```

# **Node Version manager**

===================================================================

Sometimes you just need a particular version of node

##### Install nvm

```
sudo apt-get install nvm
```

```
sudo pacman -S install nvm
```

##### Usage

* To list down all available version

```
nvm ls-remote
```

* to install one particular version

```
nvm install [version.number]
```

# **Setting up a node project directory**

===================================================================

```
npm init -y
```

# **Project Structure**

===================================================================

### node_modules

this is where all the node modules are stored for the project.

### package.json

this is the config file. you can put quick npm scripts here.

this also contains a roster of project and development dependencies. 

# **Node modules installation**

===================================================================

### Installing project dependencies

These are modules that are required for the project work on runtime. Like react, a-frame, threejs, vue, firebase

```
npm install {module name} --save
```

### Installing development dependencies

These are modules that help develop or compile the project. not needed on the project's runtime. Like webpack, babel, polyfill

```
npm install {module name} --save-dev
```
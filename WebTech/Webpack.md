# **-|- Webpack**

Bundling javascript modules for front end pages. Essentially how you use the npm modules wihtout react. so you don't need to script tag every module in your html

sources

<https://www.youtube.com/watch?v=CZnmKWgmL7s>

<https://www.youtube.com/watch?v=X1nxTjVDYdQ>

# **Setup**

===================================================================

### Basic node

Start by setting your node project

```
npm init -y
```

we put -y just so that you can skip the configuration step

then

1. make a public/index.html
2. make a src/index.js

### Webpack setup

**install webpack and the cli tool**

```
npm install --save-dev webpack webpack-cli
```

**Add a build script in the package.json**

```
"scripts": {
  "build": "webpack",
  "dev": "webpack --mode development",
  "start": "webpack serve"
}
```

# **Bundling**

===================================================================**Building for Development**

```
npm run dev
```

**Building for Production**

```
npm run build
```

the above will bundle the what you need in to a /dist folder. inside the folder is a main.js file. Development bundle is just a bundle wihtout all the spaces and lines removed.

The above is just running the script object in you package.json

**Make html point to dist/main.js**

```
<script src="../path/to/dist/main.js"/>
```

# **Configuration**

===================================================================

### Creating the config file

Create a 'webpack.config.js' file in the node project root folder.

**Importing path**

```
const path = require('path');
```

### Config structure

it's all in the object called module.exports.

And every category of the settings is an object

```
const path = require('path');
module.exports = {
  mode: 'development', // switch to 'production' for production build
  entry:{ // handles entry point javascript
    main: path.resolve(__dirname, './src/app.js')
  },
  output: { // handles final js bundle output settings
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
}
```

### Source-map

Allows tracing error and logs to their source js files. instead of pointing everything to the main.js

just add this to the webpack config

```
module.exports = {
  devtool: "source-map"
}
```

### Babel setup

Babel helps trans-pile code for older browsers. Allows newer javascript functions to run is most browsers. not just the cutting edge ones

**Installing**

```
npm install --save-dev @babel/core @babel/preset-env babel-loader 
```

**Webpack config**

```
module.exports = {
  // ...
  module:{
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          // without additional settings this will reference .babelrc
          loader: 'babel-loader'
        }
      }
    ]
  }
}
```

**Babelrc**

create a .babelrc file

```
{
  "presets" : ["@babel/preset-env"]
}
```

### Webpack Server

Install the webpack server module

```
npm install webpack-dev-server
```

add dev server configuration to webpack.config

```
devServer: {
  static: {
    directory: path.join(__dirname, 'public')
  }
}
```

add script to package.json

# Polyfill issues

===================================================================

### Why it happens

Webpack can also transpile (downgrade) javascript to work on older browsers. But this process balloons the project up by a ton. So it's an opt-in feature now rather than turned on by default.

### Browserlist

First add a .browserslistrc file and simply add.

```
defaults
```

that's it.

### 1) Importing and setting core-js

these are the core javascript functionalities.

```
npm install --save-dev core-js
```

**.babelrc setup**

just copy below. Remember the double square brackets. Because... just because

```
{
  "presets" : [
    [
      "@babel/preset-env",
      {"debug": true, "useBuiltIns": "usage", "corejs": 3}
    ]
  ]
}
```

### 2) enable polyfill

Use this package

<https://www.npmjs.com/package/node-polyfill-webpack-plugin>

**Install**

```
npm install node-polyfill-webpack-plugin
```

**Usage**\
Add the following to your `webpack.config.js`:

```
const NodePolyfillPlugin = require("node-polyfill-webpack-plugin")

module.exports = {
	// Other rules...
	plugins: [
		new NodePolyfillPlugin()
	]
}
```

# Quick boilerplate

===================================================================

##### node project setup

```
npm init -y
```

```
mkdir src public
touch src/index.js
touch public/index.html
```

##### Installs

```
npm install --save-dev webpack webpack-cli @babel/core @babel/preset-env babel-loader core-js node-polyfill-webpack-plugin
```

##### package.json

add scripts

```
"scripts": {
  "build": "webpack",
  "dev": "webpack --mode development",
  "start": "webpack serve"
}
```

##### webpack.config.js

```
const path = require('path');
const NodePolyfillPlugin = require("node-polyfill-webpack-plugin");
module.exports = {
  mode: 'development', // switch to 'production' for production build
  entry:{ // handles entry point javascript
    main: path.resolve(__dirname, './src/index.js')
  },
  output: { // handles final js bundle output settings
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'public')
  },
  devtool: "source-map",
module:{
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          // without additional settings this will reference .babelrc
          loader: 'babel-loader'
        }
      }
    ]
  },
	plugins: [
		new NodePolyfillPlugin()
	]
}
```

##### .babelrc setup

create .babelrc file

just copy below. Remember the double square brackets. Because... just because

```
{
  "presets" : [
    [
      "@babel/preset-env",
      {"debug": true, "useBuiltIns": "usage", "corejs": 3}
    ]
  ]
}
```
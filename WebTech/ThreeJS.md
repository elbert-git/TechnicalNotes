# What next to learn

\- Handling Animations

\- interatctions and input

\- post processing 

\- ThreeJS and react

\- Miscellaneous

	- 3D Assets folder duplication. Need to be in same place as script.

# **-|- ThreeJS**

===================================================================

### In general

A Javascript wrapper for webGL. Easily render 3d Objects in the scene.

# **Installation**

===================================================================

### Script tag

```
<script async src="https://unpkg.com/es-module-shims@1.3.6/dist/es-module-shims.js"></script>
```

### NPM

```
npm install --save three
```

then import by

```
// Option 1: Import the entire three.js core library.
import * as THREE from 'three';
```

or

```
// Option 2: Import just the parts you need.
import { Scene } from 'three';
```

# **Basic Setup**

===================================================================

```
// --- create scene
const scene = new THREE.Scene();
// create camera, need fovAngle, aspect ratio and near/far clip planes
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth/window.innerHeight, 0.1, 1000 );
// move cam so we can what is in center
camera.position.z = 5;

// --- create renderer
const renderer = new THREE.WebGLRenderer();
// set renderer canvas size
renderer.setSize( window.innerWidth, window.innerHeight );
// Attach renderer to body
document.body.appendChild( renderer.domElement );

// --- Creatingh a basic mesh object
// you need a Geometry object and material
const geometry = new THREE.BoxGeometry();
const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
const cube = new THREE.Mesh( geometry, material );
// add cube to scene
scene.add( cube );


// --- create update loop
function Update() {
  // queuenew frame to render
  requestAnimationFrame( animate );

  // update logic goes here
  // code.....

  // render this current frame
  renderer.render( scene, camera );
};

// Start update loop
Update();
```

# **How objects are structured**

===================================================================

* **Root**
  * **Render**
    * render scene into dom element
  * **Camera**
    * perspective of render
  * **Scene**
    * The root Transform/GameObject
    * **Group**
      * a group of transforms
    * **Mesh**
      * a single mesh object
      * contains geometry and material data
    * **Object3D**
      * tranform node
    * **Light**
      * light object

# **Update loop**

===================================================================

This is the core update loop boiler plate. every fram this fucntion runs. 

anything you need to update. put it here

```
// --- create update loop
function Update() {
  // queuenew frame to render
  requestAnimationFrame( animate );

  // update logic goes here
  // code.....

  // render this current frame
  renderer.render( scene, camera );
};

// Start update loop
Update();
```

# **Loading in GLTFs**

===================================================================

* import loader

```
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
```

* load the file

```
const loader = new GLTFLoader();

loader.load( 'path/to/model.gltf', ( gltf ) => {
    scene.add( gltf.scene );
  }
  undefined,
  ( error ) => {
    console.error( error );
  }
);
```

### Regarding file paths and deployment

**During development**

* Create a 3DAssets folder for loading

put all files that THREEJs loaders have to load here. put the folder into src folder

For some reason THREE js wont load outside of src folder

but during deployment you will need the 3DAssets folder in the public folder

put in src for development then copy to public for deployment to server. 

**During production/deployment/delivery**

of if you just want to put it on a server. 

* Copy 3DAssets folder to public folder

Because you will only upload the public folder

no need to rewrite file paths in .js scripts

# **Interactions**

===================================================================

# 
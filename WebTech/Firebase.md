# **-|- Firebase**

===================================================================

### In General

A simple catch-all back-end implementation

### Source

[NetNinja's firebase 9 tutorial](https://www.youtube.com/playlist?list=PL4cUxeGkcC9jERUGvbudErNCeSZHWUVlb)

# **Installation**

===================================================================

### Installing the cli

```
npm i firebase-cli
```

### Installing firebase

```
npm install firebase
```

# **General Project setup**

===================================================================

* **create project on firebase website**

  Go to the firebase console website and create a new project
* **get project credentials**

  Go to the project settings and you will find the project credentials. you will need it to initialised the firebase client
* **initialise firebase app from client**

  Create firebase.js and put below inside.

```
import {initializeApp} from 'firebase/app';

const firebaseConfig = {// copy from firebase console website};

initializeApp(firebaseConfig)
```

# **Firebase Authentication**

===================================================================

### **In general**

Firebase uses json tokens to verify if a user is logged in. If a valid json token is found in user localstorage, then the user is logged in. Generally firebase auth is just a collections of functions that you call.

### **Setup Auth Methods**

You need to go to the console to enable various authentication methods like via email/password or via google auth.

❗❗❗❗ keep in mind sign out and sign in fucntions are async functions ❗❗❗❗

### **Importing the module**

```
// import module
import {getAuth} from 'firebase/auth';

// get object
const auth = getAuth();
```

### **Usage**

Below will document the usage of using email and password. But will be teh same for all login methods. Just change the method names appropriately according to the docs. 🌐 [link to docs](https://firebase.google.com/docs/auth)

* enabling the email/pass auth.

  Go to firebase console and enable email/pass auth
* registering

```
// import
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";

// register
const auth = getAuth();
createUserWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // Signed in 
    const user = userCredential.user;
    // ...
  })
  .catch((error) => {
    const errorCode = error.code;
    const errorMessage = error.message;
    // ..
  });
```

* signing in

```
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";

const auth = getAuth();
signInWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // Signed in 
    const user = userCredential.user;
    // ...
  })
  .catch((error) => {
    const errorCode = error.code;
    const errorMessage = error.message;
  });
```

* signing out

```
import { getAuth, signOut } from "firebase/auth";

const auth = getAuth();
signOut(auth).then(() => {
  // Sign-out successful.
}).catch((error) => {
  // An error happened.
});
```

### Auth State Persistance

Set whether or not authentication tokens persist from session to session and how.

```
import { getAuth, setPersistence, signInWithEmailAndPassword, browserSessionPersistence } from "firebase/auth";

const auth = getAuth();
setPersistence(auth, browserSessionPersistence)
  .catch((error) => {
    // Handle Errors here.
  });
```

##### List of persistance

```
//will sign out when  closed tab
import {browserSessionPersistence } from 'fireabase/auth';

// inMemoryPersistence - will clear on page reload
import {inMemoryPersistence} from 'fireabase/auth';

// default is local - only a sign out will clear auth
// do nothing
```

# **Firestore Database**

===================================================================

### **General intuition**

Firebase database implementation.

**Structure**

Firestore is a giant folder for storing jsons. It is structured with collections and documents. Think collections as folders and documents and files.

**Document ID**

every document has an id so that you can grab them

### Importing the module

import firestore and get firestore object

```
// import firestore
import {getFirestore} from 'firebase/firestore';

// get firestore object
const db = getFirestore();
```

### **Basic Usage (CRUD)**

* import firestore and get firestore object

```
// import firestore
import {getFirestore} from 'firebase/firestore';

// get firestore object
const db = getFirestore();
```

* reading documents from collection (files from folders)oc

```
// imports
import {getFirestore, collection, getDocs} from 'firebase/firestore';

// get collection reference
const collectionReference = collection(db, 'collectionName')

// get documents from collection
getDocs(collectionReference); //returns whole doc json

// better way of getting data
getDocs(collectionReference).then((snapshot) => {
  let finalArray = [];
  snapshot.docs.forEach((doc) => {
    finalArray.push({...doc.data(), id: doc.id});
  });
}).catch(err => {
  console.log(err);
});
```

* reading a single document

```
// import 
import {getDoc} from 'firebase/firestore';

// get doc reference
cosnt docReference = doc(db, 'collectionName', {documentId});

// get doc
let data = getDoc(db, 'collectionName', {docId});
```

* adding and deleting documents

```
// import 
import {addDoc} from 'firebase/firestore';

// use add Docs
addDoc(collectionReference, {dataJson});
```

* delete documents

```
// import
import {docRef, deleteDoc} from 'firebase/firestore';

// get doc reference
cosnt docReference = doc(db, 'collectionName', {documentId});

// delete doc
deleteDoc(docRef); // keep in mind this is async. 
```

* Updating documents

```
//import
import {updateDoc} from 'firebase/firestore';

// get doc reference
const docReference = doc(db, 'collectionName', {documentId});

// updateDoc
updateDoc(docRef, {keyToUpdate: newValue});
```

### **Real-time data listener**

```
// import onSnapshot
import {onSnapshot} from 'firebase/firestore';

//create event listener
onSnapshot(collectionReference).then((snapshot) => {
  let finalArray = [];
  snapshot.docs.forEach((doc) => {
    finalArray.push({...doc.data(), id: doc.id});
  });
}).catch(err => {
  console.log(err);
});
```

### **Querying data**

* import query() and where()

```
//import query and where
import {query, where} from 'firebase/firestore';
```

* querying

```
const queryData = query(collectionRef, where("key","comparator","value"));

const queryData = query(collectionRef, where("autho","==","C.S Lewis"));
```

* Accessing data from query

```
getDocs(queryData).then((snapshot) => {
  let finalArray = [];
  snapshot.docs.forEach((doc) => {
    finalArray.push({...doc.data(), id: doc.id});
  });
}).catch(err => {
  console.log(err);
});
```

### **Sorting Data**

* Creating an index

You need to create something called an index before you can sort stuff. For now just try the function once then It will give you a an error and a link to create an index automatically. Go to the link and create the index. Wait a few minutes then it should work once the index is enabled.

* import orderBy

```
// import
import {orderBy} from 'firebase/firestore';
```

* create a query

```
const queryData = query(collectionRef, where("key","comparator","value"));

const queryData = query(collectionRef, orderBy('key', 'desc/asc'));
```

* read query data

```
getDocs(queryData).then((snapshot) => {
  let finalArray = [];
  snapshot.docs.forEach((doc) => {
    finalArray.push({...doc.data(), id: doc.id});
  });
}).catch(err => {
  console.log(err);
});
```

### **TimeStamps**

* import server timestamp

```
import {serverTimestamp} from 'firebase/firestore';
```

* use fucntion

```
let time = serverTimestamp();
```

# **Firebase Functions**

===================================================================

# **Firebase rules and security**

===================================================================
# Firebase

## Config Setup Example

```js
import * as firebase from "firebase/app";

import "firebase/auth";
import "firebase/database";
import "firebase/storage";

// ADD YOUR FIREBASE CONFIG OBJECT HERE:
var firebaseConfig = {
  apiKey: "",
  authDomain: "",
  databaseURL: "",
  projectId: "",
  storageBucket: "",
  messagingSenderId: "",
  appId: ""
};

const firebaseApp = firebase.initializeApp(firebaseConfig);
const firebaseAuth = firebaseApp.auth();
const firebaseDb = firebaseApp.database();
const firebaseStorage = firebaseApp.storage();

export { firebaseAuth, firebaseDb, firebaseStorage };
```

## Image Upload

```js
const storageRef = firebaseStorage.ref();

storageRef
  .child(`images/${name}`)
  .put(file)
  .then(snapshot => snapshot.ref.getDownloadURL())
  .then(url => {
    console.log(url);
    this.lastUploadUrl = url;
  })
  .catch(console.error);
```

## Vue Plugin Setup

```js
import * as firebase from "firebase/app";

import "firebase/auth";
import "firebase/database";
import "firebase/storage";
import "firebase/firestore";

// ADD YOUR FIREBASE CONFIG OBJECT HERE:
var firebaseConfig = {
  apiKey: "{apiKey}",
  authDomain: "jamstack-api.firebaseapp.com",
  databaseURL: "https://jamstack-api.firebaseio.com",
  projectId: "jamstack-api",
  storageBucket: "jamstack-api.appspot.com",
  messagingSenderId: "844489125366",
  appId: "1:844489125366:web:32d92a90517a0f6a"
};

const fireApp = firebase.initializeApp(firebaseConfig);
const fireAuth = fireApp.auth();
const fireDB = fireApp.database();
const fireStorage = fireApp.storage();
const fireStoreDB = fireApp.firestore();
const GoogleProvider = new firebase.auth.GoogleAuthProvider();
console.log(fireStoreDB);

export { GoogleProvider, fireApp, fireAuth, fireDB, fireStorage, fireStoreDB };

export default ({ Vue }) => {
  Vue.prototype.$fireApp = fireApp;
  Vue.prototype.$fireAuth = fireAuth;
};
```

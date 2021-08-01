# Firebase

## Setup

- Create at least 2 different firebase projects: development and production.
- Make sure to disable localhost in the authorized domains section for the
  production version.
- Create a `.env.local` file and set up the environment variables like this:

~~~
// no need to set the value as a string
REACT_APP_FIREBASE_API_KEY=...
~~~

- Install firebase:

~~~
npm i firebase
~~~


- Create a `firebase.js` file

~~~
import firebase from "firebase/app";
import "firebase/auth";

const app = firebase.initializeApp({
  apiKey: process.env.REACT_APP_FIREBASE_API_KEY,
  authDomain: process.env.REACT_APP_FIREBASE_AUTH_DOMAIN,
  ...
});

export const auth = app.auth();
export default app
~~~

## Deploy

~~~
npm i -g firebase-tools
firebase login:ci

// copy the token somewhere safe
~~~

~~~
firebase init
hosting > use an existing project > build > No > 
configure as a single page app
npm run build
firebase deploy
~~~

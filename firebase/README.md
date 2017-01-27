# Firebase2 - Cookbook
  Firebase settings 

- Index
  + How to Install
  + Install Packages



### How to Install

```
  npm i firebase angularfire2 --save
```
##### index.html 
ps: See in the firebase ( WEB )
```
  <script src="https://www.gstatic.com/firebasejs/3.6.7/firebase.js"></script>
``` 



##### app.module.ts
```
  // firebase 
  import { AngularFireModule } from 'angularfire2';
  import { firebaseConfig } from './environments/firebaseconfig.ts';
  declare var firebase: any;
  
  imports: [  AngularFireModule.initializeApp( firebaseConfig ) ] 
```

##### environments/firebaseconfig.ts
```

 export const firebaseConfig = {
     apiKey: "AIzaSyAy9mjhz3tB-loI3crIMYPGkUodjfauXDM",
     authDomain: "loianekk.firebaseapp.com",
     databaseURL: "https://loianekk.firebaseio.com",
     storageBucket: "loianekk.appspot.com",
     messagingSenderId: "698017949259"
   };
     firebase.initializeApp(firebaseConfig);

```




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
ps: Take it in the firebase ( WEB )
```html
  <script src="https://www.gstatic.com/firebasejs/3.6.ksksksksks7/firebase.js"></script>
``` 


### NEW method

##### app.module.ts
```js
import { environment } from './../environments/environment';
// firebase 
import { AngularFireModule } from 'angularfire2';
 
  imports: [  AngularFireModule.initializeApp(environment.firebase),

```

##### environments/  

In the 2 environments files add what you want 
```js

export const environment = {
  production: false,
  firebase: {
     apiKey: ' Use single quotes here...', 
     authDomain: ' xxxxxxxxxxxxxxxxxxx ', 
     databaseURL: ' xxxxxxxxxxxxxxxxxx  ', 
     storageBucket: ' xxxxxxxxxxxxxxxx ',
     messagingSenderId: ' xxxxxxxxxxx ' 
  }
  MY_API: 'api info'
};

``` 

In the .services  files that will use the MY_API

```js
import { environments } from '../path';

export const MY_API = environment.MY_API;

``` 


### Old Method

##### app.module.ts
```js
  // firebase 
  import { AngularFireModule } from 'angularfire2';
  import { firebaseConfig } from '../environments/firebaseconfig';
  declare var firebase: any;
  
  imports: [  AngularFireModule.initializeApp( firebaseConfig ) ] 
```

##### environments/firebaseconfig.ts 
### OLD method
```js

 export const firebaseConfig = {
     apiKey: ' Use single quotes here...', 
     authDomain: ' xxxxxxxxxxxxxxxxxxx ', 
     databaseURL: ' xxxxxxxxxxxxxxxxxx  ', 
     storageBucket: ' xxxxxxxxxxxxxxxx ',
     messagingSenderId: ' xxxxxxxxxxx ' 
   };
     firebase.initializeApp(firebaseConfig);

```


### How to Deploy

First install the firebase-tools
```
sudo npm i -g firebase-tools
``` 
With --prod flag ( minify + uglify ) the application

```
ng build --env=prod
``` 

# Deploy Steps 

```
ng build --prod
```

```
firebase login
```

```
firebase init 
> dist
> y
// or overwrite ? N
> y
``` 
```
firebase deploy 
``` 


#### need help
```
firebase deploy --help
``` 





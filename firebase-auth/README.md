# Firebase Authentication - Cookbook

### Updated -  May 2017

#### angularfire2 V4
https://github.com/angular/angularfire2




### How to Install

```
  npm i firebase angularfire2 --save
```

##### index.html 
ps: Take it in the firebase ( WEB )
```html
  <script src="https://www.gstatic.com/firebasejs/3.6.ksksksksks7/firebase.js"></script>
``` 

##### app.module.ts
```js

  // firebase 
  import { AngularFireModule } from 'angularfire2';
  // firebase database
  import { AngularFireDatabaseModule, AngularFireDatabase, FirebaseListObservable } from 'angularfire2/database';
  // firebase auth system
  import { AngularFireAuthModule, AngularFireAuth } from 'angularfire2/auth';
  import { firebaseConfig } from '../environments/firebaseconfig';

  import * as firebase from 'firebase/app';

  
  imports: [  AngularFireModule.initializeApp( firebaseConfig.firebase ) ] 
  // Or use like this.
  imports: [  AngularFireModule.initializeApp( firebaseConfig.firebase, 'my-app-name' ) ] 
  
```



##### environments/firebaseconfig.ts
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

### Components tree

```
ng g component auth
```
inside the auth component create the rest of components
cd src/app/auth/

``` 
ng g c signup -> or register. Sign Up a new user

ng g c email  -> login with email

ng g c login  -> welcome page with login with email , login with facebook , login with google ...

```


### SIGNUP

#### signup.html
```html
    <form #formRegister='ngForm'>
       <div class="input-field col s12">
         <input type="email" class="validate" name="email" (ngModel)="email" required>
         <label for="email" align="left">Email</label>
       </div>
       <div class="input-field col s12">
         <input id="Password" type="password" class="validate" name="password" (ngModel)="password" required>
         <label for="Password"  align="left">Password</label>
       </div>
       <p>
         <input type="checkbox" id="test5" required/>
         <label for="test5"><a href="#modal1">I agree to the terms</a></label>
       </p>
       <br>
          <a type="submit" class="waves-effect waves-light btn col s12 m12 l12" *ngIf="formRegister.valid" (click)="onSubmit(formRegister)" >Register <i class="material-icons">send</i></a>
       <br>
       <br>
    </form>
```


#### signup.component.ts
```js

import { FormsModule, ReactiveFormsModule, FormGroup, FormBuilder } from '@angular/forms';
import { AngularFireAuth } from 'angularfire2/auth';
import * as firebase from 'firebase/app';

import { Observable } from 'rxjs/Observable';


    isLoggedIn: boolean = false;
    state: string = '';
    error: any;
    okMessage: any;
    email: any;
    password: string;
    formRegister: FormGroup;

    constructor(private afAuth: AngularFireAuth,private router: Router,private fb: FormBuilder) {
          // FormRegister
              this.formRegister = this.fb.group({
                email: this.email,
                password: this.password
                });
     }

  // Register using Email and Pass
  onSubmit(formRegister) {
    if (formRegister.valid) {
      console.log(formRegister.value);
      this.afAuth.auth.createUserWithEmailAndPassword(formRegister.value.email,formRegister.value.password
      ).then(
        (success) => {
          console.log(success);
          this.router.navigate(['/dashboard']);
        }).catch(
        (err) => {
          this.error = err;
        });
    }
    }

``` 
Now that we can create new user's. Let's go to Email -> Login with Email.

ps: Go to console.firebase and "Enable" the email option. Check the Firebase "Rules".


### EMAIL

#### email.component.html
```html
 <form [formGroup]="formLogin" >
    <div class="input-field col s12">
      <input type="email" class="validate" name="email" formControlName="email" required>
      <label for="email" align="left">Email</label>
    </div>
    <div class="input-field col s12">
      <input id="Password" type="password" class="validate" name="password" formControlName="password" required>
      <label for="Password"  align="left">Password</label>
    </div>
    <div class="input-field col s12">
       <a type="submit" class="waves-effect waves-light btn col s12 m12 l12" *ngIf="formLogin.valid"(click)="onSubmit(formLogin)">Login</a>
       <br>
       <br>
       <br>
       <br>
    </div>
  </form>
``` 


#### email.component.ts
```js

import { FormsModule, ReactiveFormsModule, FormGroup, FormBuilder } from '@angular/forms';
import { AngularFireAuth } from 'angularfire2/auth';
import * as firebase from 'firebase/app';

import { Observable } from 'rxjs/Observable';


    isLoggedIn: boolean = false;
    state: string = '';
    error: any;
    okMessage: any;
    email: any;
    password: string;
    formLogin: FormGroup;

    constructor(private afAuth: AngularFireAuth,private router: Router,private fb: FormBuilder) {
          // FormLogin
              this.formLogin = this.fb.group({
                email: this.email,
                password: this.password
                });
     }

 
 // Login with Email V4
  onSubmit(formLogin) {
    if(formLogin.valid) {
      console.log(formLogin.value);
       this.afAuth.auth.signInWithEmailAndPassword(formLogin.value.email, formLogin.value.password
      ).then(
        (success) => {
        console.log(success);
        this.router.navigate(['/dashboard']);
      }).catch(
        (err) => {
        console.log(err);
        this.error = err;
      });
    }
   }

```

### LOGIN Page 

#### login.component.html

```html

<!-- Modal Structure -->
<div id="modal1" class="modal">
  <div class="modal-content">
    <h4>Email Details</h4>
    <p>If you have a FACEBOOK account and your email is from google. ex. @gmail.com . <br> Try to login using google </p>
  </div>
</div>

<div class="row">
  <br>
  <br>
  <div class="col m4 l3"></div>
  <div class="col s12 m6 l6 card blue-grey lighten-3">
    <div class="blue-grey lighten-3">
      <br>
      <a class="waves-effect waves-light white-text" [routerLink]="['/']">Back to Home </a>
      <!-- Modal Trigger -->
      <a class="waves-effect waves-light right white-text" href="#modal1"><i class="material-icons">info_outline</i></a>
      <div class="center">
        <h3 class="white-text">Login</h3>
        <a class="waves-effect waves-light white-text" [routerLink]="['/auth/signup']">Don't have a account ? click here </a>
      </div>
      <!-- <span class="card-title">Card Title</span> -->
      <!-- <img id="lock" src="../assets/lock.svg" alt="lock"  width="55"> -->
      <div align="center">
        <span class="error" *ngIf="error">{{ error }}</span>
      </div>
    </div>
    <div class="input-field col s12">
      <br>
      <br>
      <a type="submit" class="waves-effect waves-light btn col s12 m12 l12 grey lighten-1 z-depth-2" [routerLink]="['/auth/email']">Login Email</a>
      <br>
      <br>
      <br>
      <a type="submit" class="waves-effect waves-light btn col s12 m12 l12 red z-depth-4" (click)="loginG()">Login Google</a>
      <br>
      <br>
      <br>
      <a type="submit" class="waves-effect waves-light btn col s12 m12 l12 blue darken-3 z-depth-2" (click)="signInWithFacebook()">Login Facebook</a>
      <br>
      <br>
      <br>
    </div>
  </div>
</div>

``` 

#### login.component.ts
```js
import { FormsModule, ReactiveFormsModule, FormGroup, FormBuilder } from '@angular/forms';
import { AngularFireAuth } from 'angularfire2/auth';
import * as firebase from 'firebase/app';

import { Observable } from 'rxjs/Observable';


    isLoggedIn: boolean = false;
    state: string = '';
    error: any;
    okMessage: any;
    email: any;
    password: string;
    formLogin: FormGroup;

    constructor(private afAuth: AngularFireAuth,private router: Router,private fb: FormBuilder) { }

   // Anonymosyly Login  --> Enable in firebase login method too.
   anonymously() {
    this.afAuth.auth.signInAnonymously();
    this.router.navigate(['/dashboard']);
    console.log('auth anony');
  }

  // Login Facebook
 signInWithFacebook() {
    this.afAuth.auth.signInWithPopup( new firebase.auth.FacebookAuthProvider())
    .then(
         (success) => {
         this.router.navigate(['/dashboard']);
         }).catch(
           (err) => {
             this.error = err;
           });
  }

```




### COMPONENTS Where you will use the auth system.

```js
import { AngularFireAuth } from 'angularfire2/auth';
import * as firebase from 'firebase/app';


export class MEUCOMPONENT {

  user: Observable<firebase.User>;
  email: any;
  displayName: string;
  uid: any;
  photo: any;

  constructor(public router: Router,public afAuth: AngularFireAuth) { 
     
        afAuth.authState.subscribe(user => {
          if (!user) {
            this.displayName = null;        
            return;
          }
          this.displayName = user.displayName;      
          this.email = user.email;
          this.uid = user.uid;
          this.photo = user.photoURL;
        });


  }

 
 signOut() {
    this.afAuth.auth.signOut();
    this.router.navigate(['/']);
    console.log('Logout');
  }

  

}

```  



#### Check CanActivate methods in the end...























## Old Methods below

- Index
  + How to 
  + Files


### How to Install

```
  npm i firebase angularfire2 --save
```

##### index.html 
ps: Take it in the firebase ( WEB )
```html
  <script src="https://www.gstatic.com/firebasejs/3.6.ksksksksks7/firebase.js"></script>
``` 

##### app.module.ts
```js
  // firebase 
  import { AngularFireModule } from 'angularfire2';
  import { firebaseConfig } from '../environments/firebaseconfig';
  declare var firebase: any;
  
  imports: [  AngularFireModule.initializeApp( firebaseConfig ) ] 
```

##### environments/firebaseconfig.ts
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
### Components tree

```
ng g component auth
```
inside the auth component create the rest of components
cd src/app/auth/

``` 
ng g c login  -> welcome page with login with email , login with facebook , login with google ...

ng g c signup -> or register. Sign Up a new user

ng g c email  -> login with email
```

In the src/app/auth

Create 2 new files.

auth.module.ts

auth.routing.ts

auth.service.ts

auth-guard.service.ts


#### auth.module.ts
```js
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule, ReactiveFormsModule, FormGroup, FormBuilder } from '@angular/forms';

import { AuthComponent } from './auth.component';
import { AuthRoutingModule } from './auth.routing.module';

import { LoginComponent } from './login/login.component';
import { SignupComponent } from './signup/signup.component';
import { EmailComponent } from './email/email.component';
import { AuthService } from './auth.service';
import { AuthGuardService } from './auth-guard.service';

@NgModule({
  imports: [CommonModule , AuthRoutingModule , FormsModule , ReactiveFormsModule],
  declarations: [ AuthComponent, LoginComponent, SignupComponent, EmailComponent ],
  providers: [ AuthService , AuthGuardService ]
})
export class AuthModule { }
``` 
### Notes

All components from auth system use this methods and inputs.

```js
import { FormsModule, ReactiveFormsModule, FormGroup, FormBuilder } from '@angular/forms';
import { AngularFire , AuthMethods, AuthProviders } from 'angularfire2';
import { Observable } from 'rxjs/Observable';

    isLoggedIn: boolean = false;
    state: string = '';
    error: any;
    email: any;
    password: string;
    formLogin: FormGroup;

    constructor(public af: AngularFire, private router: Router,private fb: FormBuilder) { }

``` 



### SIGNUP

#### signup.html
```html
    <form #formRegister='ngForm'>
       <div class="input-field col s12">
         <input type="email" class="validate" name="email" (ngModel)="email" required>
         <label for="email" align="left">Email</label>
       </div>
       <div class="input-field col s12">
         <input id="Password" type="password" class="validate" name="password" (ngModel)="password" required>
         <label for="Password"  align="left">Password</label>
       </div>
       <p>
         <input type="checkbox" id="test5" required/>
         <label for="test5"><a href="#modal1">I agree to the terms</a></label>
       </p>
       <br>
          <a type="submit" class="waves-effect waves-light btn col s12 m12 l12" *ngIf="formRegister.valid" (click)="onSubmit(formRegister)" >Register <i class="material-icons">send</i></a>
       <br>
       <br>
    </form>
```


#### signup.component.ts
```js
// Signup Complete
  onSubmit(formRegister) {
        if (formRegister.valid) {
          console.log(formRegister.value);
          this.af.auth.createUser({
            email: formRegister.value.email,
            password: formRegister.value.password
          }).then(
            (success) => {
              console.log(success);
              this.router.navigate(['/docs']);
            }).catch(
              (err) => {
                this.error = err;
              });
        }
    }

```
ps: Go to console.firebase and "ACTIVATE" the email option. Check the "Rules"

Now that we can create new user's. Let's go to Email -> Login with Email

### EMAIL

#### email.component.html
```html
 <form [formGroup]="formLogin" >
    <div class="input-field col s12">
      <input type="email" class="validate" name="email" formControlName="email" required>
      <label for="email" align="left">Email</label>
    </div>
    <div class="input-field col s12">
      <input id="Password" type="password" class="validate" name="password" formControlName="password" required>
      <label for="Password"  align="left">Password</label>
    </div>
    <div class="input-field col s12">
       <a type="submit" class="waves-effect waves-light btn col s12 m12 l12" *ngIf="formLogin.valid"(click)="onSubmit(formLogin)">Login</a>
       <br>
       <br>
       <br>
       <br>
    </div>
  </form>
``` 


#### email.component.ts
```js

import { FormsModule, ReactiveFormsModule, FormGroup, FormBuilder } from '@angular/forms';
import { AngularFire , AuthMethods, AuthProviders } from 'angularfire2';
import { Observable } from 'rxjs/Observable';

    state: string = '';
    error: any;
    email: any;
    password: string;
    formLogin: FormGroup;
    constructor(private router: Router,private fb: FormBuilder,public af: AngularFire) {

      // LoginForm
     this.formLogin = this.fb.group({
      email: this.email,
      password: this.password
      });


      // end of constructor
    }


 // SIGNIN WORKING
    onSubmit(formLogin) {
      console.log('clicked formLogin');
    if(formLogin.valid) {
      console.log(formLogin.value);
      this.af.auth.login({
        email: formLogin.value.email,
        password: formLogin.value.password
      },
      {
        provider: AuthProviders.Password,
        method: AuthMethods.Password
      }).then(
        (success) => {
        console.log(success);
        this.router.navigate(['/docs']);
      }).catch(
        (err) => {
        console.log(err);
       this.error = err;
      });
    }
   }
``` 

At this moment, we can Register and Login with this new user.
Now we go to auth.service.ts to create
- Logout 
- Facebook Auth
- Google Auth
- Anonymous Auth
To do it is just change the provider and method.
AuthProviders.Anonymous, AuthMethods.Anonymous.

and see if the user is currentUser and it's authenticated()




#### auth.service.ts
in this service we will use.

import { FirebaseAuthState , AngularFireAuth } from 'angularfire2';

```js

import { Injectable } from '@angular/core';
import { Router } from '@angular/router';
import { AngularFire ,  AuthMethods, AuthProviders ,FirebaseAuthState , AngularFireAuth } from 'angularfire2';
import { Observable } from 'rxjs/Observable';

import 'rxjs/add/operator/take';
import 'rxjs/add/operator/map';



/////////////////////////////////////////////////////////////////////////////
//  Here in auth.service.ts
//
//  currentUser()
//  loginGoogle()
//  loginFacebook()
//  logout()
//  isAutenticated()  -> Guards
//
// LOGIN E REGISTER wanna stay in respective components
///////////////////////////////////////////////////////////////////////////////


@Injectable()
export class AuthService {

  isLoggedIn: boolean = false;
  name: string;
  email: string;
  photoUrl?: string;
  uid: any;
  error: any;
  FirebaseAuthState: FirebaseAuthState;
  // user_photo?: any;

    constructor(public af: AngularFire, private router: Router ) {

      // W.O.R.K.I.N.G currentUser() and state
      let user = this.currentUser().subscribe( user => {
        if (user && this.af.auth) {
        this.isLoggedIn = true;
        user = user;
        // this.photoUrl = user.photoURL;
        // this.user_photo = this.af.auth.google.photoURL;
      }
    });

      // end constructor
      }



  currentUser(): Observable<FirebaseAuthState> {
    this.isLoggedIn = true;
    return this.af.auth;
  }


  logout() {
    console.log('Logout service');
      this.af.auth.logout();
   }

   loginG() {
    return this.af.auth.login({
      provider: AuthProviders.Google,
      method: AuthMethods.Popup,
    }).then(
      (success) => {
      this.router.navigate(['/docs']);
      // this.photoUrl = this.af.auth.google.photoUrl;
      }).catch(
        (err) => {
          this.error = err;
        });
   }

   loginFace() {
       return this.af.auth.login({
         provider: AuthProviders.Facebook,
         method: AuthMethods.Popup,
       }).then(
         (success) => {
         this.router.navigate(['/docs']);
         }).catch(
           (err) => {
             this.error = err;
           });
   }




// used in CanActivated Guards
  isAutenticated() : Observable<boolean> {
    return this.af.auth
      .take(1)
      .map( (authState: FirebaseAuthState) => !!authState);
  }


  ////////////////////////////////////////////////////////////////////////////
  // PROVIDER'S SCHEMA
  //  Remember use providers
  // const firebaseAuthConfig = [
  //   { providers: AuthProviders.Password, methods: AuthMethods.Popup },
  //   { providers: AuthProviders.Google, methods: AuthMethods.Popup },
  //   { providers: AuthProviders.Facebook, methods: AuthMethods.Popup },
  //  ];
  //////////////////////////////////////////////////////////////////////////////

}


``` 

### Login Page


#### login.component.html
```html


<!-- Modal Structure -->
<div id="modal1" class="modal">
  <div class="modal-content">
    <h4>Email Details</h4>
    <p>If you have a FACEBOOK account and your email is from google. ex. @gmail.com . <br> Try to login using google </p>
  </div>
</div>

<div class="row">
  <br>
  <br>
  <div class="col m4 l3"></div>
  <div class="col s12 m6 l6 card blue-grey lighten-3">
    <div class="blue-grey lighten-3">
      <br>
      <a class="waves-effect waves-light white-text" [routerLink]="['/']">Back to Home </a>
      <!-- Modal Trigger -->
      <a class="waves-effect waves-light right white-text" href="#modal1"><i class="material-icons">info_outline</i></a>
      <div class="center">
        <h3 class="white-text">Login</h3>
        <a class="waves-effect waves-light white-text" [routerLink]="['/auth/signup']">Don't have a account ? click here </a>
      </div>
      <!-- <span class="card-title">Card Title</span> -->
      <!-- <img id="lock" src="../assets/lock.svg" alt="lock"  width="55"> -->
      <div align="center">
        <span class="error" *ngIf="error">{{ error }}</span>
      </div>
    </div>
    <div class="input-field col s12">
      <br>
      <br>
      <a type="submit" class="waves-effect waves-light btn col s12 m12 l12 grey lighten-1 z-depth-2" [routerLink]="['/auth/email']">Login Email</a>
      <br>
      <br>
      <br>
      <a type="submit" class="waves-effect waves-light btn col s12 m12 l12 red z-depth-4" (click)="loginG()">Login Google</a>
      <br>
      <br>
      <br>
      <a type="submit" class="waves-effect waves-light btn col s12 m12 l12 blue darken-3 z-depth-2" (click)="loginFace()">Login Facebook</a>
      <br>
      <br>
      <br>
    </div>
  </div>
</div>

``` 





#### login.component.ts
```js
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';
import { FormsModule, ReactiveFormsModule, FormGroup, FormBuilder } from '@angular/forms';

import { AngularFire , AuthMethods, AuthProviders } from 'angularfire2';

import { AuthService } from '../auth.service';
import { Observable } from 'rxjs/Observable';
declare var $: any;



  constructor(private authS: AuthService, private router: Router,private fb: FormBuilder,public af: AngularFire) {  }


   // Google frontend
   photoUrl?: any;
   loginG() {
    return this.authS.loginG();
   }

  // Facebook frontend
  loginFace() {
    return this.authS.loginFace();

  }
``` 


### CanActivave
To Use RouteGuards to the routes.

STEPS
1 - auth-guard.service.ts
2 - auth.service.ts
3 - import this 2 files in the app.module.ts


#### auth-guard.service.ts
```js

import { Injectable } from '@angular/core';
import { CanActivate , Router } from '@angular/router';


import { FirebaseAuthState , AngularFire } from 'angularfire2';
import { AuthService } from './auth.service';
import { Observable } from 'rxjs/Observable';
import 'rxjs/add/operator/do';

@Injectable()
export class AuthGuardService {

  constructor(private authS: AuthService,
              public af: AngularFire,
              private router: Router) {
    //  console.log(this.af.auth);
   }

 user: FirebaseAuthState;

 canActivate(): Observable<boolean> {
          console.log('Route Guards !! :< ');
         return this.authS.isAutenticated().do( authenticated => {
           if (!authenticated) this.router.navigate(['/auth/login']);
         });
   }

   // in the ROUTES:
   // canActivate: [ AuthGuardService ]



}
```


#### auth.service.ts
```js


import { FirebaseAuthState , AngularFireAuth } from 'angularfire2';

// used in CanActivated Guards
  isAutenticated() : Observable<boolean> {
    return this.af.auth
      .take(1)
      .map( (authState: FirebaseAuthState) => !!authState);
  }

```

#### app.routing.ts
use the canActivate: [ AuthGuardService ] 

```js

import { AuthGuardService } from './auth/auth-guard.service';

{ path: 'users',
    loadChildren: 'app/users/users.module#UsersModule' , canActivate: [ AuthGuardService ]
 },
```


#### app.module.ts
```js

import { AuthService } from './auth/auth.service';
import { AuthGuardService } from './auth/auth-guard.service';

// I put to stop the fromPromise ERROR.
import { Observable } from 'rxjs/Observable';


providers: [ AuthService , AuthGuardService ],



``` 



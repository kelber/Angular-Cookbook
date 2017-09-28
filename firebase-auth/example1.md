
### Authentication > May 2017
https://angularfirebase.com/lessons/angular-firebase-authentication-tutorial-oauth/


1 - Firebase enable
2 - 
ng g service core/auth
ng g component users/user-login
ng g component users/user-profile



OBS: 1 - Create  "getters"  to turn it more easy ...
https://www.typescriptlang.org/docs/handbook/classes.html   
// cod3r courses.

##### service.ts
```js
// Returns true if user is logged in
get authenticated(): boolean {
  return this.authState !== null;
}

// Returns current user
get currentUser(): any {
  return this.authenticated ? this.authState.auth : null;
}

// Returns current user UID
get currentUserId(): string {
  return this.authenticated ? this.authState.uid : '';
}
```

if you  want to save your user records the firebase realtime database. It can be useful if you plan on iterating over users in your app or if you collection custom data on users. It’s can also be setup as a resuable function.

```js
private updateUserData(): void {
  let path = `users/${this.currentUserId}`; // Endpoint on firebase
  let data = {
               name: this.currentUser.displayName,
               email: this.currentUser.email,
             }
  this.db.object(path).update(data)
  .catch(error => console.log(error));
}
```


##### component.ts
we are going to create a separate method for each provider. Just like in the service, we will add a reusable function called afterSignIn that will execute after the service finishes logging in the user. For now, we will just have the router to redirect the user to the home page.

```js

private afterSignIn(): void {
  // Do after login stuff here, such router redirects, toast messages, etc.
  this.router.navigate(['/']);
}



  signInWithGoogle(): void {
    this.auth.googleLogin()
      .then(() => this.afterSignIn());
  }
  ```


  #### html
  ```html
  <div *ngIf="!auth.currentUser; else alreadyLoggedIn">
<button (click)="signInWithGoogle()">
  Connect Google
</button>
<ng-template #alreadyLoggedIn>
    already logged in!
</ng-template>
```




/// CODIGOS SEPARADOS


```js
import { Injectable } from '@angular/core';
import { Router } from "@angular/router";
import { AngularFireDatabaseModule, AngularFireDatabase, FirebaseListObservable } from 'angularfire2/database';
import { AngularFireAuth } from 'angularfire2/auth';
import * as firebase from 'firebase';


@Injectable()
export class AuthService {

  authState: any = null;

  constructor(private afAuth: AngularFireAuth,
              private db: AngularFireDatabase,
              private router:Router) {

            this.afAuth.authState.subscribe((auth) => {
              this.authState = auth
            });
          }

  // Returns true if user is logged in
  get authenticated(): boolean {
    return this.authState !== null;
  }

  // Returns current user data
  get currentUser(): any {
    return this.authenticated ? this.authState : null;
  }

  // Returns
  get currentUserObservable(): any {
    return this.afAuth.authState
  }

  // Returns current user UID
  get currentUserId(): string {
    return this.authenticated ? this.authState.uid : '';
  }

  // Anonymous User
  get currentUserAnonymous(): boolean {
    return this.authenticated ? this.authState.isAnonymous : false
  }

  // Returns current user display name or Guest
  get currentUserDisplayName(): string {
    if (!this.authState) { return 'Guest' }
    else if (this.currentUserAnonymous) { return 'Anonymous' }
    else { return this.authState['displayName'] || 'User without a Name' }
  }

  //// Social Auth ////


  refatoradoKELBERAuthFacebook() {
    this.afAuth.auth.signInWithPopup(  new firebase.auth.FacebookAuthProvider());
  }
  
  githubLogin() {
    const provider = new firebase.auth.GithubAuthProvider()
    return this.socialSignIn(provider);
  }

  googleLogin() {
    const provider = new firebase.auth.GoogleAuthProvider()
    return this.socialSignIn(provider);
  }
  


  facebookLogin() {
    const provider = new firebase.auth.FacebookAuthProvider()
    return this.socialSignIn(provider);
  }

  twitterLogin(){
    const provider = new firebase.auth.TwitterAuthProvider()
    return this.socialSignIn(provider);
  }

  private socialSignIn(provider) {
    return this.afAuth.auth.signInWithPopup(provider)
      .then((credential) =>  {
          this.authState = credential.user
          this.updateUserData()
      })
      .catch(error => console.log(error));
  }


  //// Anonymous Auth ////

  anonymousLogin() {
    return this.afAuth.auth.signInAnonymously()
    .then((user) => {
      this.authState = user
      this.updateUserData()
    })
    .catch(error => console.log(error));
  }

  //// Email/Password Auth ////

  emailSignUp(email:string, password:string) {
    return this.afAuth.auth.createUserWithEmailAndPassword(email, password)
      .then((user) => {
        this.authState = user
        this.updateUserData()
      })
      .catch(error => console.log(error));
  }

  emailLogin(email:string, password:string) {
     return this.afAuth.auth.signInWithEmailAndPassword(email, password)
       .then((user) => {
         this.authState = user
         this.updateUserData()
       })
       .catch(error => console.log(error));
  }

  // Sends email allowing user to reset password
  resetPassword(email: string) {
    var auth = firebase.auth();

    return auth.sendPasswordResetEmail(email)
      .then(() => console.log("email sent"))
      .catch((error) => console.log(error))
  }


  //// Sign Out ////

  signOut(): void {
    this.afAuth.auth.signOut();
    this.router.navigate(['/'])
  }


  //// Helpers ////

  private updateUserData(): void {
  // Writes user name and email to realtime db
  // useful if your app displays information about users or for admin features

    let path = `users/${this.currentUserId}`; // Endpoint on firebase
    let data = {
                  email: this.authState.email,
                  name: this.authState.displayName
                }

    this.db.object(path).update(data)
    .catch(error => console.log(error));

  }




}












```
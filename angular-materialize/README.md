# angular2-materialize
  How to install this library using **@angular/cli**


### Updated -  March 2017


- Index
  + How to Install
  + Configuration
  + Using materialize in the components


### How to Install
  Check if your system is updated ( Node + angular/cli )

  https://github.com/kelber/How-To-Install-On-Linux/tree/master/Angular-CLI


```
npm install materialize-css --save
npm install angular2-materialize --save

```
##### jQuery **Required**  and HammerJS
```
npm install jquery@^2.2.4 --save
npm install hammerjs --save
```


### Configuration

##### angular-cli.json
Add this path in the **styles** array.

"../node_modules/materialize-css/dist/css/materialize.css",

```
"styles": [
  "../node_modules/materialize-css/dist/css/materialize.css",
  "styles.css"
],
```

Add this paths in the **scripts** array.

```
"scripts": [
      "../node_modules/jquery/dist/jquery.js",
      "../node_modules/hammerjs/hammer.js",
      "../node_modules/materialize-css/dist/js/materialize.js"
],



```


##### app.module.ts
Import and declare MaterializeModule in the @NgModule

```js

import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

// Materialize
import { MaterializeModule } from 'angular2-materialize';


import { AppComponent } from './app.component';


@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule

 // Materialize  
   ,MaterializeModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Stop your running your app and restart again.  

```
 > ng serve

```  



##### index.html
In the index.html add the CDN of google fonts and material icons

### K-> Attencion in http: x https://  security (s) is important to deploy
```
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

```


### Using materialize in the components

Example: in the  home.component.ts for using Javascript **Parallax**, **DropDown** and **SideNav**


```js
import { Component, OnInit } from '@angular/core';

// declare
declare var $: any

export class HomeComponent implements OnInit {

  ngOnInit() {

// initialization

      $('.button-collapse').sideNav();
      $('.dropdown-button').dropdown();
      $('.parallax').parallax();



  }

}
```
Visit: http://materializecss.com  
and take  **initialization** the jQuery functions like:

 $('.parallax').parallax();


#### Oficial angular2-materialize site:
### https://www.npmjs.com/package/angular2-materialize



#### Oficial materializecss site:
### http://materializecss.com





### **If**  your system asking to import 'materialize-css' in the app.module.ts

```js
import 'materialize-css';
import 'angular2-materialize';
```
### **If**  error e.velocity appear's in your Browser console it will be resolve take off these 2 lines.

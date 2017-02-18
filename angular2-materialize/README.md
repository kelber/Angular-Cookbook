# angular2-materialize
  How to install this library using **@angular/cli**


### Updated -  February 2017


- Index
  + How to Install
  + Configuration
  + Using materialize in the components


### How to Install

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
Add this 3 lines and declare MaterializeModule in the @NgModule

```

import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

// Materialize  
import 'materialize-css';
import 'angular2-materialize';
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
Note:  import 'materialize-css' **before**
       import 'angular2-materialize';






##### index.html
In the index.html add the CDN of google fonts and material icons
```
<link href="http://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

```


### Using materialize in the components

Example: in the  home.component.ts for using Javascript **Parallax**


```
import { Component, OnInit } from '@angular/core';

// declare
declare var $: any

export class HomeComponent implements OnInit{

  ngOnInit() {

// initialization
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

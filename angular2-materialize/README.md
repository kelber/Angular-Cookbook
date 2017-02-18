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
##### jQuery is Required
```
npm install jquery@^2.2.4 --save
```


### Configuration

##### angular-cli.json
Add this line in the styles array.
"../node_modules/materialize-css/dist/css/materialize.css",

```
"styles": [
"../node_modules/materialize-css/dist/css/materialize.css",
"styles.css"
]
```


##### app.module.ts
Add this 3 lines and declare in the @NgModule

```

import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

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
    HttpModule,
  **MaterializeModule**
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
Note:  import 'materialize-css' **before** import 'angular2-materialize';






##### index.html
In the index.html add the CDN of google fonts and material icons
```
<link href="http://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

```


### Using materialize in the components

Example: in the  home.component.ts for using Javascript **Parallax**
\\ declare var $: any;
\\ use Jquery initialization

```
import { Component, OnInit } from '@angular/core';

declare var $: any

export class HomeComponent implements OnInit{

  ngOnInit() {

    $('.parallax').parallax();

  }

}
```
In this site have the code of **initialization** the jQuery functions like:  $('.parallax').parallax();


#### Oficial materializecss site:  http://materializecss.com

#### Oficial angular2-materialize site:
https://www.npmjs.com/package/angular2-materialize

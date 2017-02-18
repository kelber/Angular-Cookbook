# angular2-materialize
  How to install this library using <strong> @angular/cli </strong>  


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

In the angular-cli.json file add this line in the styles[] array

```
"styles": [
<strong>  "../node_modules/materialize-css/dist/css/materialize.css",</strong>
"styles.css"
]
```

In the /app folder
##### app.module.ts

```

import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

<strong>
import 'materialize-css';
import 'angular2-materialize';
import { MaterializeModule } from 'angular2-materialize';
</strong>


import { AppComponent } from './app.component';


@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
  <strong>MaterializeModule</strong>
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
Note:  import 'materialize-css' <strong>before</strong> import 'angular2-materialize';




##### index.html
In the index.html add the CDN of google fonts and material icons
```
<link href="http://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

```


### Using materialize in the components

Example: in the  home.component.ts for using Javascript <strong>Parallax</strong>

```
import { Component, <strong>OnInit</strong> } from '@angular/core';

<strong>declare var $: any; </strong>

export class HomeComponent implements OnInit{

  ngOnInit() {

    <strong> $('.parallax').parallax();</strong>

  }

}
```

#### In the  http://materializecss.com/ have the code of **initialization** the jQuery functions like:  $('.parallax').parallax();


#### Oficial angular2-materialize:
https://www.npmjs.com/package/angular2-materialize

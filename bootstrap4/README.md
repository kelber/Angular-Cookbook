#  Bootstrap4 

#### Ref: https://ng-bootstrap.github.io/#/getting-started



### updated in October 2017 

Install
```
npm install --save bootstrap@next
```

index.html
import CDN's:  https://getbootstrap.com/docs/4.0/getting-started/introduction/

```html
<!--mobile-first-->
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
``` 
#### _variables.scss
copy what you want to styles.scss.

styles.scss
```css

@import '~/bootstrap/dist/css/boostrap.css';

$body-bg:      royalblue !default;
$body-color:   $theme-color("primary") !default;


@mixing anchor {
  font-size: 1.1em;
  font-weight: bold;
}

$background-image url('/assets/car.jpg') no-repeat;
// background-size: cover;


@media(max-width: 575px) { ... }
@media(min-width: 576px) { ... }
or
@media(min-width: 576px) and (max-width: 767px) { ... }




// Fonts

$font-family-sans-serif: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol" !default;
$font-family-monospace:  "SFMono-Regular", Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace !default;
$font-family-base:       $font-family-sans-serif !default;



// where you will use

@import '../../styles.scss';

.btn {
  @include anchor;
}

```
### Layout
```html
  <div class="container"></div>
  <div class="container-fluid">100% width</div>
  
<!--GRID -->
<div class=-"row">
  <div class="col">1coluna</div>
  <div class="col-8">8 colunas</div>
  

<!--3 columns-->
  <div class="col-6 col-md4">1</div>
  <div class="col-6 col-md4">2</div>
  <div class="col-6 col-md4">3</div>
  
  <!--VERTICAL ALIGN-->
  
  <div class="row align-items-start">Start </div>
  <div class="row align-items-center">Center </div>
  <div class="row align-items-end">End </div>
  
  <!--HORIZONTAL ALIGN-->
  
  <div class="row justify-content-start">Start </div>
  <div class="row justify-content-center">Center </div>
  <div class="row justify-content-end">End</div>
  
  <!--OFFSETING-->
  <div class="col-6 col-md4">4</div>
  <div class="col-6 col-md4 ml-auto ml-md-auto">pass 4 and put in the end 4</div>


</div>

```

















### updated in August 2017 

Install
```
npm install --save @ng-bootstrap/ng-bootstrap

```

##### app.module.ts

```js
import {NgbModule} from '@ng-bootstrap/ng-bootstrap';


imports: [
  NgbModule.forRoot()
];

``` 

#### Ref: https://v4-alpha.getbootstrap.com/getting-started/introduction/

Paste this lines in your index.html 

```html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.6/css/bootstrap.min.css" integrity="sha384-rwoIResjU2yc3z8GV/NPeZWAv56rSmLldC3R/AZzGRnGxQQKnKkoFVhFQhNUwEyJ" crossorigin="anonymous">

<script src="https://code.jquery.com/jquery-3.1.1.slim.min.js" integrity="sha384-A7FZj7v+d/sdmMqp/nOQwliLvUsJfDHW+k9Omg/a/EheAdgtzNs3hpfag6Ed950n" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/tether/1.4.0/js/tether.min.js" integrity="sha384-DztdAPBWPRXSA/3eYEEUWrWCy7G5KFbe8fFjk5JAIxUYHKkDx6Qin1DkWx51bBrb" crossorigin="anonymous"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.6/js/bootstrap.min.js" integrity="sha384-vBWWzlZJ8ea9aCX4pEW3rVHjgjt7zpkNpZk+02D9phzyeVkE+jo0ieGizqPLForn" crossorigin="anonymous"></script>

``` 

### Put FontAwsome ICONS
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css">

### Using the components

#### https://ng-bootstrap.github.io/#/components/accordion/api


```js
    <ngb-alert>Alert component here </ngb-alert>

```

#  Bootstrap4 

#### Ref: https://ng-bootstrap.github.io/#/getting-started


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

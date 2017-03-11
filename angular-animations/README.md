# angular- Animations using HostBinding


### Updated -  March 2017


- Index
  + Configuration
  + Using the file in your components


### Configuration

##### import in your folder /app the file  **router-animations.ts**



##### in your .component.ts

```js
import { Component , OnInit , HostBinding } from '@angular/core';
import { moveIn } from '../router.animations';
or
import { moveIn , fallIn , moveInLeft } from '../router.animations';
```


add this code in your component.

```js

@Component({
  selector: '',
  templateUrl: '',
  styleUrls: [],

  animations: [moveIn(), fallIn(), moveInLeft() ],
  host: { '[@moveIn]' : '' }
})
```


in your html add the tag

```html
<a class="brand-logo" [@fallIn]="state">Your App.com</a>

<h3 [@moveInLeft]>H3 Title</h3>
```


### Just add your **method** of router-animations.ts to your component and use it in your html tag



# Angular Animations state transitions
### trigger , state, style, transitions , animate




##### in your .component.ts
```js
import { Component ,OnInit,  trigger , state, style,transition,  animate } from '@angular/core';


@Component({
  selector: '',
  templateUrl: '',
  styleUrls: [],


  animations: [
    trigger('intro', [
     transition('* => *' , animate(2000)),


      state('go', style({
        'background-color': 'red',
        'color': 'white'
      })),

      transition( '* => *', animate(100)),

      state('stop', style({
        'background-color': 'whitesmoke',
        'color': 'teal'
      })),


    ])
  ]
})

```


The idea of this animations is create  states. **intro** , **go**, **stop** and running trough this.


```js


export class Component implements OnInit {
  banner = 'intro';

  constructor() {}

  ngOnInit() {

    this.banner = 'stop';

    // Ex. de setTimeout
    // setTimeout( () => {
    //   this.router.navigate(['/games'])
    //
    //  }, 4000);
    //
  }
}
```

In your html

you set the class="banner" CSS
banner = 'intro', to start position;


```html
<h1 class="banner" [@intro]="banner">Your App.com</h1>

```
You define the banner using the color: red;

```css
.banner {
  color: red;
}

```
#### 1: You define in the .css file the color of class .banner is red.
#### 2: The animations: trigger start in 'intro' and run trought states until 'stop'.

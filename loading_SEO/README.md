 

# SEO
```js
import { Meta, Title } from '@angular/platform-browser';

constructor(public meta: Meta, public title: Title) { 
 this.title.setTitle('Side of Fav icon...');
 this.meta.addTags([
      { name: 'author', content: 'Kelber'},
      { name: 'keywords', content: 'posts, Posts, important words'},
      { name: 'description', content: 'A pages description,usually one or two sentences. 135 to 160 characteres' }
    ])

}

// Answer
// <head> <meta name="Kelber"></meta></head>


```
 
## LOADING 

#### Intro page in the index.html

```html
 <app-root>
 <style>
  app-root {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;

    /*color: pink;*/
    color: lightblue;
    text-transform: uppercase;
    font-family: -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        Roboto,
        Oxygen-Sans,
        Ubuntu,
        Cantarell,
        Helvetica,
        sans-serif;
    font-size: 2.5em;
    text-shadow: 2px 2px 10px rgba(0,0,0,0.2);
  }
  body {
    background: steelblue;
    /*background: salmon;*/
    margin: 0;
    padding: 0;
  }

  @keyframes dots {
    50% {
      transform: translateY(-.4rem);
    }
    100% {
      transform: translateY(0);
    }
  }

  .d {
    animation: dots 1.5s ease-out infinite;
  }
  .d-2 {
    animation-delay: .5s;
  }
  .d-3 {
    animation-delay: 1s;
  }
  </style>

  Loading<span class="d">.</span><span class="d d-2">.</span><span class="d d-3">.</span>
  </app-root>
  
  ```





  
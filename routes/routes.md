# Angular - Routes 

### 2018 

## Lazy Loading

Ex: About module with lazy loading
app-routing.mdule.ts
```js
  { path: 'about', loadChildren: './about/about.module#AboutModule' }
```
about.module or about-routing.module.ts
```js
  { path: '', component: AboutComponent } 

  // dont forget to put in the declarations
  [ AboutComponent ]
```


  ## Children Routes
 ```js
  { path: 'restaurants/:id', component: RestaurantsComponent,
    children: [
      { path: '', redirectTo: 'restaurants', pathMatch: 'full' },
      { path: 'restaurants', component: RestaurantsComponent }
    ]
   }

 ```

## Module with Providers
Ex: AuthService avoiding conflits with multiple imports.

shared.module.ts
```js
  import { NgModule, ModuleWithProviders } from '@angular/core';

  export class SharedModule {
    return {
      ngModule.SharedModule,
      providers: [ Put here all 'services' from AuthService ]
    }
  }
```

app.module.ts
```js
  imports: 
  [
     SharedModule.forRoot()  // will load all providers avoiding conflits with 
  ]

```


## Pre-Loading Strategy
Load in "background" all LazyLoading Modules

app.module.ts
```js
  import { RouterModule, PreloadAllModules } from '@angular/routes';

  RouterModule.forRoot( Routes, {
    preloadingStrategy: PreloadAllModules
  })

 // Will load the home + 0chunck + 1chunck + 2chunck...
 ```

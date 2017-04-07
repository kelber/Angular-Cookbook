# NG2-Translate

#### Ref: https://www.npmjs.com/package/ng2-translate


### updated in Abril 2017 
### @angular v4

Install
```
  sudo npm i ng2-translate --save
```


##### app.module.ts

```js

import { TranslateModule , TranslateStaticLoader, TranslateLoader } from 'ng2-translate';

// create this file. missingtemplate.component and import here 
// to give a answer for the missing words...
import {  MyMissingTranslationHandler } from './missingtemplate.component';

// create this function and redirect to /src/i18n or your preference folder
export function createTranslateLoader(http: Http) {
return new TranslateStaticLoader(http, './src/i18n', '.json');
    }


imports: [

     TranslateModule.forRoot({

    provide: TranslateLoader,
    useFactory: (createTranslateLoader) ,
    deps: [Http ]
    })


];
``` 

#### create this file  missingtemplate.component.ts

it will give a answer for missing words...

```js
import { MissingTranslationHandler , MissingTranslationHandlerParams } from
'ng2-translate';

export class MyMissingTranslationHandler implements MissingTranslationHandler {
  handle( params: MissingTranslationHandlerParams ) {
    return 'This works is not translated yet ' + params.key;
  }

  }

``` 

##### app.component.ts
Note: I put this code in the navbar.component.ts to apply in all application too.

```js
import { TranslateService } from 'ng2-translate';


   constructor(private translate: TranslateService) {
  translate.addLangs(["en", "fr"]);
  translate.setDefaultLang('en');

  let browserLang = translate.getBrowserLang();
  translate.use(browserLang.match(/en|fr/) ? browserLang : 'en');
  }

```

##### model.json

```json

{
    "Home": {
      "mainTitle": "This is the main title",
      "secondTitle": "This is the  2" 
    } 
}

``` 

##### in the html for example navbar.component.html

```html
<div>
  <label>
    {{ 'Home.mainTitle' | translate }}
    <select #langSelect (change)="translate.use(langSelect.value)">
      <option *ngFor="let lang of translate.getLangs()" [value]="lang" [selected]="lang === translate.currentLang">{{ lang }}</option>
    </select>
  </label>
</div>

<h2>{{ 'Home.mainTitle' | translate }}</h2>

``` 








###  old schema below

##### app.component.ts
PS: I make it passing in navbar.component too.

```
import { TranslateService } from 'ng2-translate';

constructor(private translate: TranslateService) {
    translate.addLangs(["pt", "en" , "es", ]);
    translate.setDefaultLang("pt");
    
    let browserlang = translate.getBrowserLang();
    translate.use(browserlang.match( / pt|en|es / ) ? browserlang : "pt" )
  // translate.use("pt"); // test
}


  changeLanguage(lang) {
    this.translate.use(lang);
}

```

##### app.module.ts

```
import { TranslateModule } from 'ng2-translate';

//  TranslateModule.forRoot()  

```

Create folder i18n

- src
  + app
  + assets
  + environments
  + **i18n** 
     ++ pt.json
     ++ en.json
     ++ es.json


##### en.json ( Example ) 
ps: "Navbar" is to use in {{ 'Navbar.Langagues.Portuguese' | translate }}

```
{
  "Navbar": {
    "navTitle": "Title nav",
    "navSlogan": "Slogan HERE",
    "navAbout": "About",
    "Language": "Language",
    "Languages": {
      "Portuguese": "Portuguese",
      "English":    "English",
      "Espanish":  "Spanish"
    }
 },
  "Home": {
    "homeText": "Welcome Home",
    "secondText": "Change the Language"
  },
  "About": {
    "title": "About page"


  }


}


```

##### Html Template

Navbar 

```

<!-- Dropdown Structure -->
<ul id="dropdown1" class="dropdown-content">
  <li><a (click)="changeLanguage('pt')">{{ 'Navbar.Languages.Portuguese'  | translate }} </a></li>
  <li><a (click)="changeLanguage('en')">{{ 'Navbar.Languages.English' | translate }} </a></li>
  <li class="divider"></li>
  <li><a (click)="changeLanguage('es')">{{ 'Navbar.Languages.Espanish' | translate }} </a></li>
</ul>
<nav>
  <div class="nav-wrapper teal darken-2">
    <a href="#!" class="brand-logo">T4T.com</a>
    <ul class="right hide-on-med-and-down">
      <li><a href="sass.html"> {{ 'Navbar.navTitle' | translate }} </a></li>
      <li><a href="sass.html"> {{ 'Navbar.navSlogan' | translate }} </a></li>
      <li routerLink="/about"><a > {{ 'Navbar.navAbout' | translate }} </a></li>
      <!-- Dropdown Trigger -->
      <li><a class="dropdown-button" href="#!" data-activates="dropdown1"> {{ 'Navbar.Language' | translate }}  <i class="material-icons right">arrow_drop_down</i></a></li>
    </ul>
  </div>
</nav>

```
Pages Schema

```
  <h3> {{ 'About.title' | translate }} </h3>

```

### Opcional Mode  - Show a error message in the html template

missingtemplate.component.ts
```
import { MissingTranslationHandler , MissingTranslationHandlerParams } from
'ng2-translate';

export class MyMissingTranslationHandler implements MissingTranslationHandler {
  handle( params: MissingTranslationHandlerParams ) {
    return 'Translate not work  ' + params.key;
  }

}   


```

##### app.component.ts

```

// translate
import { TranslateModule , TranslateService, MissingTranslationHandler } from 'ng2-translate';
import { MyMissingTranslationHandler } from '../missingtemplate.component';

providers: [ 
    { provide: MissingTranslationHandler, useClass: MyMissingTranslationHandler },

]

```




























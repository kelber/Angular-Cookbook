# NG2-Translate

#### Ref: https://www.npmjs.com/package/ng2-translate

Install
```
  sudo npm i ng2-translate --save
```

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

### Opcional Mode

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




























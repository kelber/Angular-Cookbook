
# Pug



#Index.html
  <link rel="icon" type="image/x-icon" href="favicon.ico">

# pasta/styles
    Arquivos _btn.scss, _global.scss e outros
#styles.scss
```css
@import '~styles/mixins';
@import '~styles/variables';

@import '~bootstrap-sass/assets/stylesheets/bootstrap/normalize';
@import '~bootstrap-sass/assets/stylesheets/bootstrap/mixins/';
@import '~bootstrap-sass/assets/stylesheets/bootstrap/grid';
@import '~bootstrap-sass/assets/stylesheets/bootstrap/responsive-embed';
@import '~bootstrap-sass/assets/stylesheets/bootstrap/responsive-utilities';
@import '~bootstrap-sass/assets/stylesheets/bootstrap/utilities';
@import '~bootstrap-sass/assets/stylesheets/bootstrap/type';
@import '~bootstrap-sass/assets/stylesheets/bootstrap/scaffolding';
// @import '~bootstrap-sass/assets/stylesheets/bootstrap/modals';

@import '~font-awesome/scss/font-awesome';

@import '~styles/custom-utilities';
@import '~styles/global';
@import '~styles/btn';
@import '~styles/elements';
@import '~styles/form';
```


## index.ts
cada module coloca-se um index.ts
Ex: 
cadastro/index.ts
```js
export * from './cadastro.module';
export * from './form-cadastro/form-cadastro.component';
// mais outros components
```




## environments.ts
 api: 'http://localhost:3000'

## app.api.ts
```js
import { environment } from '../environments/environment'

// velho
export const API = environment.api;

export class API {

  static readonly MEAT_API = environment.api


  // REGISTER-EMAIL
  static readonly REGISTER_EMAIL = `${MEAT_API}/register-email`;

}

// para usar essa API:
// this.http.get(API.CLIENTES)

```
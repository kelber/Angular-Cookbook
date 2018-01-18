
# Short Url in Angular
Example:
```js
// import { AuthService } from '../../../core/auth.service';
import { AuthService } from '@core/auth.service';
// or
import { UserLoginComponent } from '@shared/user-login/user-login.commponent';

```

tsconfig.json
```js
// "lib": [
// ],
 "baseUrl": "src",
 "paths": {
   "myapp-@core/*": [ "app/core/*" ],  //myapp avoid collision
   "myapp-@shared/*": [ "app/shared/*" ],
   "myapp-@environments/*": [ "environments/*" ],

 }

```

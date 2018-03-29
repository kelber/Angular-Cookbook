### Email Pattern

```js
  import { Validators } from '@angular/forms';

  emailPattern = '/^(([^<>()\[\]\.,;:\s@\"]+(\.[^<>()\[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i';

  this.orderForm = this.fb.group({
    email: [ '', Validators.required, Validators.pattern(this.emailPattern) ],
  });

```

### Email + Confirm Email

```js
  import { Validators, AbstractControl } from '@angular/forms';

  this.orderForm = this.fb.group({
    email: [ '', Validators.required, Validators.minLength(5) ],
    emailConfirmation: [ '', Validators.required ],
  }, { validator ou validators: OrderComponent.equalsTo });


  static equalsTo(group: AbstractControl): { [key: string]: boolean } {
    const email = group.get('email');
    const emailConfirmation = group.get('emailConfirmation');
    if ( !email || emailConfirmation ) {
      return undefined
    }
    if ( email !== emailConfirmation.value ) {
      return { emailNotMatch: true }
    }
      return undefined  // se nao bateram nao associa a grupo nenhum
  }

```

```html
  <span *ngIf="orderForm.hasError('emailNotMatch')"> Email not match</span>

```
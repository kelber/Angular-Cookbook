
# Reactive FormsModule - Model Driven

Ref:
https://scotch.io/tutorials/using-angular-2s-model-driven-forms-with-formgroup-and-formcontrol
https://blog.thoughtram.io/angular/2016/06/22/model-driven-forms-in-angular-2.html

```js
import { FormsModule , ReactiveFormsModule , FormGroup , FormBuilder } from '@angular/forms';

registerForm: FormGroup;

  constructor( private fb: FormBuilder ) {}

```

```html

<form [formGroup]="registerForm">
    <input formControlName="firstName" />
    <input formControlName="lastName" />
    <br>
    <!-- here is the formGroupName of address -->
      <fieldset formGroupName="address">
        <input formControlName="street" />
        <input formControlName="city" />
      </fieldset>
</form>



<!-- VALIDATE STATE -->
    <input formControlName="firstName" />
    <p *ngIf="registerForm.controls.firstName.errors">This field is required</p>

```

```js

this.registerForm = this.fb.group({
  firstName: '',
  lastName: '',
    address: this.fb.group({
      street: '',
      city: ''
    })
});


// or using the complete form validations
this.registerForm = this.fb.group({
  firstName: [ '', Validators.required ],
  lastName:  [ '', Validators.minLength(5) ],
  password:  [ '' , Validators.pattern('[0-9]+')],
    address: this.fb.group({
      street: '',
      city: ''
    })
});


// to SEND or UPDATE values
// setValue -> sendValue
// pathValue -> updateValue

this.registerForm. setOrPathValue({
  email: 'your@email.com',    // this.email
  password: '123'             //this.password

});

// console.log(this.registerForm) --> [ object , object ]
// console.log(this.registerForm.value) -->  values



```

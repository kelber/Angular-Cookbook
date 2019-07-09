
# Reactive FormsModule - Model Driven


### Updated 7 July 2019
Maximilian Course
// Select Radio Button

this.signupForm = this.fb.group({
      'userData': {
            'username': [ ],
       },
       'hobbies': new FormArray( [] )
 });
 
 onAddHoby() {
      const control = new FormControl(null, Validators.required);
      ( <FormArray>this.signForm.get('hobbies')).push(control);
 }

// Html
<div formArrayName="hobbies">
      <button (click)="onAddHoby()">Add Hobby</button>
      <div *ngFor="let hobbyControl of signForm.get('hobbies').controls; let i = index">
          <input type="text" class="form-control" [formControlName]="i" >
      </div>
      
</div>


### Updated September 2017

import the FormsModule, ReactiveFormsModule in the SharedModule

```js
import { FormsModule , ReactiveFormsModule } from '@angular/forms';
```

Estructure

|-reports <br>
--|-form-input <br>
--|-form-radio <br>
--|-form-select <br>



## Example - Input Fields



#### Father Component
Pass all the fields to Son Component and in the son have the HTML tags and details...

**father.html**
```html
<p> {{ evaluationForm?.value | json }} and {{ evaluationForm?.valid }} </p>



<form [formGroup]="evaluationForm" novalidate>

      <app-input label="Vehicle" errorMessage="Mandatory field">
            <!--in the SON component will replace for the <ng-content></ng-content> -->
            <input type="text"
               class="form-control"
               placeholder="Vehicle"
               formControlName="vehicle">
      </app-input>
      
 </form>
 
  <button type="submit" 
          class="btn btn-primary btn-block"
          [disabled]="!evaluationForm.valid"
         (click)="onSubmit(evaluationForm)">
    Submit
  </button>


```

**father.component.ts**
```js
import { FormsModule, ReactiveFormsModule, FormGroup, FormBuilder, Validators } from '@angular/forms';

 evaluationForm: FormGroup;

 ngOnInit() {
    this.evaluationForm = this.fb.group({
        vehicle: [ '',Validators.required ],
     
    })

 }

```


#### Son Component
Receive the informations and here have the HTML tags and details...

**son.html**
```html

 <div class="form-group" >
    <div class="has-success" [class.has-success]="hasSuccess()"><label>{{ label }} </label>
    
        <!--here receive the <input />-->
        <ng-content></ng-content>  
    
    <div *ngIf="hasSuccess()" class="form-control-feedback">Ok</div>
    <small *ngIf="hasError()" [class.has-error]="hasError()">{{ errorMessage }}</small>
    </div>
  </div>


``` 

```js
import { Component, OnInit, Input, ContentChild, AfterContentInit } from '@angular/core';
import { NgModel, FormControlName } from '@angular/forms';

export class SonComponent implements OnInit, AfterContentInit {


 input: any;
 
 @Input() label: string;
 @Input() errorMessage: string;
 

 
  /** optional?   @ContentChild(NgModel) model: NgModel  **/
 @ContentChild(FormControlName) control: FormControlName


  ngAfterContentInit() {
    this.input = this.control
    /**  this.input = this.model || this.control **/
  }
  

  hasSuccess(): boolean{
    return this.input.valid && (this.input.dirty || this.input.touched)
  }
  hasError() {
    return this.input.invalid && ( this.input.dirty || this.input.touched )
  }


``` 


## Example for Select Fields ( radio, select, booleans )


Take it from angular.io documentation
```html
   <!--[ngValue]="brand" the Object You add all fields. -->
    <select class="form-control" formControlName="brand" >
        <label>Select the Brand</label>
         <option *ngFor="let brand of brands" [ngValue]="brand.id"
        >{{ brand?name }} </option>
    </select>
``` 

#### Father Component

 **father.html**
```html


       <app-radio [options]="paymentOptions" 
                 formControlName="paymentOption">
       </app-radio>
 


``` 
**father.component.ts**
```js

  paymentOptions: RadioOption[] = [
    {label: 'Money', value: 'MON'},
    {label: 'Debit', value: 'DEB'},
    {label: 'Credit', value: 'CRED'}
  ]
  
   ngOnInit() {
    this.evaluationForm = this.fb.group({
        vehicle: [ '',Validators.required ],
        paymentOption: this.fb.control( '', [Validators.required])
    })

``` 


#### Son Component

**son.html**
```html

<div *ngFor="let option of options">
  <label>
    <div class="iradio_flat-red" 
         [class.checked]="option.value === value"
         (click)="setValue(option.value)">
    </div>
    {{option.label}}
  </label>
</div>

``` 


**son.component.ts**
```js

import { Component, OnInit, Input, forwardRef } from '@angular/core';
import {NG_VALUE_ACCESSOR, ControlValueAccessor} from '@angular/forms'

import {RadioOption} from './radio-option.model'


@Component({
      /** add more **/  ,
  providers: [
    {
      provide: NG_VALUE_ACCESSOR,
      useExisting: forwardRef(()=>RadioComponent),
      multi: true
    }
  ]
  

  export class RadioComponent implements OnInit, ControlValueAccessor {

  @Input() options: RadioOption[]

  value: any
  onChange: any

      
  setValue(value: any){
    this.value = value
    this.onChange(this.value)
  }
  
/** This code is from ControlValueAccessor  click with RightBtn and open this file.
  
/**
   * Write a new value to the element.
   */
  writeValue(obj: any): void {
    this.value = obj
  }
  /**
   * Set the function to be called when the control receives a change event.
   */
  registerOnChange(fn: any): void {
    this.onChange = fn
  }
  /**
   * Set the function to be called when the control receives a touch event.
   */
  registerOnTouched(fn: any): void {}
  /**
   * This function is called when the control status changes to or from "DISABLED".
   * Depending on the value, it will enable or disable the appropriate DOM element.
   *
   * @param isDisabled
   */
  setDisabledState?(isDisabled: boolean): void {}

``` 




///////////////////////////////////////////////////////////////////////////////////




#### Reactive Forms - Model Driven May 2017

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

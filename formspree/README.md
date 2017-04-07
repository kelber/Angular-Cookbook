
# Form email using only JS

main site: www.formspree.io

this is the simple way to send emails using JS.



```html

<form action="https://formspree.io/kelberstuchi@gmail.com"  method="POST" id="myForm">
  <input type="text" name="text" required  placeholder="{{ 'rightCard.contMessage' | translate }}">
  <input type="email" name="_replyto" required  placeholder="{{ 'rightCard.contEmail' | translate }}"  >
 <!-- <a class="waves&#45;effect waves&#45;light btn white&#45;text" type="submit" value="Send" (click)="sendForm()"> {{ 'rightCard.contBtn' | translate }}</a> -->
 <input align="center" type="submit" (click)="sendForm()" class="waves-effect waves-light btn btn-largue white-text center" value="{{ 'rightCard.contBtn' | translate }}" >
 <br>
 <span align="center" *ngIf="messageA" >{{ 'rightCard.messageOk' | translate }} </span>
 </form>

``` 


```js

messageA: boolean = false; 

sendForm() {

this.messageA = !this.messageA;

$('#myForm').submit( function (e) {

  var _replyto = document.getElementById('_replyto')
  var text = document.getElementById('text')

  if( !this._replyto || !this.text) {
    console.log('error here');
  } else {
    console.log('estou else');

   $.ajax({
   url: 'https://formspree.io/kelberstuchi@gmail.com',
   method: 'POST',
   data: $(this).serialize(),
   dataType: 'json'
});

  e.preventDefault()
  $(this).get(0).reset()
  console.log('enviado com sucesso !');

   }
   this.text.value = '';
   this._replyto.value  = '';
})


  setTimeout( () => {
    this.router.navigate(['']);
  }, 3500);



}


``` 





#### Template Driven x Reactive ( Data Driven )

#### Template
Orientado ao template.
Formulario configurado no HTML e o angular deduz um
formGroup apartir do HTML


#### Data Driven
Formulario criado programaticamente é é sincronizado com a 
DOM/HTML



```js

formulario: FormGroup;

ngOnInit() {
    // Criando: Metodo 1
    this.formulario = new FormGoup({
        nome: new FormControl(null),
        email: new FormControl(null)           // cada campo é um controle de formulario
    })
}

    // Criando: Metodo com FomrBuilder

    this.formulario = this.formBuilder.group({
        nome: [''],
        email: ['']
    })


    onSubmit() {
        this.http.post(url)
            .map( res => res )
            .subscribe( 
                dados => {
                   // resetar form
                   this.formulario.reset(); },
                (error: any) => alert('errou'));
    }



```

```html
<form [formGroup]="formulario">
    <input formControlName="nome" />
    <input formControlName="email" />


</form>


```

V94 - Validação nos campos do Angular
```js


this.formulario = this.formBuilder.group({
    nome: ['', Validators.required, Validators.minLength(3) ],
    email: ['', [Validators.required, Validators.email ]]
})

```

v95 - Validacao com CSS
```html

<div class="form-group" [ngClass]="aplicaCssErro('nome')">
    <div class="col-sm-12">
    <label for="nome" class="control-label">Nome</label>
    </div>

    <div class="col-sm-12">
    <input type="text" class="form-control" formControlName="nome" id="nome" placeholder="Nome">

    <!-- componente descrito abaixo -->
   <app-campo-control-erro
    [mostrarErro]="verificaValidTouched('nome')"
    msgErro="Nome é obrigatorio">   
   </app-campo-control-erro>


   <!-- DICA LOIANE -->
   <!-- .get ou .controls É A MESMA COISA -->
 <app-campo-control-erro
   [mostrarErro]="!formulario.get('nome').valid"
   [mostrarErro]="!formulario.controls('nome').touched">
<app-campo-control-erro>

    </div>
</div>  




```

### Aplicando CSS 

```js

// acho que da pra trocar 2fn em um hasError() { }
verificaValidTouched(campo) {
    return !this.formulario.get(campo).valid &&
            this.formulario.get(campo).touched;
}

aplicaCssErro(campo) {
    return {
    'has-error': this.verificaValidTouched(campo),
    'has-feedback': this.verificaValidTouched(campo)
    };
}

/*  usando no HTML
<div class="form-group" [ngClass]="aplicaCssErro('nome')">
</div>

*/

```

app-campo-control-erro
```js
import { Component, OnInit, Input } from '@angular/core';

@Component({
selector: 'app-campo-control-erro',
templateUrl: './campo-control-erro.component.html',
styleUrls: ['./campo-control-erro.component.css']
})
export class CampoControlErroComponent implements OnInit {

@Input() msgErro: string;
@Input() mostrarErro: boolean;

constructor() { }

ngOnInit() {
}

}


```

```html
<div *ngIf="mostrarErro" >
<span class="glyphicon glyphicon-remove form-control-feedback"></span>
<span class="sr-only">(error)</span>
<div class="alert alert-danger errorDiv" role="alert">
    {{ msgErro }}
</div>
</div>

```

#### Validacao de EMAIL

```js

verificaEmailInvalido() {
    let campoEmail = this.formulario.get('email');
    if(campoEmail.errors) {    // errors: veja no console
        return campoEmail.errors['email'] && campoEmail.touched;
    }
}
```
```html
<app-campo-control-erro
[mostrarErro]="verificaEmailInvalido()"
```



v96 - Campos Endereços - campos alinhados no principal endereco.cep etc...

```html

<div formGroupName="endereco">

    <div class="form-group">

    <div class="col-md-3" [ngClass]="aplicaCssErro('endereco.cep')">
        <label for="cep" class="control-label">CEP</label>
        <input type="text" class="form-control" id="cep" formControlName="cep">
        <app-error-msg [control]="formulario.get('endereco.cep')" label="CEP"></app-error-msg>
     </div>

    <div class="col-md-3" [ngClass]="aplicaCssErro('endereco.numero')">
        <label for="numero" class="control-label">Número</label>
        <input type="text" class="form-control" id="numero" formControlName="numero">
        <app-error-msg [control]="formulario.get('endereco.numero')" label="Número"></app-error-msg>
      
    </div>

    <div class="col-md-6">
        <label for="complemento" class="control-label">Complemento</label>
        <input type="text" class="form-control" id="complemento" formControlName="complemento">
    </div>

    </div>

    <div class="form-group" [ngClass]="aplicaCssErro('endereco.rua')">
    <div class="col-sm-12">
        <label for="rua" class="control-label">Rua</label>
    </div>
    <div class="col-sm-12">
        <input type="text" class="form-control" id="rua" formControlName="rua">
        <app-error-msg [control]="formulario.get('endereco.rua')" label="Rua"></app-error-msg>
    </div>
    </div>

    <div class="form-group">
    <div class="col-md-5" [ngClass]="aplicaCssErro('endereco.bairro')">
        <label for="bairro" class="control-label">Bairro</label>
        <input type="text" class="form-control" id="bairro" formControlName="bairro">
        <app-error-msg [control]="formulario.get('endereco.bairro')" label="Bairro"></app-error-msg>
    </div>

    <div class="col-md-4" [ngClass]="aplicaCssErro('endereco.cidade')">
        <label for="cidade" class="control-label">Cidade</label>
        <select class="form-control" id="cidade" formControlName="cidade">
        <option *ngFor="let cidade of cidades" [value]="cidade.nome">{{ cidade.nome }}</option>
        </select>
        <app-error-msg [control]="formulario.get('endereco.cidade')" label="Cidade"></app-error-msg>
    </div>

    <div class="col-md-3" [ngClass]="aplicaCssErro('endereco.estado')">
        <label for="estado" class="control-label">Estado</label>
        <select class="form-control" id="estado" formControlName="estado">
        <option *ngFor="let estado of estados" [value]="estado.sigla">{{ estado.nome }}</option>
        </select>
        <app-error-msg [control]="formulario.get('endereco.estado')" label="Estado"></app-error-msg>
    </div>
    </div>

</div>


```


```js


this.formulario = this.formBuilder.group({
    nome: ['', Validators.required ],
    email: ['', [Validators.required, Validators.email ]],
    
    endereco: this.formBuilder.group({
    cep: [null, [Validators.required, ]],  //FormValidations.cepValidator
    numero: [null, Validators.required],
    complemento: [null],
    rua: [null, Validators.required],
    bairro: [null, Validators.required],
    cidade: [null, Validators.required],
    estado: [null, Validators.required]
}),


```

V98 - setValue e pathValue
# CEP


consulta-cep.service.ts
```js

import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { of } from 'rxjs';

@Injectable({
providedIn: 'root'
})
export class ConsultaCepService {

constructor(private http: HttpClient) { }

consultaCEP(cep: string) {

    console.log(cep);

    // Nova variável "cep" somente com dígitos.
    cep = cep.replace(/\D/g, '');

    // Verifica se campo cep possui valor informado.
    if (cep !== '') {
    // Expressão regular para validar o CEP.
    const validacep = /^[0-9]{8}$/;

    // Valida o formato do CEP.
    if (validacep.test(cep)) {
        return this.http.get(`//viacep.com.br/ws/${cep}/json`);
    }
    }

    // caso erro
    return of({});
}
}

```



component.ts
```js

// setValue para pathValue é que o PATH é apenas uma CORREÇÃO

consultaCEP() {
    const cep = this.formulario.get('endereco.cep').value;

    if (cep != null && cep !== '') {
    this.cepService.consultaCEP(cep)
    .subscribe(dados => this.populaDadosForm(dados));
    }
}

resetaDadosForm() {
    this.formulario.patchValue({
    endereco: {
        rua: null,
        complemento: null,
        bairro: null,
        cidade: null,
        estado: null
    }
    });
}


populaDadosForm(dados) {
    this.formulario.patchValue({
    endereco: {
        rua: dados.logradouro,
        // cep: dados.cep,
        complemento: dados.complemento,
        bairro: dados.bairro,
        cidade: dados.localidade,
        estado: dados.uf
    }
    });

    this.formulario.get('nome').setValue('Loiane');

    // console.log(form);
}


```


```html
<div class="col-md-3" [ngClass]="aplicaCssErro('endereco.cep')">
    <label for="cep" class="control-label">CEP</label>
    <input type="text" class="form-control" id="cep" formControlName="cep"
    (blur)="consultaCEP()"
    >
    <app-error-msg [control]="formulario.get('endereco.cep')" label="CEP"></app-error-msg>
 
 
</div>
```



V99 - Validação de todos os campos no botão submit

```js
onSubmit() {
    if(this.formulario.valid) {
        // logica caminho feliz
    }
    else {
        console.log('invalido');
        Object.keys(this.formulario.controls)
            .forEach( campo => {
                console.log(campo);   // nome, email, endereco
                const controle = this.formulario.get(campo);  // propriio campo
                // controle.markAsDirty ou markAsTouched
                controle.markAsDirty();
                if(contorle instanceof FormGroup) {
                    this.verificaValidacoesForm(controle)
                }
            });
    }
}


// Object.keys() // vai ajudar extrair as chaves
// do formulario que são nome: email: etc...

```


V102 - Combobox(simples) - Select
// exemplo Estado: SP
```html

<select formControlName="estado">
    <option *ngFor="let estado of estaodos" [value]="estado.sigla">{{ estado.nome }}
</select>

```
V103 - Combobox com Objeto ( ngValue e compareWith )
*Comparando objetos mais complexos*

```html
    <label>Cargo</label>
    <select formControlName="cargo">
        <option *ngFor="let cargo of cargos" [value]="cargo">{{ cargo.desc }}</option>
    </select>

    <button>Setar cargo</button>

```

```js
cargos: any[];
getCargos() {
    return [
        { nome: 'Dev', nivel: 'Junior', descr: 'Dev Jr' },
        { nome: 'Dev', nivel: 'Pleno', descr: 'Dev Pl' },
        { nome: 'Dev', nivel: 'Senior', descr: 'Dev Sr' },
    ]
}

ngOnInit() {
    this.cargos = this.dropdownService.getCargos();
}


this.formulario = this.formBuilder.group({
    // nome: ['', Validators.required ],
    // email: ['', [Validators.required, Validators.email ]],
    // endereco: this.fb.group({
        // outros
    // }),
    cargo: ['']

});

// setar um valor dif do setado
setarCargo() {
    const cargo =  { nome: 'Dev', nivel: 'Pleno', descr: 'Dev Pl' };  // aqui é Pleno e na tela tá Jr
    this.formulario.get('cargo').setValue(cargo);
}
// resp: no console fica "cargo": [Object, Object] e está no combo mostrando errado
/*  Referencias

=== é objeto de ref. que é endereço PARA pegar a ref tem que usar [ngValue]

[value]="cargo" para [ngValue]="cargo" mas .... ainda não seta nada

RESP: compareWith
*/


// agora use
compararCargos(obj1, obj2) {
    return obj1 && obj2 ? (obj1.nome === obj2.nome) : obj1 === obj2;
}

```


```html
    <!-- <label>Cargo</label>
    <select formControlName="cargo">
        <option *ngFor="let cargo of cargos" [value]="cargo" -->
        [compareWith]="compararCargos"
<!--         
        >{{ cargo.desc }}</option>
    </select>
    <button>Setar cargo</button> -->

```

V104 - ComboBox Multiplo ( Select Multiple )

```js

tecnologias: any[];
this.tecnologias = this.dropdownServices.getTecnologias();

getTecnologias() {
    return [
        { nome: 'java', desc: 'Java' },
        { nome: 'javascript', desc: 'Javascript' },
        { nome: 'php', desc: 'PHP' },
        { nome: 'ruby', desc: 'Ruby' },
    ]
}


setarTecnologias() {
    this.formulario.get('tecnologias').setValue('java', 'javascript', 'php')
}


```
```html
<label>Cargo</label>
<select multiple formControlName="tecnologias">
    <option  *ngFor="let tecnologia of tecnologias" [value]="tecnologia.nome">{{ tecnologia.desc }}</option>
</select>

<button (click)="setarTecnologias()">Setar tecnologias</button>


```


V105 - Radio button = Newsletter
```html
Newsletter
<div class="form-check" *ngFor="let item of newsletterOp">
<input type="radio" formControlName="newsletter" value="sim" checked>
<label class="form-check-label" 
       formControlName="newsletter"
       [value]="item.valor"
       > {{ item.desc }}
</label>


```

```js

newsletterOp: any[];
getNewsletter(){
    return [
        { valor: 's', desc: 'Sim' },
        { valor: 'n', desc: 'Não' },
    ];
}

// adicione no group
newsletter: ['s'],


```

V106 - Checkbox unico - ex: Termos
```js
termos: ['', Validators.pattern('true') ]


```

```html
<div [ngClass]="aplicaCssErro('termos')">
<input type="checkbox" formControlName="termos">Aceito os termos
```


V107 - FormArray Checkboxes Dinâmicos

```js
frameworks = ['Angular', 'React', 'Vue', 'Sencha' ];

```

// V107, 108 109 A FAZER


V110 - Validação entre dois campos ( Confirmar Email ) - Validacoes customizadas
Loiane tem um arquivo form-validaton.ts com metodos 

```js
email: ['', Validators.email],
confirmarEmail: ['', Validators.email]


```


```html

<input formControlName="email" />
<input formControlName="confirmarEmail" />

```

form-validations.ts
```js
import { FormArray, FormControl } from '@angular/common/forms';

export class FormValidatons {

    // existem alguns la
    static equalsTo(otherField: string) {
        const validator = (formControl: formControl) => {
            if(otherField == null) {
                throw new Error('E necessario campo');
            }
        }
        return validator;
    }



}


```





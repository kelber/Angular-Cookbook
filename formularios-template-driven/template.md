```html
<!-- v73 Template Forms -->

<!-- ngForm é do formsModule -->
<form #f="ngForm" (ngSubmit)="onSubmit(f)">   
    <input name="nome" [(ngModel)]="usuario.nome"/>
    <input name="email" [(ngModel)]="usuario.email" />

    <button type="submit" [disabled]="!f.valid">Submit</button>
</form>
```

```js


usuario: any = {
    nome: 'Loiane',
    email: 'email@abc.com'
}

onSubmit(f) {
    console.log(f);  // Resultado Objeto inteiro precisa do ngModel
    console.log(this.usuario);

    this.http.post('url', JSON.stringify(form.value))  // enviando JSON
            // .map().subscribe angular4
}


```

## Validações  CSS

```html
<form #f="ngForm" (ngSubmit)="onSubmit(f)">   
    <input name="nome" [(ngModel)]="usuario.nome"/>
    <input name="email" [(ngModel)]="usuario.email" />

    <button type="submit">Submit</button>
</form>

<!-- #nome -->
<input name="nome" [(ngModel)]="usuario.nome" #nome />
{{ nome.className }}  

<!-- css Aplica classe nessas condições abaixo -->
.ng-invalid.ng-touched:not(form) {
    border: 1px solid red;
}

```

## Validações - mensagens

**controls Objeto que tem nome e email propriedades**
```html

<input name="nome" [(ngModel)]="usuario.nome" 
       #nome="ngModel" />

<span *ngIf="!nome.valid && nome.touched" maisClassedoframework class="alert alert-danger" ou [class.has-error]="!nome.valid && nome.touched"> Nome Obrigatório </span>
```

<!-- obs usando  [class.has-error]="!nome.valid && nome.touched" vc pode tirar o estilo do arquivo css -->

```js
```
<!-- V83 refazer -->
#### Refatora msgns 
**maneira anterior repete muito**
```html
[ngClass]="hasError()"

```

```js
```

#### FormsGroup  --> ngModelGroup
```html
<!-- agrupando formGroup endereço -->

<div ngModelGroup="endereco">
    <!-- campos ref endereços -->
</div>

{ 
    "nome": " ",
    "email": " ",
    "endereco": {
        "campos": " "
    }


}


```


#### Formulario Endereço
**atributo readonly não edita o input**

**viaCep.com.br**


```html
<input type="text" name="cep" ngModel required #cep="ngModel" (blur)="consultaCep($event.target.value)" />

```

```js
// pegou do manual jquery  V85
consultaCep(cep, form) {
    const cep = cep.replace(/\D/g, '');  // somente numericos
    if(cep != '') {
        const validacep = /^[0-9]{8}$/;

        if(validacep.test(cep)) {
            this.   resetaDadosForm(form);
            return this.http.get(`//viacep.com.br/ws/${cep}/json`)
                .map( dados => dados.json())
                .subscribe(dados => {
                    console.log(dados);
                })
        }
    }
}

populeDadosForm(dados, form) {
    form.pathValue({
        // nome: null,
        // email: null,  com path so o que precisa
        endereco: {
            rua: dados.logradouro,
            cep: dados.cep,
            // numero: '',
            complemento: dados.complemento,
            bairro: dados.bairro,
            cidade: dados.cidade,
            estado: dados.uf,

        }

    })
}



// obs: aumentar parametro f
(blur)="consultaCep($event.target.value, f)" />  // 'f'  do formulario
```

<!-- setValue faz atualizacao de TUDO -->
<!-- pathValue faz atualizacao do que foi mudado -->


### Resetar form

```js
resetarDados() {
    formulario.form.patchValue({
        endereco: {
            rua: null,
            cep: null
            complemento: null,
            bairro: null,
            cidade: null,
            estado: null
        }

    })
}
```



```html
```

```js
```




```html
```

```js
```
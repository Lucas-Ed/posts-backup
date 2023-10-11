![](https://bs-uploads.toptal.io/blackfish-uploads/components/seo/content/og_image_file/og_image/1275958/top-18-most-common-angularjs-developer-mistakes-41f9ad303a51db70e4a5204e101e7414.png)

**Passo 1:** Crie um novo componente ou abra um componente existente no qual você deseja adicionar a validação.

Passo 2: Importe as classes necessárias do Angular Forms no arquivo do componente. Essas classes incluem FormGroup, FormControl e Validators. Certifique-se de importá-las no início do seu arquivo:


```
import { FormGroup, FormControl, Validators } from '@angular/forms';
```

**Passo 3:** Crie um objeto FormGroup no método ngOnInit() do seu componente. O FormGroup é uma coleção de objetos FormControl que representa o formulário e seus controles. Adicione um FormControl para cada campo que você deseja validar. Aqui está um exemplo de como criar um formulário de login com campos de e-mail e senha:

```
ngOnInit() {
  this.loginForm = new FormGroup({
    email: new FormControl('', [Validators.required, Validators.email]),
    password: new FormControl('', Validators.required)
  });
}
```
Nesse exemplo, definimos um campo email e um campo password. O primeiro argumento para FormControl é o valor inicial do campo, e o segundo argumento é um array de validadores.

**Passo 4:** No seu modelo de exibição (template), vincule os campos do formulário aos elementos HTML usando a diretiva formControlName. Por exemplo:


```
<form [formGroup]="loginForm" (ngSubmit)="submitForm()">
  <label>Email</label>
  <input type="text" formControlName="email">
  <div *ngIf="loginForm.controls.email.touched && loginForm.controls.email.invalid">
    <div *ngIf="loginForm.controls.email.errors.required">Campo obrigatório.</div>
    <div *ngIf="loginForm.controls.email.errors.email">Email inválido.</div>
  </div>

  <label>Password</label>
  <input type="password" formControlName="password">
  <div *ngIf="loginForm.controls.password.touched && loginForm.controls.password.invalid">
    <div *ngIf="loginForm.controls.password.errors.required">Campo obrigatório.</div>
  </div>

  <button type="submit">Login</button>
</form>
```
Neste exemplo, usamos formControlName para vincular os campos email e password aos elementos <input>. Também usamos *ngIf para exibir mensagens de erro condicionalmente com base no estado de validação de cada campo.

**Passo 5:** No método submitForm(), você pode verificar se o formulário é válido antes de enviar os dados:


```
submitForm() {
  if (this.loginForm.valid) {
    // Envie os dados do formulário
    const formData = {
      email: this.loginForm.value.email,
      password: this.loginForm.value.password
    };
    // Faça o que precisa ser feito com os dados do formulário, como enviar para um servidor

    // Limpe o formulário após o envio
    this.loginForm.reset();
  } else {
    // Trate os erros de validação
    Object.keys(this.loginForm.controls).forEach(field => {
      const control = this.loginForm.get(field);
      if (control.invalid) {
        control.markAsTouched();
      }
    });
    // Exiba uma mensagem de erro na página.
    alert("Por favor, corrija os erros no formulário antes de enviar.");
  }
}

```
Agora você tem um formulário com validação no Angular usando TypeScript. Você pode adicionar mais validadores personalizados, como Validators.minLength ou criar seus próprios validadores personalizados, se necessário.

Lembre-se de importar os módulos necessários no seu módulo principal (por exemplo, FormsModule, ReactiveFormsModule) para que a validação funcione corretamente.

Espero que este tutorial seja útil para você!
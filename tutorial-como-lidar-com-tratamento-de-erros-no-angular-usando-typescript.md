![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS9Lz7V63NzbugiV4Xv5fmpT4LXKKKnZ3EBU14ozvBdo7nn-GraVlWxmdunMx_wZhWHrDc&usqp=CAU)

**Passo 1:** Crie um serviço de tratamento de erros
Crie um serviço separado para tratar erros. Isso ajudará a centralizar a lógica de tratamento de erros e reutilizá-la em toda a aplicação.

**1.1.** Crie um novo serviço usando o comando Angular CLI:

```
ng generate service error-handler
```
**1.2.** Abra o arquivo error-handler.service.ts e adicione o seguinte código:

```
import { ErrorHandler, Injectable, Injector } from '@angular/core';
import { HttpErrorResponse } from '@angular/common/http';
import { Router } from '@angular/router';

@Injectable()
export class ErrorHandlerService implements ErrorHandler {
  constructor(private injector: Injector) {}

  handleError(error: any): void {
    const router = this.injector.get(Router);

    if (error instanceof HttpErrorResponse) {
      // Tratar erros de requisição HTTP
      if (error.status === 401) {
        // Redirecionar para a página de login ou exibir uma mensagem de erro
        router.navigate(['/login']);
      } else if (error.status === 404) {
        // Redirecionar para uma página de erro 404 ou exibir uma mensagem de erro
        router.navigate(['/404']);
      } else {
        // Exibir mensagem de erro genérica
        console.error('Ocorreu um erro na requisição HTTP:', error);
      }
    } else {
      // Tratar outros erros não relacionados à requisição HTTP
      console.error('Ocorreu um erro:', error);
    }
  }
}
```
**Passo 2:** Configurar o serviço de tratamento de erros
**2.1.** Abra o arquivo app.module.ts e importe o serviço ErrorHandlerService:

```
import { ErrorHandlerService } from './error-handler.service';
```
**2.2.** Em seguida, adicione o serviço ao array providers do módulo:

```
@NgModule({
  // ...
  providers: [
    { provide: ErrorHandler, useClass: ErrorHandlerService },
    // ...
  ],
  // ...
})
export class AppModule { }

```
**Passo 3:** Usar o tratamento de erros
Agora que você configurou o serviço de tratamento de erros, pode utilizá-lo em seus componentes e serviços.

**3.1.** Injete o serviço ErrorHandler no componente ou serviço onde você deseja lidar com erros:

```
import { ErrorHandler } from '@angular/core';

constructor(private errorHandler: ErrorHandler) { }
```
**3.2.** Dentro do método onde você deseja lidar com os erros, utilize o serviço para capturar e tratar erros:

```
this.http.get('api/data').subscribe(
  (response) => {
    // Lógica de sucesso
  },
  (error) => {
    this.errorHandler.handleError(error);
  }
);
```
Agora, sempre que ocorrer um erro durante uma requisição HTTP ou em qualquer outro local onde você usar o serviço ErrorHandler, o código dentro do método handleError será executado, permitindo que você trate os erros de forma adequada.

Lembre-se de personalizar as ações de tratamento de erro de acordo com as necessidades específicas da sua aplicação. Você pode exibir mensagens de erro, redirecionar o usuário para páginas específicas ou executar outras ações dependendo do tipo de erro.
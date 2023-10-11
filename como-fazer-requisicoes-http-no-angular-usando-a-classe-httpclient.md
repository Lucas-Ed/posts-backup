Angular HttpClient tutorial; No Angular, usamos a API HttpClient para lidar com as solicitações HTTP. Neste tutorial, você aprenderá como acionar solicitações HTTP em Angular usando a API HttpClient.

![](https://www.positronx.io/wp-content/uploads/2019/06/4439-001.jpg)

Para começar, é preciso importar o módulo HTTPClientModule no módulo principal da aplicação. Em seguida, é preciso injetá-lo em um componente ou serviço através do construtor, como mostrado abaixo:


```
import { HttpClient } from '@angular/common/http';

@Component({
  // ... outras configurações
})
export class MeuComponente {
  constructor(private http: HttpClient) {}
}
```

Agora, já podemos começar a fazer requisições HTTP usando o objeto http. Vamos ver alguns exemplos de como podemos utilizá-lo.

## GET

Para fazer uma requisição GET, basta chamar o método get passando a URL como parâmetro:

```
listarTodosProdutos() {
this.http.get('http://minha-api.com/recursos').subscribe(
  (dados) => {
    console.log(dados);
  },
  (erro) => {
    console.error(erro);
  }
);
}
```
O método get retorna um objeto do tipo Observable, que permite a inscrição em eventos de sucesso ou falha da requisição. No exemplo acima, estamos inscrevendo-nos em ambos os eventos, passando uma função para ser chamada quando a requisição for bem-sucedida (dados são recebidos) e outra para ser chamada quando houver um erro.

## POST
Para fazer uma requisição POST, basta chamar o método post passando a URL e o corpo da requisição como parâmetros:


```
const produto = {
  nome: 'caneta',
  quantdade: 30
};

adicionarProduto(){
this.http.post('http://minha-api.com/recursos', produto).subscribe(
  (dados) => {
    console.log(dados);
  },
  (erro) => {
    console.error(erro);
  }
);
}
```

## PUT e DELETE
Para fazer uma requisição PUT ou DELETE, basta seguir a mesma lógica, chamando os métodos put ou delete respectivamente:


```
// PUT
const produto = {
  nome: 'caneta',
  quantdade: 30
};
alterarProduto(){
this.http.put('http://minha-api.com/recursos/1', produto).subscribe(
  (dados) => {
    console.log(dados);
  },
  (erro) => {
    console.error(erro);
  }
);
}
```
## DELETE


```
// DELETE
excluirProduto(){
this.http.delete('http://minha-api.com/recursos/1').subscribe(
  (dados) => {
    console.log(dados);
  },
  (erro) => {
    console.error(erro);
  }
);
}
```

## Configurando a interface do componente
Sabendo que temos 4 tipos de requisições possíveis na API, vamos adicionar a mesma quantidade de botões no AppComponent, um para cada request. Para isso, apagaremos todo o conteúdo do app.component.html e adicionaremos o código abaixo:

```
<button (click)="listarTodosProdutos()">GET</button>
<button (click)="adicionarProduto()">POST</button>
<button (click)="alterarProduto()">PUT</button>
<button (click)="excluirProduto()">DELETE</button>
```

## Tratamento de erros
É comum querer tratar erros de maneira mais específica em cada requisição, e para isso o HTTPClient fornece o método handleError, que pode ser usado da seguinte maneira:


```
import { HttpErrorResponse } from '@angular/common/http';

private tratarErro(erro: HttpErrorResponse) {
  if (erro.error instanceof ErrorEvent) {
    //// Ocorreu um erro do lado do cliente ou da rede. Trate-o de acordo.
    console.error('Ocorreu um erro:', erro.error.message);
  } else {
    // O back-end retornou um código de resposta malsucedido.
    // O corpo da resposta pode conter pistas sobre o que deu errado,
    console.error(
      `Backend returnou um código de ${erro.status}, ` + `body was: ${erro.error}`
    );
  }
  // retornar um observável com uma mensagem de erro voltada para o usuário
  return throwError('Algo ruím aconteceu; por favor, tente novamente mais tarde.');
};

this.http.get('http://minha-api.com/recursos').subscribe(
  (dados) => {
    console.log(dados);
  },
  (erro) => this.tratarErro(erro)
);

```

# Requisições tipadas
Projetos Angular usam a linguagem TypeScript por padrão, o que nos permite desfrutar dos recursos que essa linguagem oferece. Entre eles está a tipagem estática, que é a possibilidade de fixar o tipo de uma variável no momento da sua declaração.

Uma das possíveis aplicações para esse recurso é na definição das classes que representam os dados/entidades da nossa aplicação. Por exemplo, seguindo a ideia que desenvolvemos anteriormente, podemos criar uma classe Produto representando esse tipo que trafega entre a SPA e a API (e que possivelmente seria vinculado a inputs, por exemplo, para exibição e captura de dados em um projeto real).

Fazendo isso, podemos tipar também o retorno das requisições HTTP, de forma que nós, ou quem precisar manter nosso código, saberemos o que esperar como resultado de cada request.

Para exemplificar, vamos criar uma classe chamada Produto. Para isso adicionaremos uma pasta models e dentro dela o arquivo produto.model.ts ao projeto contendo o seguinte código:


```
export class Produto {
    id : number;
    nome : string;
}
```
Em seguida, importaremos esse tipo no AppComponent para que possamos usá-lo nas requisições:


```
import { Produto } from './models/produto.model';
```
Feito isso, podemos agora especificar o tipo de retorno das requisições GET. No caso do método listarTodosProdutos, o tipo de retorno será Produto[ ], ou seja, um array de produtos. Já no listarProdutoPorId o tipo é apenas Produto, posto que apenas um item é retornado.Abaixo vemos como fica a requisição GET:


```
listarTodosProdutos() {
  this.http.get<Produto[]>(`${ this.apiURL }/produtos`)
            .subscribe(resultado => console.log(resultado));
}
```
Ao fazer isso, também contamos com um auxílio a mais do editor, que passa a mostrar o tipo do resultado.
Já na requisição POST podemos especificar o tipo tanto no corpo da requisição, quanto na resposta, assim como mostra a seguir:


```
adicionarProduto() {
  var produto = new Produto();
  produto.nome = "Cadeira Gamer";

  this.http.post<Produto>(`${ this.apiURL }/produtos`, produto)
  //restante do código sem alterações
}
```

O mesmo ocorre com a requisição PUT, porém como seu retorno esperado é 204 (No Content), ela não deve ser tipada como Produto, pois o corpo da resposta virá vazio.

Assim finalizamos este conteúdo sabendo realizar diferentes tipos de requisição HTTP no Angular, seja com objetos dinâmicos ou tipados.
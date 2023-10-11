O Axios é uma biblioteca Frontend que pode ser usada para fazer requisições HTTP de maneira fácil e rápida. Ele é amplamente utilizado em aplicações web e mobile para se conectar com APIs REST e outros serviços de back-end. Neste artigo, vamos ver como utilizar o Axios para fazer requisições HTTP em uma API REST.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--FckeNU0D--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/36k73z7ceesz2jvrsi74.png)

Para começar, é necessário instalar o Axios em sua aplicação. Você pode fazer isso utilizando o npm (gerenciador de pacotes do Node.js) ou o yarn (outro gerenciador de pacotes). Abra o terminal e digite o seguinte comando:

```
npm install axios
```
ou

```
yarn add axios
```
Agora, vamos importar o Axios em seu código, você pode fazer isso adicionando a seguinte linha no início do seu arquivo:

```javascript
import axios from 'axios';
```

Com o Axios instalado e importado em seu código, você pode começar a fazer requisições HTTP. O Axios possui uma sintaxe bastante simples, permitindo que você faça requisições GET, POST, PUT, DELETE e outras de maneira fácil.

Aqui está um exemplo de como fazer uma requisição GET utilizando o Axios:


```javascript
axios.get('https://api.exemplo.com/users')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.log(error);
  });
```

Neste exemplo, estamos fazendo uma requisição GET para a URL https://api.exemplo.com/users. Quando a requisição é concluída com sucesso, o objeto de resposta é passado para o bloco then, onde podemos acessar os dados retornados pela API através da propriedade response.data. Se ocorrer algum erro durante a requisição, o bloco catch será executado e o erro será passado para ele.

Você também pode adicionar parâmetros de consulta à sua requisição utilizando a propriedade params da seguinte maneira:


```javascript
axios.get('https://api.exemplo.com/users', {
  params: {
    id: 12345
  }
})
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.log(error);
  });
```
Isso fará com que a URL da sua requisição seja https://api.exemplo.com/users?id=12345

Além de fazer requisições GET, o Axios também permite que você faça requisições POST, PUT e DELETE de maneira muito similar.

Aqui está um exemplo de como fazer uma requisição POST utilizando o Axios:


```javascript
axios.post('https://api.exemplo.com/users', {
  name: 'John',
  age: 30
})
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.log(error);
  });
```

Neste exemplo, estamos fazendo uma requisição POST para a URL https://api.exemplo.com/users com alguns dados na carga útil da requisição (name e age). Quando a requisição é concluída com sucesso, o objeto de resposta é passado para o bloco then, onde podemos acessar os dados retornados pela API através da propriedade response.data. Se ocorrer algum erro durante a requisição, o bloco catch será executado e o erro será passado para ele.

Aqui está um exemplo de como fazer uma requisição PUT utilizando o Axios:


```javascript
axios.put('https://api.exemplo.com/users/12345', {
  name: 'Jane',
  age: 35
})
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.log(error);
  });
```

Neste exemplo, estamos fazendo uma requisição PUT para a URL https://api.exemplo.com/users/12345 com alguns dados na carga útil da requisição (name e age). Quando a requisição é concluída com sucesso, o objeto de resposta é passado para o bloco then, onde podemos acessar os dados retornados pela API através da propriedade response.data. Se ocorrer algum erro durante a requisição, o bloco catch será executado e o erro será passado para ele.

Por último, aqui está um exemplo de como fazer uma requisição DELETE utilizando o Axios:


```javascript
axios.delete('https://api.exemplo.com/users/12345')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.log(error);
  });
```

Neste exemplo, estamos fazendo uma requisição DELETE para a URL https://api.exemplo.com/users/12345. Quando a requisição é concluída com sucesso, o objeto de resposta é passado para o bloco then, onde podemos passar a data a ser deletado, se ouver erro usamos o catch para exibi-lo no console.

### Referências:
[Axios](https://axios-http.com/ptbr/docs/intro)
[Rocketseat](https://blog.rocketseat.com.br/axios-um-cliente-http-full-stack/)
[Devmedia](https://www.devmedia.com.br/consumindo-uma-api-com-react-js-e-axios/42900)
[Alura](https://www.alura.com.br/artigos/requisicoes-http-utilizando-axios)
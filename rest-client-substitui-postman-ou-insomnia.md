Se você trabalha com API Rest, deve conhecer aplicações como [Postman](https://www.postman.com) ou [Insomnia](https://insomnia.rest/download), as quais têm como função enviar uma requisição para uma API e obter uma resposta. De fato, tais aplicações trabalham muito bem e são fáceis de utilizar, basta pouco tempo para entender como funcionam suas funções básicas.

![](https://deviniciative.files.wordpress.com/2019/06/1-uhzoof1etgckn9_xisst4w.png)

Mas por melhor que sejam, quando trabalhamos em equipe, podemos encontrar dificuldades. Você provavelmente já se viu na seguinte situação: Surge uma necessidade de adicionar paginação em uma listagem de usuários, então o desenvolvedor back-end realiza as alterações necessárias na API, atualiza o seu ambiente de teste no Postman e gera um arquivo JSON de exportação, para enviar ao desenvolvedor front-end, ou qualquer outro, o qual precisará testar a API.

Em um cenário como esse, seria interessante versionar o arquivo do Postman, logo economizaria tempo de outros desenvolvedores, assim ao atualizar a versão da API, já teria as requisições enviando os novos parâmetros necessários. Porém, o processo ainda seria demorado, pois precisaríamos importar o novo arquivo dentro da aplicação.

Para solucionar esse problema há como alternativa uma extensão presente no [Visual Studio Code](https://code.visualstudio.com) chamada [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client), essa extensão realiza requisições na API e exibe a sua resposta como vemos no exemplo:

![](https://miro.medium.com/max/640/1*uCrQRx4oJSTWRkzc6rYrlg.webp)

## Mas como faço isso funcionar?
O processo é bastante simples, segue um passo a passo de como instalar e criar a estrutura de arquivos:

1. Busque pela extensão REST Client e instale-a;

![](https://miro.medium.com/max/720/1*vWseU88ujqYi51NqlDGsIQ.webp)

2. Crie uma pasta junto com sua aplicação com o nome test e um arquivo com o nome de sua preferência com a extensão .http;

![](https://miro.medium.com/max/606/1*LneuZ21MRrxWkN7DUwT2Bg.webp)

3. No arquivo recém criado, vamos escrever a requisição da rota da sua aplicação veja o exemplo`http://localhost:3000/notifications`

![](https://i.postimg.cc/J4JHYWvB/Sem-t-tulo.png)

4. Pronto, basta clicar em “Send Resquest” para executar a requisição.

![](https://i.postimg.cc/QNvWqM43/Sem-t-tulo1.png)

## Mais de uma requisição
Para adicionar mais de uma requisição é necessário adicionar um comentário ###. Para ficar melhor organizado você pode adicionar um indicativo para cada uma das requisições, como na foto acima

# Considerações finais
É claro que as ferramentas Postman e Insomnia são excelentes e bastante completas, a intenção deste artigo não é criticar ambas e sim apresentar uma solução alternativa, e que pode ser mais prática de acordo com a sua necessidade.
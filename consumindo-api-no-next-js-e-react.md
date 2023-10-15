Para a construção desse exemplo de como consumir uma API no Next.js e React, você precisará usar os comandos em seu cmd dentro da pasta do projeto, lembre-se de estar com o npm ou yarn instalados em seu pc. Vamos criar aplicação next e instalar a dependência axios.
Comandos:

```
npm install --save next react react-dom

npm install --save axios
```
Axios é um cliente HTTP baseado em Promises para fazer requisições. Pode ser utilizado tanto no navegador quanto no Node.js.
Após obtermos os dados com o response (última parte do artigo), usamos o map() para percorrer e nos mostrar os dados obtidos.

![](https://media-exp1.licdn.com/dms/image/C5612AQG6pE9yqgcEMg/article-inline_image-shrink_1500_2232/0/1632888933872?e=1675296000&v=beta&t=MR7b-dXdMOyN6WTiHc5IUCDZ60SbzzAp-Krsmu5nSDI)

Essa é a parte em que possuímos um método estático chamado getInitialProps que é responsável por fazer  qualquer ação assíncrona que precisa ser realizada antes do componente ser exibido  em tela como, por exemplo, uma chamada à API REST.
Então dentro do axios.get() colocamos nossa URL a ser consumida.
Url: https://sujeitoprogramador.com/rn-api/?api=posts

![](https://media-exp1.licdn.com/dms/image/C5612AQFnlKzh03bAnA/article-inline_image-shrink_1500_2232/0/1632888647958?e=1675296000&v=beta&t=h_XeJgLyAOBZKEC8FOAgpKN6qRQmf_L7v134t2BmCeE)
Para rodar o servidor no localhost, devemos usar o comando:
`npm rum dev `

Pronto!
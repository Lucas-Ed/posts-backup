Antes de instalar o Tailwind CSS e integrá-lo em seu projeto, certifique-se disso:

Você tem o Node.js instalado em seu computador para fazer uso do gerenciador de pacotes Node (npm) no terminal.
Seu projeto está todo configurado com seus arquivos criados.
Esta é a aparência da nossa estrutura de projeto no momento:

```
-Tailwind-tutorial
    -public
        -index.html
        -styles.css
    -src
        -styles.css
```        
 Em seguida, inicie um terminal para o seu projeto e execute os seguintes comandos:
` npm install -D tailwindcss`
O comando acima instalará o framework Tailwind CSS como uma dependência. Em seguida, gere seu arquivo tailwind.config.js executando o comando abaixo:
` npm install -D tailwindcss `
O arquivo tailwind.config.js estará vazio quando criado, então nós temos que adicionar algumas linhas de código:

```
 module.exports = {
  content: ["./src/**/*.{html,js}", "./public/*.html"],
  theme: {
    extend: {},
  },
  plugins: [],
}; 
```
Os caminhos de arquivo fornecidos na matriz de conteúdo permitirão que o Tailwind purgue/remova qualquer estilo não utilizado durante o tempo de construção.
A próxima coisa a fazer é adicionar as diretrizes “@tailwind” ao seu arquivo CSS na pasta src – aqui é onde Tailwind gera todos os seus estilos de utilidade pré-definidos para você:

```
@tailwind base;
@tailwind components;
@tailwind utilities; 
```
A última coisa a fazer é iniciar o processo de construção executando este comando no seu terminal:
`  npx tailwindcss -i ./src/styles.css -o ./public/styles.css --watch `

No código acima, estamos dizendo ao Tailwind que nosso arquivo de entrada é a folha de estilo na pasta src e que qualquer estilo que nós usamos tem que ser construído no arquivo de saída na pasta pública. --watch permite que o Tailwind assista seu arquivo para mudanças para um processo de construção automática; omitir isso significa que nós temos que executar esse script toda vez que queremos construir nosso código e ver a saída desejada.

## Usando CSS Tailwind

Agora que instalamos e montamos o Tailwind CSS para nosso projeto, vamos ver alguns exemplos para entender completamente sua aplicação.
### Exemplo Flexbox
Para usar flex no Tailwind CSS, você precisa adicionar uma classe de flex e, em seguida, a direção dos itens flex:

```
<div class="flex flex-row">
      <button> Button 1 </button>
      <button> Button 2 </button>
      <button> Button 3 </button>
    </div>
```

 ![](https://kinsta.com/wp-content/uploads/2022/01/flexbox-container-1024x582.png)
    Usando `flex-row-reverse` irá reverter a ordem na qual os botões aparecem.


`flex-col` os empilha uns sobre os outros. Aqui está um exemplo:
```
<div class="flex flex-col">
      <button> Button 1 </button>
      <button> Button 2 </button>
      <button> Button 3 </button>
 </div>
```
    
![](https://kinsta.com/wp-content/uploads/2022/01/flex-col-1024x582.png)
Assim como o exemplo anterior, `flex-col-reverse` reverte a ordem.

  **## Exemplo de grade**
Ao especificar colunas e linhas no sistema de grade, nós adotamos uma abordagem diferente, passando em um número que irá determinar como os elementos irão ocupar o espaço disponível:    
```
<div class="grid grid-cols-3">
      <button> Button 1 </button>
      <button> Button 2 </button>
      <button> Button 3 </button>
      <button> Button 4 </button>
      <button> Button 5 </button>
      <button> Button 6 </button>
    </div>
```
![](https://kinsta.com/wp-content/uploads/2022/01/grid-col-1024x582.png)

# Cores
O Tailwind CSS vem com um monte de cores pré-definidos. Cada cor tem um conjunto de variações diferentes, com a variação mais clara sendo 50 e a mais escura sendo 900.

Aqui está uma imagem de múltiplas cores e seus códigos HTML hexadecimais para ilustrar isto
![](https://kinsta.com/wp-content/uploads/2022/01/tailwind-color-variants-1024x617.png)

Vamos dar um exemplo de como você pode fazer isso usando a cor vermelha acima para dar a um elemento de botão uma cor de fundo:
`<button class="bg-red-50">Click me</button>`
Esta sintaxe é a mesma para todas as cores em Tailwind, exceto para preto e branco, que são escritas da mesma maneira, mas sem o uso de números `bg-black` e `bg-white`.

Para adicionar a cor do texto, você usa a classe `text-{color}`:
`<p class="text-yellow-600">Hello World</p>`

# Padding
O Tailwind CSS já tem um sistema de design que o ajudaria a manter uma escala consistente em todos os seus designs. Tudo que você tem que saber é a sintaxe para aplicar cada utilidade.

A seguir estão as utilidades para adicionar padding aos seus elementos:

- `p` denota o preenchimento de todo o elemento.
- `py` denota padding padding-top e padding-bottom.
- `px` denota padding-esquerda e padding-direita.
- `pt` denota padding-top.
- `pr` denota padding-direita.
- `pb` denota padding-baixo.
- `pl` denota padding-esquerda

Para aplicá-los aos seus elementos, você teria que usar os números apropriados fornecidos pelo Tailwind – um pouco parecidos com os números que representavam as variantes de cores na última seção. Aqui está o que queremos dizer:

```
<button class="p-0">Click me</button>
<button class="pt-1">Click me</button>
<button class="pr-2">Click me</button>
<button class="pb-3">Click me</button>
<button class="pl-4">Click me</button>
```
# Margem
As utilidades pré-definidas para padding e margem são muito similares. Você tem que substituir o `p` por um `m`:
- `m`
- `my`
- `mx`
- `mt`
- `mr`
- `mb`
- `ml`

# Como criar um plugin com o Tailwind CSS
Mesmo que o Tailwind CSS tenha muitas utilidades e sistemas de projeto já construídos para você, ainda é possível que você tenha uma funcionalidade particular que você gostaria de adicionar para estender o que o Tailwind pode ser usado. O Tailwind CSS nos permite fazer isso através da criação de um plugin.

Vamos sujar nossas mãos criando um plugin que adiciona a cor aqua e um utilitário de rotação que gira um elemento 150º no eixo X. Vamos fazer esses utilitários no arquivo tailwind.config.js usando um pouco de JavaScript.

```
const plugin = require("tailwindcss/plugin");

module.exports = {
  content: ["./src/**/*.{html,js}", "./public/*.html"],
  theme: {
    extend: {},
  },
  plugins: [
    plugin(function ({ addUtilities }) {
      const myUtilities = {
        ".bg-aqua": { background: "aqua" },
        ".rotate-150deg": {
          transform: "rotateX(150deg)",
        },
      };
      addUtilities(myUtilities);
    }),
  ],

};
```
Agora, vamos quebrar isso. A primeira coisa que fizemos foi importar a função de plugin do Tailwind:

```
const plugin = require("tailwindcss/plugin");
```
Então nós continuamos a criar nossos plugins na matriz de plugins:

```
 plugins: [
    plugin(function ({ addUtilities }) {
      const newUtilities = {
        ".bg-aqua": { background: "aqua" },
        ".rotate-150deg": {
          transform: "rotateX(150deg)",
        },
      };
      addUtilities(newUtilities);
    }),
  ],
```
Você pode ter que reexecutar o script de construção depois de fazer seu plugin.

Agora que os plugins estão prontos, nós podemos testá-los:

```
<button class="bg-aqua rotate-150deg">Click me</button>
```
Se você fez tudo certo, você deve ter um botão com uma cor aqua com o texto girado a 150º no eixo X.
![](https://user-images.githubusercontent.com/321738/63501763-88dbf600-c4cc-11e9-96cd-94adadc2fd72.png)

O Storybook é uma ferramenta muito útil para desenvolvedores de aplicações React. Ele permite criar e testar componentes de forma isolada, sem a necessidade de criar um aplicativo completo. Isso facilita o desenvolvimento e permite que os desenvolvedores criem componentes reutilizáveis e consistentes em suas aplicações.

![](https://miro.medium.com/max/720/1*WDA4H4IVKaBnliEcDJhlqw.webp)

Para começar a usar o Storybook com o React, você primeiro precisa instalar o pacote npm do Storybook. Isso pode ser feito executando o seguinte comando no seu terminal:

```
npx storybook init
```
Em seguida, você precisa inicializar o Storybook em seu projeto React. Isso pode ser feito executando o comando a seguir no terminal:

```
getstorybook
```
Isso criará uma nova pasta chamada `.storybook` em seu projeto, onde todos os arquivos do Storybook serão armazenados.

E acessar a url indicada, que no meu caso é: http://localhost:6006
Ao acessar a url indicada, é possível visualizar o storybook com algumas stories de exemplo:

![](https://i.postimg.cc/Yq1yxrtd/story.png)

Antes de irmos pra próxima etapa vamos mudar o nosso thema de light pra dark, e tbm da aba docs, para fazermos isso vamos criar um arquivo dentro do diretório `.storybook` com o nome `manager.js`, no arquivo manager vamos fazer a configuraçao da seguinte maneira:

```js
import {addons} from '@storybook/addons';
import {themes} from '@storybook/theming';

addons.setConfig({
    theme: themes.dark,
})
```
Para mudar o thema da aba docs é só incluir no arquivo preview.js:
o `import {themes} from '@storybook/theming';` e dentro da função principal:

```js
docs: {
    theme: themes.dark,
  }
```
Pronto agora agrada aos olhos, rsrsrs

![](https://i.postimg.cc/wTnkgzWh/ererhrhr.png)

Agora você está pronto para começar a criar seus próprios componentes de stories. É possível navegar no menu lateral e ver o componente Button funcionando.

Se acessarmos nosso projeto, podemos observar que foi criado uma pasta .storybook dentro do diretório raiz da aplicação. Essa pasta contém arquivos referente as configurações do storybook.


```js
import { configure } from '@storybook/react';
function loadStories() {
  require('../src/stories');
}
configure(loadStories, module);
```

A função loadStories importa o arquivo `src/stories/index.js`, que por sua vez, contém a definição das stories, conforme abaixo:


```js
import React from 'react';

import { storiesOf } from '@storybook/react';
import { action } from '@storybook/addon-actions';
import { linkTo } from '@storybook/addon-links';

import { Button, Welcome } from '@storybook/react/demo';

storiesOf('Welcome', module).add('to Storybook', () => <Welcome showApp={linkTo('Button')} />);

storiesOf('Button', module)
  .add('with text', () => <Button onClick={action('clicked')}>Hello Button</Button>)
  .add('with some emoji', () => <Button onClick={action('clicked')}>😀 😎 👍 💯</Button>);
```
Cada componente tem suas próprias stories, de modo que cada uma represente um estado dele. Com isso, podemos construir e testar cada componente de forma isolada, o que nos leva a ter mais controle no processo de desenvolvimento.

Seguindo o código acima, o método `storiesOf` é responsável por inicializar as stories de um componente, e ele espera como primeiro parâmetro o nome do componente (que é o nome que aparecerá naquele menu lateral) e como segundo parâmetro, a variável global module. A funcão `storiesOf` retorna um objeto que contém o método add, que será utilizado para adicionar novas stories ao componente.

No exemplo acima, está sendo definido uma story para o componente Welcome, com a descrição “to Storybook”. Também estão sendo defininidas as stories para o componente Button: “with text” e “with some emoji”.

Outra coisa que podemos ver no arquivo de exemplo, é o uso da função action e linkTo. A funcão action é utilizada para criar funções mocks que podem ser passadas como callbacks através das props. Quando os mocks são executados, eles geram um log que aparece no storybook, o que é útil para debugging. A função linkTo por sua vez, cria links para outras stories.

Agora vamos ver exemplos que se aproximam mais de casos reais.

## Button
Vamos criar um componente Button, que possui algumas variações de estado:

Primeiramente, crie uma pasta Button dentro de src. Dentro dela crie um arquivo `Button.jsx` e outro arquivo `Button.css`. A estrutura desses arquivos deve estar da seguinte maneira:
O arquivo `.storybook/config.js` é o responsável por carregar as stories do projeto e ele contém o seguinte código:


```
src/
  Button/
    Button.jsx
    Button.css
```

O código para o componente será o seguinte:

```js
import React from 'react';
import './Button.css';

const Button = ({ children, onClick, disabled }) => (
  <button
    onClick={onClick}
    disabled={disabled}
    className={`button ${disabled ? 'button--disabled' : ''}`}
  >
    {children}
  </button>
);

export default Button;
```
No código acima, nós definimos o componente Button, que aceita as props: children, onClick e disabled.

Essas três props nós repassamos para o elemento button do html. Porém, nós também utilizamos a prop disabled para inserir ou não o class name: button--disabled que será utilizado para estilizar o componente no respectivo estado.

Para estilizar o componente acima, o arquivo Button.css deve conter o seguinte código:


```css
.button {
  background: #3498db;
  border: 0;
  border-radius: 10px;
  padding: 15px;
  font-size: 15px;
  color: #ffffff;
}

.button--disabled {
  opacity: 0.7;
  cursor: not-allowed;
}
```

O arquivo acima possui um estilo padrão para o componente através da classe `.button` e possui um estilo adicional para o estado disabled, através da classe `.button--disabled`

Por último, criaremos as stories do nosso componente. Substitua o código do arquivo `src/stories/index.js` pelo seguinte:


```js
import React from 'react';

import { storiesOf } from '@storybook/react';
import { action } from '@storybook/addon-actions';

import Button from '../Button/Button';

storiesOf('Button', module)
  .add('default', () => (
    <Button onClick={action('clicked')}>Button</Button>
  ))
  .add('disabled', () => (
    <Button onClick={action('clicked')} disabled>Hello Button</Button>
  ));
```
No arquivo acima, nós importamos o componente Button e criamos duas stories para o mesmo. Cada story possui uma utilização básica do componente. A primeira story nós só passamos um callback para a prop `onClick`, e sendo assim, o button assumirá seu estado padrão. Na segunda story, além da prop `onClick`, nós passamos a prop disabled, para que nessa story o componente assuma o respectivo estado.

Feito isso, acesse novamente o storybook no seu navegador e veja o resultado.

![](https://i.postimg.cc/Rh96dMTz/btn.png)

# Conclusão
Vimos que é possível criar cada componente de forma independente, isso nos dá mais controle do desenvolvimento e também nos compele a construir componentes mais resilientes, pensando em como eles irão se comportar em cada situação.

Aproveite que as stories estão configuradas e carregando automaticamente e crie um novo componente com novas stories. A melhor maneira de aprender e fixar o conhecimento, é praticando.

Gostou do post e achou útil? Ajude a divulgar para que mais pessoas tenham acesso! ❤️ ️


[Referência-01](https://www.youtube.com/watch?v=VmPbKj3uekE)
[Referência-02](https://storybook.js.org/tutorials/design-systems-for-developers/react/pt/document/)
[Referência-03](https://www.youtube.com/watch?v=WwiU6chNl4U)
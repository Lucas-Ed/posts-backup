![](https://miro.medium.com/v2/resize:fit:1200/1*vj_VVGBUs-K9NksbZjdeeg.png)

**Passo 1:** Configurando o projeto React com TypeScript

Crie um novo projeto React com TypeScript usando o comando npx create-react-app nome-do-projeto --template typescript.
Navegue até a pasta do projeto usando o comando cd nome-do-projeto.
Inicie o servidor de desenvolvimento com o comando npm start.

**Passo 2:** Criando um componente de formulário

Crie um novo componente de formulário. Por exemplo, crie um arquivo chamado Formulario.tsx na pasta src.
Dentro do componente Formulario, defina uma interface para o estado inicial com os campos que você deseja validar. Por exemplo:

```
import React, { useState } from 'react';

interface FormState {
  nome: string;
  email: string;
  senha: string;
}

const Formulario: React.FC = () => {
  const [form, setForm] = useState<FormState>({
    nome: '',
    email: '',
    senha: ''
  });

  // Restante do código...
}

```
Crie manipuladores de mudança para atualizar o estado do formulário. Por exemplo:

```
const handleNomeChange = (event: React.ChangeEvent<HTMLInputElement>) => {
  setForm({ ...form, nome: event.target.value });
}

const handleEmailChange = (event: React.ChangeEvent<HTMLInputElement>) => {
  setForm({ ...form, email: event.target.value });
}

const handleSenhaChange = (event: React.ChangeEvent<HTMLInputElement>) => {
  setForm({ ...form, senha: event.target.value });
}

```
Renderize o formulário JSX com os campos e os respectivos manipuladores de mudança. Por exemplo:

```
return (
  <form>
    <label>
      Nome:
      <input type="text" value={form.nome} onChange={handleNomeChange} />
    </label>
    <label>
      Email:
      <input type="email" value={form.email} onChange={handleEmailChange} />
    </label>
    <label>
      Senha:
      <input type="password" value={form.senha} onChange={handleSenhaChange} />
    </label>
    <button type="submit">Enviar</button>
  </form>
);

```
**Passo 3:** Adicionando validação aos campos

Declare um estado para armazenar os erros de validação. Por exemplo:

```
const [erros, setErros] = useState<Partial<FormState>>({});
```
Crie uma função de validação para verificar os campos e atualizar os erros. Por exemplo:

```
const validarCampos = () => {
  const novosErros: Partial<FormState> = {};

  // Validação do campo nome
  if (form.nome.trim() === '') {
    novosErros.nome = 'Por favor, digite o seu nome.';
  }

  // Validação do campo email
  if (form.email.trim() === '') {
    novosErros.email = 'Por favor, digite o seu email.';
  } else if (!/\S+@\S+\.\S+/.test(form.email)) {
    novosErros.email = 'Por favor, digite um email válido.';
  }

  // Validação do campo senha
  if (form.senha.trim() === '') {
    novosErros.senha = 'Por favor, digite a sua senha.';
  }

  setErros(novosErros);
}

```
Chame a função de validação quando o formulário for enviado. Por exemplo, adicione o seguinte código à função return:

```
<button type="submit" onClick={validarCampos}>Enviar</button>

```
Renderize as mensagens de erro na interface, abaixo de cada campo correspondente. Por exemplo:

```
<label>
  Nome:
  <input type="text" value={form.nome} onChange={handleNomeChange} />
  {erros.nome && <span>{erros.nome}</span>}
</label>
<label>
  Email:
  <input type="email" value={form.email} onChange={handleEmailChange} />
  {erros.email && <span>{erros.email}</span>}
</label>
<label>
  Senha:
  <input type="password" value={form.senha} onChange={handleSenhaChange} />
  {erros.senha && <span>{erros.senha}</span>}
</label>

```
**Passo 4:** Finalizando a validação

Para evitar o envio do formulário caso haja erros de validação, você pode adicionar uma verificação antes de realizar a submissão. Por exemplo, atualize a função validarCampos da seguinte maneira:


```
const validarCampos = (event: React.FormEvent) => {
  event.preventDefault();

  const novosErros: Partial<FormState> = {};

  // Validação dos campos...

  if (Object.keys(novosErros).length === 0) {
    // Realize as ações desejadas após a validação bem-sucedida, como enviar dados para um servidor.
    console.log('Formulário válido. Envie os dados:', form);
  } else {
    setErros(novosErros);
  }
}
```
No formulário, atualize o atributo onClick do botão "Enviar" para chamar a função validarCampos. Por exemplo:

```
<button type="submit" onClick={validarCampos}>Enviar</button>

```
Agora você tem um componente de formulário no React com validação básica usando TypeScript. Certifique-se de adaptar a validação de acordo com suas necessidades e requisitos específicos.
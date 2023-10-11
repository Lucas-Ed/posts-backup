![](https://i.postimg.cc/y8BWjxNS/foto.png)
Neste tutorial, vamos mostrar como enviar e-mails usando o serviço de Envio de E-mail Bun.sh e a biblioteca Resend em Node.js e Python. Vamos começar com Node.js:

## Node js

1. Configuração Inicial
Primeiro, certifique-se de ter o **Node.js** instalado em seu sistema, este tutorial da versão do node pode ser feito usando o sistema opracional Linux ou um subsistema Linux no Windows 10, vou partir do pressuposto que você tenha o **[bun](https://bun.sh)** instalado no sistema; se não estiver instalado, instale com o comando <code>curl -fsSL https://bun.sh/install | bash</code> Você também precisará criar uma conta no site do Bun e obter suas credenciais de API; com o bun instalado instale o [Resend](https://resend.com), com o comando `bun install resend`

2. Criar um Projeto Node.js
Crie um novo diretório para o seu projeto e navegue até ele no terminal.

```
mkdir env-email
cd env-email
```
Em seguida, inicie um projeto Node.js usando o seguinte comando:

```
npm init -y
```
3. Instale as Dependências
Instale a biblioteca resend para simplificar o envio de e-mails com o Envio de E-mail Bun.sh:

```
npm install resend
```
4. Escreva o Código
Crie um arquivo JavaScript, por exemplo, index.js, e adicione o seguinte código:


```js
import { Resend } from 'resend';

const resend = new Resend('</Sua-chave-de-api-aqui>');

resend.emails.send({
    from: 'onboarding@resend.dev',
    to: '<por-e-mail-de-destino-aqui>',
    subject: 'Bun + Resend',
    html: '<p>Primeiro teste de envio de e-mail, usando Node, concluído com <strong>sucesso !!!</strong>!</p>'
})
.then(response => {
    console.log("E-mail enviado !!!");
})
.catch(error => {
    console.log("Envio do e-mail falhou !!!");
})
```
Substitua a variável `const resend` adicionando sua chave de api em: `</Sua-chave-de-api-aqui>`, e também o destinatário do e-mail, em `to: '<por-e-mail-de-destino-aqui>'`.

5. Execute o Código
```
bun index.js
```

Se o script rodar corretamente, você receberá um e-mail no destinatário assim:

![](https://i.postimg.cc/CxHrJXdJ/Whats-App-Image-2023-09-20-at-00-43-01.jpg)

Agora, vamos mostrar como fazer a mesma coisa em Python:

## Python
1. Configuração Inicial
Certifique-se de ter o Python instalado em seu sistema.

2. Crie o ambiente virtual

```
python -m venv venv
```
3. Ative o ambiente virtual
```
source venv/Scripts/Activate
```

4. Instale bliblioteca necessária

```
pip install resend && pip install python-dotenv && pip install os
```

5. Crie em arquivo .env para sua chave api igual o exemplo:

```
API_KEY=<SUA-API-AQUI>
```
substitua `<SUA-API-AQUI>` pela sua chave.

6. Escreva o Código
Crie um arquivo Python, por exemplo, index.py, e adicione o seguinte código:


```python
import resend
import os
from dotenv import load_dotenv

# lê as variáveis de ambiente
load_dotenv()

key = os.getenv("API_KEY")

resend.api_key = key


r = resend.Emails.send({
    "from": "onboarding@resend.dev",
    "to": "<por-e-mail-de-destino-aqui>",
    "subject": 'Bun + Resend',
    "html": "<p>Primeiro teste de envio de e-mail, usando python, concluído com <strong>sucesso !!!</strong>!</p>"
})
print("E-mail enviado com sucesso!")

```
Substitua `"to": "<por-e-mail-de-destino-aqui>"`, pelo seu e-mail do destinatário de sua preferência.

4. Execute o Código
```
// no windows
python index.py

//no Linux
python3 index.py
```
Se o script rodar corretamente, você receberá um e-mail no destinatário assim:

![](https://i.postimg.cc/CKhP27q0/Whats-App-Image-2023-09-20-at-00-43-01-1.jpg)

Isso é tudo! Agora você pode enviar e-mails usando o Envio de E-mail Bun.sh e a biblioteca Resend tanto em Node.js quanto em Python. Certifique-se de substituir as informações de configuração com suas próprias credenciais e detalhes de e-mail.

Veja este projeto no meu github [aqui.](https://github.com/Lucas-Ed/env-email)

[Referência](https://www.youtube.com/watch?v=wWQ4gnvS020)
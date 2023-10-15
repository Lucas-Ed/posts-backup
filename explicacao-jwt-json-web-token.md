Olá pessoal!

Neste artigo vamos explorar um pouco do mundo de API’s e microservices e também como eles se comunicam, utilizando uma das arquiteturas de segurança mais populares do mundo.

# O que é o JWT ?
JWT é um token, nada mais. Seu objetivo é prover uma comunicação eficiente e leve entre, principalmente mas não só, API’s e microservices. As principais características do JWT são:

Baseado no standard RFC7519 da W3C
- Usado para realizar comunicação segura de objetos JSON mesmo em conexões inseguras como HTTP
- Ele tem um Header, um Payload e uma assinatura
- Auto-contido, ele contém toda a informação necessária para decriptar o mesmo (exceto o secret)
O JWT segue este fluxo:
[](https://miro.medium.com/max/720/0*8isWdh0wkSZ6legd.webp)

# Header
O Header é um objeto JSON que consiste, geralmente, do tipo (chamado de typ) que é `JWT` e o algoritmo utilizado para encriptar o mesmo (chamado de alg).

O Header só contém essas duas informações:

```
{
    "typ": "JWT",
    "alg": "HS256"
}
```

# Payload
O payload é aonde vamos colocar nossa informação, isto é chamado de public claims. Alguns atributos são definidos diretamente na RFC e são obrigatórios, por isso são chamados de reserved claims. Ou seja, tudo que é nosso é um public claim, tudo que não é nosso e é obrigatório é um reserved claim.

Os reserved claims existem somente para criar um padrão. Uma vez que os Tokens JWT foram feitos para serem utilizados em várias aplicações de forma genérica, fez-se necessário uma definição base que todas as APIs utilizando o JWT deveriam seguir:

```
{
    "iss": "http://myapi.com", // Reservado pela RFC
    "user": "khaosdoctor" // Isto é um public claim
}
```

O atributo `iss` é uma abreviação para `issuer`, que é a definição ou o nome da API que gerou este JWT. Isto é obrigatório e serve como identificação de onde o token veio. É também possível implementar um nível maior de segurança nos tokens colocando uma chave criptografada que pode (ou não) ser lida pelo servidor como uma forma de autenticação adicional.

Em conjunto com o `iss` também temos outros atributos tidos como reserved claims, estes são:

- `aud` (Audience): é comumente usado para definir quem poderá utilizar estes tokens, em conjunto com o iss é possível restringir ou permitir acessos a determinados grupos (chamados de audiência) se eles estiverem no `aud `correto.
- `exp` (Expiration): é o atributo mais utilizado, porque permite especificar uma data de expiração para os tokens. Por mais seguros que os JWT sejam, se um token completo cair nas mãos erradas (geralmente por descuido de segurança do programador), o atacante poderá fazer requisições se passando por usuário, então é importante definir uma data de expiração que será checada sempre que uma requisição for feita (a maioria das bibliotecas tem suporte para isso)
- `sub` (Subject): é geralmente utilizado para informar o id ou login do usuário em um campo próprio.

O atributo `user` foi definido pelo desenvolvedor, ou seja, ele é um public claim, pois não faz parte da obrigatoriedade do padrão. Utilizamos `user` porque, geralmente, os tokens JWT são utilizados para realizar logins em plataformas, desta forma podemos obter toda a informação do usuário logado de uma só vez sem precisar ficar consultando o banco de dados para pegar pedaços de dados que precisamos.

# Assinatura
A assinatura é o header e o payload encriptados com um secret. Isto existe basicamente para podermos evitar ataques do tipo man in the middle, aonde o invasor captura a requisição do usuário e a modifica, enviando para o servidor a sua própria requisição modificada personificando o usuário.

O hash de criptografia da assinatura do JWT é reversível somente por uma chave chamada de `secret`, portanto a menos que o usuário tenha o `secret` ela se torna irreversível, de forma que uma vez criptografado ele não poderá mais ser aberto. Assim prevenimos que o atacante altere qualquer conteúdo do payload, pois, ao ser alterado, o hash final não irá ser o mesmo do hash inicial, causando um conflito e transformando o token em inválido. Garantindo a identidade do cliente e a integridade das informações.

Basicamente o algoritmo de encriptação busca o header em base64, concatenado com um ponto simples `(.)` e a base64 do payload juntamente com o `secret`, que é a chave de decriptação, desta forma:

```
HMACSHA256(
    base64UrlEncode(header) + "." + base64UrlEncode(payload),
    secret
)
```
O `secret` deve estar na posse da aplicação que está recebendo a requisição (o servidor), pois se o secret estiver do lado do cliente, então seria possível que qualquer pessoa pegasse esse `secret` e não só revelasse o token, mas também gerar novos tokens.

O Token
Um token finalizado consiste em `base64(header).base64(payload).assinatura` mais ou menos como abaixo:

[](https://miro.medium.com/max/720/0*Ottpezt2NVZpV6Sb.webp)

Que deve ser enviado no cabeçalho `Authorization` com o prefixo `Bearer`:


```
Authorization: Bearer <token>
```
# Vantagens
- Compacto, muito mais compacto do que o XML, de forma que poupamos muitos bytes facilitando o uso em conexões lentas
- Fácil de assinar
- Fácil de parsear, muitas linguagens tem um parser JSON já out of the box, o que torna muito mais acessível o uso desta tecnologia.

Veja uma comparação do JWT com o SAML (Security Assertion Markup Language):

[](https://miro.medium.com/max/720/0*n2X2NZu9zk_UgKRF.webp)

Este artigo explica o JWT no próximo será explicado como é feito a implementação !
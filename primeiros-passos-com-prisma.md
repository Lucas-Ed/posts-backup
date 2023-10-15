# Como Usar?
Primeiro temos que instalar a CLI global do Prisma:
`yarn global add prisma`
Neste exemplo vamos usar o Prisma Cloud, se você quiser executar localmente vai ser necessário o Docker na sua maquina, voce pode baixa-lo [aqui.](https://www.docker.com/get-started/)
Para usar o Prisma Cloud é necessário se registrar [aqui](https://app.prisma.io) e depois efetuar o login pela CLI:
`$ prisma login` 
Agora que temos tudo que precisamos para usar o Prisma podemos criar uma pasta para o exemplo e inicializar o projeto pela CLI:

```
$ mkdir prisma-example
$ cd ./prisma-example
$ prisma init
```
Você vai ver algo parecido com a imagem abaixo, usando as setas do teclado selecione a opção Demo server.

![](https://miro.medium.com/max/720/1*A2GS3FsNK2-RXqTEq-RmYg.webp)

Depois você seleciona qual região do servidor, o nome do serviço e o stage (dev). O ultimo passo é selecionar qual o tipo de código deve ser gerado, para esse exemplo vou selecionar TypeScript.

Após este passos o Prisma vai gerar e publicar um serviço, disponibilizar um endpoint para acesso, gerar o código do prisma-client, criar um arquivo onde vai ser feita a [modelagem de dados](https://www.prisma.io/docs/datamodel-and-migrations/datamodel-MYSQL-knul) e o [arquivo yml de configuração.](https://www.prisma.io/docs/prisma-cli-and-configuration/prisma-yml-5cy7)
O Prisma tem outro projeto chamado [graphql-yoga](https://github.com/dotansimha/graphql-yoga) que expõe de forma simples uma API GraphQL usando como base o [apollo-server](https://github.com/apollographql/apollo-server).

# Conclusão
- Prisma é uma nova forma de acesso a dados, que resolve muitos problemas dos ORMs tradicionais e traz um poder enorme para o desenvolvimento de software. Alguns pontos chaves sobre o Prisma:
- Tipagem de dados segura
- Camada de acesso a dados
- Agnóstico a banco de dados
- Gerador de código automático
- Gerenciador de estrutura de dados(migrations)
- Query Engine de alta performance
- Suporte a base dados relacionais e não relacionais
- Suporte a transações
- Suporte a query nativas
- Não serve somente para GraphQL
- Pode ser usado como microservice
- Roda em um container Docker
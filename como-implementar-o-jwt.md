# Implementação
Para implementar um login via JWT vamos utilizar um exemplo de um API que busca uma database.

Temos uma rota `POST /login` que recebe um usuário e senha via formulário HTML simples e autentica este usuário utilizando o framework Express.js como base.

Primeiramente temos o nosso servidor base como qualquer outra aplicação Javascript utilizando express:

```
const mongoose = require('mongoose')
const express = require('express')
const bodyParser = require('body-parser')
const expressJWT = require('express-jwt')
const jwt = require('jsonwebtoken')
const apiRoutes = require('./routers/api')
const app = express()

app.use(bodyParser.urlencoded())
app.use(expressJWT({ secret: 'string de secret' })) // Utilizamos nosso middleware JWT

const User = require('./models/user') // Modelo do mongoose

// Nossa Rota
app.post('/login', (req, res) => {
  if (!req.body.username) {
    res.status(400).send('Username required')
    return
  } else if (!req.body.password) {
    res.status(400).send('Password Required')
    return
  }
  
  User.findOne({ username: req.body.username}, (err, user) => {
      user.comparePassword(req.body.password, (err, isMatch) => {
          if (err) throw err
          if (!isMatch) res.status(401).send('Invalid Password')
          res.status(200).json({})
      })
  })
})

const secrets = require('./secrets')
app.use('/api', apiRoutes)
```
Geralmente temos nosso secret em um arquivo do servidor ou (ainda melhor) em uma variável de ambiente, neste caso estamos apenas usando a string aqui por motivos didáticos.

Perceba que não estamos fazendo nada no momento, ele apenas busca um usuário e verifica se as senhas são iguais, se forem retornamos um 200 se não um 401. Vamos implementar um JWT aqui.

Primeiramente, vamos fazer uma alteração para que possamos acessar nossa rota de login sem precisar de um token, afinal não faz sentido o usuário ter um token para pedir um token, portanto vamos mudar esta linha:

```
app.use(expressJWT({ secret: 'string de secret' }))
```
Para:

```
app.use(
  expressJWT({ secret: 'string de secret' })
    .unless({ path: ['/login']})
)
```

Ficando assim:


```
const mongoose = require('mongoose')
const express = require('express')
const bodyParser = require('body-parser')
const expressJWT = require('express-jwt')
const jwt = require('jsonwebtoken')
const apiRoutes = require('./routers/api')
const app = express()

app.use(bodyParser.urlencoded())
app.use(expressJWT({ secret: 'string de secret' }).unless({ path: ['/login']}))

const User = require('./models/user') // Modelo do mongoose

// Nossa Rota
app.post('/login', (req, res) => {
  if (!req.body.username) {
    res.status(400).send('Username required')
    return
  } else if (!req.body.password) {
    res.status(400).send('Password Required')
    return
  }
  
  User.findOne({ username: req.body.username}, (err, user) => {
      user.comparePassword(req.body.password, (err, isMatch) => {
          if (err) throw err
          if (!isMatch) res.status(401).send('Invalid Password')
          res.status(200).json({})
      })
  })
})

const secrets = require('./secrets')
app.use('/api', apiRoutes)
// Restante do código
```

Desta forma estamos falando que não vamos precisar de um token para poder acessar nossa rota de login.

Se você fazer um teste, vai poder verificar que as demais rotas agora pedem um token de autenticação com uma mensagem de erro na resposta.

O próximo passo é retornar um token JWT ao invés do nosso JSON vazio. Para isso vamos precisar criar um token utilizando o módulo JWT que importamos anteriormente. Vamos na linha aonde retornamos nossa resposta vazia:

```
res.status(200).json({})
```

E vamos criar nosso token desta forma:


```
let meuToken = jwt.sign({ username: req.body.username }, 'string de secret')
res.status(200).json(meuToken)
```

Importante: Note que a string do `secret` deve ser a mesma que passamos para o nosso middleware lá em cima.

Veja que, no primeiro parâmetro do método `sign`, estamos passando o payload que queremos enviar. Isto pode ser literalmente qualquer coisa, porque é o nosso payload e as nossas informações, isso é interessante porque podemos adicionar qualquer tipo de informação para ser trafegada.

Agora teremos na resposta uma string grande que é nosso token JWT, você pode verificar se ele é válido no site http://jwt.io colocando sua assinatura e seu secret nos formulários.

[](https://miro.medium.com/max/720/0*rOZyw9DUCWwOxxzi.webp)

O código final fica assim:


```
const mongoose = require('mongoose')
const express = require('express')
const bodyParser = require('body-parser')
const expressJWT = require('express-jwt')
const jwt = require('jsonwebtoken')
const apiRoutes = require('./routers/api')
const app = express()

app.use(bodyParser.urlencoded())
app.use(
  expressJWT({ secret: 'string de secret' })
       .unless({ path: ['/login']})
)

const User = require('./models/user')

app.post('/login', (req, res) => {
  if (!req.body.username) {
    res.status(400).send('Username required')
    return
  } else if (!req.body.password) {
    res.status(400).send('Password Required')
    return
  }
  User.findOne({ username: req.body.username}, (err, user) => {
      user.comparePassword(req.body.password, (err, isMatch) => {
          if (err) throw err
          if (!isMatch) res.status(401).send('Invalid Password')

          const meuToken = jwt.sign({ username: req.body.username }, 'string de secret')
          res.status(200).json(meuToken)
      })
  })
})

const secrets = require('./secrets')
app.use('/api', apiRoutes)
```
Então podemos pegar nosso token recebido e fazer todas as requisições subsequentes utilizando o cabeçalho `Authorization: Bearer <token>`.

# Conclusão
Com isto podemos utilizar facilmente qualquer módulo JWT e entender um pouco mais como ele funciona. Se você estiver interessado em aprender um pouco mais ou se aprofundar no conteúdo, veja o site oficial https://jwt.io e também o guia e livro de introdução em https://jwt.io/introduction/.
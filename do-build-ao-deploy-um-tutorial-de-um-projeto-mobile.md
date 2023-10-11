Pessoal recetemente participei do evento NLW-11 Setup-(Trilha-Ignite) que é promovido pela [Rocketseat](https://lp.rocketseat.com.br/nlw),  no evento o desafio, foi o desenvolvimento de aplicação web, aplicação backend e o aplicativo mobile.

Como no evento não foi passado este conteúdo, resolvi, fazer este artigo para ajudar a comunidade de Dev's, vamos ao passo a passo de como fazer o build e deploy, do aplicativo construído no evento.
O projeto que faremos a etapa do build e deploy é esse [aqui.](https://github.com/Lucas-Ed/Nlw-11-Setup)

![](https://hidev.cc/wp-content/uploads/2021/11/react-native-expo-e1636065072541.png)

**1°-PASSO**

Instalar o cli expo

```bash
npm install -g eas-cli
```

**2°-PASSO**
É preciso ter se cadastrado na expo para ter acesso, caso você não tenhe cadastro faça seu cadastro [aqui](https://expo.dev/signup), ou se já tiver, faça login [aqui](https://expo.dev/login)

Fazer login na sua conta expo pelo cli:

```bash
eas login
```

Você deverá ver no seu terminal:

![](https://i.postimg.cc/KcM61bj6/eas-login.png)

se aparecer logged in é porque deu certo e você conseguiu logar.

**3°-PASSO**

Gere o arquivo eas.json:

```bash
eas build:configure
```
Você deverá ver no terminal:

![](https://i.postimg.cc/wTwpXQXL/3-config.png)
 
**4°-PASSO**
Rode o comando para fazer o build:

 ```bash
eas build
```

Você deverá ver no terminal:

![](https://i.postimg.cc/KcNSbDsw/4-build.png)

Selecione ios ou android.

Após finalizado ele fará o upload do arquivo gerado para sua conta expo, e gerará o endereço pra você fazer download do seu arquivo.

Outra maneira de fazer download do arquivo é dentro de sua conta expo você acessa o endereço: https://expo.dev/accounts/suaconta, e depois acesse: https://expo.dev/accounts/seu-username-login/projects/mobile/builds/seu-build ,você deverá ver:

![](https://i.postimg.cc/d09zJpPZ/down-build.png)

Aí só fazer o download.

**5°-PASSO**
Se preferir após a compilação (build), estiver concluída, execute `eas submit` para carregar o aplicativo nas lojas de aplicativos.

Veja como é no terminal:

![](https://i.postimg.cc/sxC0FCwh/sub-1.png)

Selecione o arquivo de build que foi feito o upload na sua conta expo:

![](https://i.postimg.cc/sgWmrNGP/select-archive.png)

Escolha o arquivo na sua conta expo:

![](https://i.postimg.cc/vZGrJZMy/select-2.png)

Você precisará de sua chave JSON da conta de serviço do Google, que é necessário para carregar seu aplicativo na Google Play Store, não vou fazer aqui está etapa mas isso é tudo o que é necessário pra você saber, está etapa da chave JSON, você consegue fazer sozinho, chegamos ao fim.
[Tutorial para gerar sua chave na goole service.](https://github.com/expo/fyi/blob/main/creating-google-service-account.md)


**Referência**
[Documentação-1 expo.](https://docs.expo.dev/build/setup/)
[Documentação-2 expo.](https://docs.expo.dev/eas-update/deployment-patterns/)
[Sobre Mim](bit.ly/3o0CAdw)
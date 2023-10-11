![](https://miro.medium.com/v2/resize:fit:954/1*Q3tWc2vG2cNbMpviHiL2oA.png)

O Docker é uma plataforma de virtualização que permite executar aplicações em containers isolados. Isso torna possível executar aplicações Django em diferentes ambientes, como máquinas virtuais, servidores físicos e até mesmo na nuvem.

Neste tutorial, vamos aprender como colocar o sistema Django em container Docker no Windows 10. Vamos usar a versão 4.2.5 do Django.

**Pré-requisitos**

Para seguir este tutorial, você precisará dos seguintes pré-requisitos:

Um computador com o sistema operacional Windows 10 instalado.
O [Docker desktop](https://www.docker.com/products/docker-desktop/) instalado.
Um editor de texto, eu indico o VsCode.

**Instalando o Docker no Windows 10**

Para instalar o Docker no Windows 10, siga estas etapas:

- [Baixe](https://www.docker.com/products/docker-desktop/) o instalador do Docker do site oficial.

- Execute o instalador.


**Criando um projeto Django**

Primeiro, você deve criar um projeto Django. Eu usarei um projeto que fiz. Para isso, execute o seguinte comando no Prompt de Comando:

```
django-admin startproject myproject
```
Você deve substituir myproject pelo nome do seu projeto.

Este comando criará um novo diretório chamado myproject com os seguintes arquivos:

- `myproject/settings.py`: Configurações do Django.
- `myproject/urls.py`: URLs do Django.
- `myproject/wsgi.py`: WSGI do Django.

**Criando um arquivo Dockerfile**

Em seguida, vamos criar um arquivo Dockerfile, no diretório raiz, que será usado para criar o container Docker do nosso projeto Django. O arquivo Dockerfile contém instruções para o Docker sobre como construir o container.

Abra o arquivo `myproject/Dockerfile` em um editor de texto e adicione as seguintes linhas:


```
FROM python:3.11

COPY . /app

WORKDIR /app

RUN pip install -r requirements.txt

EXPOSE 8000

CMD python manage.py runserver 0.0.0.0:8000
```
**Estas linhas fazem o seguinte:**

- Usam a imagem `python:3.11` como base para o container.
- Instalam o pip no container.
- Copiam os arquivos do projeto para o container.
- Definem o diretório de trabalho do container como o diretório do projeto.
- Instalam as dependências do projeto usando o pip3.
- Expoem a porta 8000 do container.
- Iniciam o servidor web do Django na porta 8000.

**Construindo o container Docker**

Agora, vamos construir o container Docker usando o arquivo Dockerfile que criamos. Para isso, primeiro abra o Docker desktop, conecte em sua conta, após isso execute o seguinte comando no terminal:

```
docker build -t myproject .
```
Substitua myproject, pelo nome do seu projeto.

Rodado o comando anterior você vera no terminal algo como:

![](https://i.postimg.cc/TP7D1JVh/build-dck.png)

Este comando irá construir o container Docker com o nome do seu projeto.

**Executando o container Docker**

Para executar o container Docker, execute o seguinte comando no Prompt de Comando:

```
docker run -d -p 8000:8000 myproject
```
Este comando irá executar o container Docker na porta 8000.

você vera no seu terminal algo como:

![](https://i.postimg.cc/K8N2n9sc/run.png)

Agora rode o comando para ver se o container esta ativo:

```
docker ps
```

Você verá no terminal algo como:

![](https://i.postimg.cc/hjC8TqV8/ps.png)

Abra o Docker desktop para checar também a imagem do rojeto criada e se esta em execução como mostrou pelo terminal, você deve ver o Docker desktop, desta maneira:

![](https://i.postimg.cc/rs1WV0qp/desktop-dck.png)

como no meu caso o projeto criado tem o nome de pythonando-8.0, eu vejo assim, você verá com o nome do seu projeto.

**Testando o aplicativo Django**

Agora, podemos acessar o aplicativo Django em um navegador. Abra um navegador e acesse o seguinte URL:


```
# No meu caso a url é assim:

http://localhost:8000/usuarios/login/
```

Você deverá ver a página inicial do aplicativo Django.

![](https://i.postimg.cc/L6fT05fh/login.png)

**Conclusão**

Neste tutorial, aprendemos como colocar o sistema Django em container Docker no Windows 10. Agora, você pode executar o seu aplicativo Django em diferentes ambientes, de forma rápida e fácil.

Agora veja o projeto que Dockerizei [aqui.](https://github.com/Lucas-Ed/pythonando-8.0)

**Dicas adicionais**

Para acessar o container Docker, você pode usar o comando `docker exec -it my`
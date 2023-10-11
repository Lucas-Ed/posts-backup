Acredito que todo mundo que necessite usar outras versões do Python na mesma máquina, sofre com instalações de máquinas virtuais, seja virtualenv, anaconda ou outras, este breve tutorial te ensinará como usar o docker para rodar um projeto de uma api [FastApi](https://fastapi.tiangolo.com) em python.

## Necessidade
Estava eu trabalhando numa api, FastApi em Python porém a FastApi requer Python > que 3.7 e minha máquina tem o Python na versão 3.6.8 instalado, dai surgiu a necessidade de rodar em docker, confesso que antes tentei outras maneiras de rodar o 2 versões do Python na mesma máquina com o virtualenv, porém tive mt dor de cabeça e não deu certo ! 

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/2560px-Docker_%28container_engine%29_logo.svg.png)

## Tutorial
Primeiro, é necessário ter o Docker instalado na sua máquina. Se você ainda não o tem, pode baixá-lo no [site oficial do Docker.](https://www.docker.com/products/docker-desktop/)
Depois de instalar o Docker você precisará ter instalado a [imagem do Python para usar no docker](https://hub.docker.com/_/python),você pode instala-la com o comando:

```
docker pull python
```
No diretório raiz, crie um arquivo: `requirements.txt` para colocar as blibliotecas necessárias, a serem instaladas, escreva assim o arquivo:

```
fastapi>=0.89.0,<0.89.2
pydantic>=1.8.0,<2.0.0
uvicorn>=0.20.0,<0.20.1
yfinance>=0.2.3,<0.2.4
```
Após isso, você precisará criar um arquivo chamado "Dockerfile" na pasta do seu projeto. Este arquivo irá conter as instruções para o Docker criar a imagem da sua aplicação.

No arquivo Dockerfile, adicione a seguinte linha para especificar a versão do Python que você deseja usar:

```
FROM python:3.11.1

```
Em seguida, adicione as seguintes linhas para instalar as dependências do seu projeto e configurar o diretório de trabalho:


```
COPY ./requirements.txt . 
RUN pip install --upgrade pip --no-cache-dir -r  requirements.txt
COPY . /app
WORKDIR /app

EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

```

Agora você pode adicionar o restante do código do seu projeto (incluindo o arquivo main.py do FastAPI) para o diretório /app do container do Docker.

Por fim, adicione a seguinte linha no arquivo Dockerfile para especificar o comando para iniciar sua aplicação:


```
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

```
Agora você pode construir a imagem do seu projeto usando o seguinte comando:


```
docker build -t my-fastapi-app .

```

Em seguida, você pode iniciar um container a partir da imagem construída com o seguinte comando:


```
docker run -p 8000:8000 my-fastapi-app

```

E pronto, sua aplicação estará rodando em uma versão específica do Python usando o Docker! Você pode acessá-la digitando o endereço `http://localhost:8000` em seu navegador.

**Nota:** Isso é apenas um exemplo básico e é provável que seu projeto tenha mais dependências e configurações específicas. Tenha cuidado para adicionar esses detalhes adequadamente ao seu arquivo Dockerfile e comandos do Docker
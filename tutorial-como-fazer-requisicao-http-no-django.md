![](https://dkrn4sk0rn31v.cloudfront.net/uploads/2020/11/consumindo-api-python.png)

No Django, é possível fazer requisições HTTP para outros serviços ou APIs usando a biblioteca requests. Este tutorial irá mostrar como fazer isso usando a versão 4.2.6 do Django.

**Requisitos**

Para seguir este tutorial, você precisará do seguinte:

- Uma instalação do Python 3
- Uma instalação do Django 4.2.6
- Uma instalação da biblioteca requests

- **Criar ambiente virtual**

```
python -m venv venv
```

- **Ativar ambiente virtual do python**
```
source venv/Scripts/Activate
```

**Instalando a biblioteca requests**

Para instalar a biblioteca `requests`, abra um terminal e execute o seguinte comando:

```
pip install requests
```
**Criando um projeto Django**

Para criar um projeto Django, abra um terminal e execute o seguinte comando:

```
django-admin startproject myproject
```
Este comando criará um diretório chamado myproject com os arquivos do django.

**Configurando o projeto Django**

Abra o arquivo `myproject/settings.py` e adicione as seguintes linhas à seção INSTALLED_APPS:


```
INSTALLED_APPS = [
    ...
    'requests',
]
```
Isso adicionará a biblioteca requests ao projeto Django.

**Criando uma view para fazer a requisição HTTP**

Abra o arquivo `myproject/urls.py` e adicione a seguinte rota à seção urlpatterns:

```
from django.urls import path

from myproject.views import make_http_request

urlpatterns = [
    path('', make_http_request),
]
```

Esta rota irá chamar a view `make_http_request()` quando um usuário acessar a URL /.

**Criando a view `make_http_request()`**

Abra o arquivo `myproject/views.py` e adicione a seguinte view:


```
from requests import get

def make_http_request(request):
    """
    Faz uma requisição HTTP para a URL especificada.

    Args:
        request: A requisição do usuário.

    Returns:
        A resposta da requisição.
    """

    url = request.GET.get('url', 'https://www.google.com')
    response = get(url)
    return response
```

Esta view usa a biblioteca requests para fazer uma requisição HTTP para a URL especificada pelo usuário.

**Testando a requisição HTTP**

Para testar a requisição HTTP, inicie o servidor Django executando o seguinte comando no terminal:

```
python manage.py runserver
```
Em seguida, abra um navegador e acesse a URL `http://localhost:8000/?url=https://www.google.com`.

Se tudo estiver correto, o navegador exibirá a página inicial do Google.

**Exemplo**

O seguinte exemplo mostra como usar a view `make_http_request()` para fazer uma requisição HTTP para a API do GitHub:


```
from requests import get

def make_http_request(request):
    """
    Faz uma requisição HTTP para a API do GitHub.

    Args:
        request: A requisição do usuário.

    Returns:
        A resposta da requisição.
    """

    url = request.GET.get('url', 'https://api.github.com/users/bard')
    response = get(url)
    return response
```

Para testar esta requisição, abra um navegador e acesse a URL `http://localhost:8000/?url=https://api.github.com/users/bard`.

Se tudo estiver correto, o navegador exibirá a seguinte resposta JSON:

```
{
    "login": "bard",
    "id": 1234567890,
    "avatar_url": "https://avatars.githubusercontent.com/u/1234567890?v=4"
}
```


**Conclusão**

Este tutorial mostrou como fazer requisições HTTP no Django usando a biblioteca `requests`.
Espero que este tutorial seja útil para você!

[Sobre Mim.](https://bit.ly/3o0CAdw)
![](https://saif.tn/media/posts/post-your_first_steps_with_django_create_django_project.png)

Django é um framework web de código aberto escrito em Python. É uma das plataformas de desenvolvimento web mais populares do mundo, sendo usado por empresas como Instagram, Spotify e Disqus.

As diretivas do Django são instruções que podem ser usadas para controlar o comportamento do framework. Elas são uma parte essencial do Django e podem ser usadas para melhorar a segurança, o desempenho e a escalabilidade de seus aplicativos.

**1. URLS**

A diretiva URLS é usada para definir as URLs do seu aplicativo. As URLs são as rotas que os usuários usam para acessar seu aplicativo.

O primeiro passo é no core do projeto criar a url que inclui o aplicativo, exemplo:

```
urlpatterns = [
    path('admin/', admin.site.urls),
    path('usuarios/', include('usuarios.urls')),
]
```

Para usar a diretiva URLS, você precisa definir o arquivo `urls.py` em seu aplicativo. Este arquivo contém uma lista de URLs que seu aplicativo suporta.

Por exemplo, o seguinte código define uma URL que leva à página `/home`:

```
from django.urls import path

urlpatterns = [
    path("home", HomeView.as_view(), name="home"),
    path('login/', views.logar, name="login"),
]
```

Então para acessar a home do projeto a url ficará assim `usuarios/login/`.

**2. Acessando as url's no html.**

A diretiva `{% url " " %}` é usada para gerar URLs em seus templates do Django.

Para usar esta diretiva, você primeiro precisa definir as URLs do seu aplicativo em seu arquivo `urls.py` Por exemplo, o seguinte código define uma URL que leva à página `/home`:

```
from django.urls import path

urlpatterns = [
    path("home", HomeView.as_view(), name="home"),
]
```

Em seguida, você pode usar a diretiva `{% url " " %}` em seus templates para gerar URLs para essas rotas. Por exemplo, o seguinte código renderizará um link para a página `/home`:

```
<a href="{% url "home" %}">Home</a>
```

Este código renderizará o seguinte link:

```
<a href="/home">Home</a>
```

Você também pode usar a diretiva `{% url " " %}` para gerar URLs com parâmetros. Por exemplo, o seguinte código renderizará um link para a página `/product/123`:

```
<a href="{% url "product" pk=123 %}">Produto 123</a>
```
Este código renderizará o seguinte link:

```
<a href="/product/123">Produto 123</a>
```

Aqui está um exemplo completo de como usar a diretiva `{% url " " %}` em um template do Django:

```
from django.urls import path

urlpatterns = [
    path("home", HomeView.as_view(), name="home"),
    path("product/<int:pk>", ProductView.as_view(), name="product"),
]
```

**- HTML.**


```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Home</title>
</head>
<body>
    <a href="{% url "home" %}">Home</a>
    <a href="{% url "product" pk=123 %}">Produto 123</a>
</body>
</html>
```
Este exemplo renderizará uma página HTML com dois links: um para a página `/home` e outro para a página `/product/123`.

**3. Views (acessar os dados do banco)**

Para acessar os dados do banco no HTML no Django, você precisa primeiro definir uma coleção de dados em seu código Python. Por exemplo, o seguinte código define uma lista de pedidos:

Para usar esta diretiva, você primeiro precisa definir uma coleção de dados em seu código Python. Por exemplo, o seguinte código define uma lista de pedidos:


```
from django.db import models

class Pedido(models.Model):
    id = models.AutoField(primary_key=True)
    nome_cliente = models.CharField(max_length=255)
    produto = models.CharField(max_length=255)
    quantidade = models.IntegerField()

pedidos = Pedido.objects.all()
```

Em seguida, você pode passar essa coleção de dados para seu template usando o contexto. Por exemplo, o seguinte código define uma view que retorna uma lista de pedidos:


```
from django.shortcuts import render

def pedidos(request):
    pedidos = Pedido.objects.all()
    context = {
        "pedidos": pedidos,
    }
    return render(request, "pedidos.html", context)
```

Finalmente, você pode acessar os dados da coleção de pedidos em seu template usando a diretiva `{% for pedido in pedidos %}`. Por exemplo, o seguinte código renderizará uma lista de todos os pedidos:


```
{% for pedido in pedidos %}
    <li>{{ pedido.nome_cliente }}</li>
{% endfor %}
```

Este código renderizará uma lista de itens com o seguinte conteúdo de exemplo:


```
[
    "João",
    "Maria",
    "Pedro"
]
```

Você também pode usar a diretiva `{% for pedido in pedidos %}` para acessar os dados de cada pedido. Por exemplo, o seguinte código renderizará uma lista de todos os pedidos, juntamente com o produto e a quantidade encomendada:

```
{% for pedido in pedidos %}
    <li>{{ pedido.nome_cliente }} comprou {{ pedido.produto }} em quantidade de {{ pedido.quantidade }}</li>
{% endfor %}
```

Este código renderizará uma lista de itens com o seguinte conteúdo:

```
[
    "João comprou Camisa em quantidade de 1",
    "Maria comprou Calça em quantidade de 2",
    "Pedro comprou Sapato em quantidade de 3"
]
```
**4. STATICFILES**

A diretiva **STATICFILES** é usada para definir os arquivos estáticos do seu aplicativo. Os arquivos estáticos são arquivos que não são alterados com frequência, como imagens, CSS e JavaScript.

Para usar a diretiva **STATICFILES**, você precisa definir o diretório `STATIC_ROOT` em seu arquivo `settings.py`:


```
STATIC_URL = '/static/'
STATICFILES_DIRS = (os.path.join(BASE_DIR, 'templates/static'),)
STATIC_ROOT = os.path.join('static')
```

Este diretório é o local onde o Django armazenará todos os seus arquivos estáticos.

Em seguida, você pode usar a diretiva `{% static %}` em seus templates para referenciar arquivos estáticos. Por exemplo, o seguinte código renderizará a imagem `image.jpg`:

```
{% load static %}

{% block 'head' %}

    <link href="{% static 'geral/css/style.css' %}" rel="stylesheet">

{% endblock 'head' %}

<img src="{% static "image.jpg" %}" />
```

A diretiva `{% static %}` também pode ser usada para referenciar arquivos CSS. Por exemplo, o seguinte código renderizará o arquivo CSS styles.css:


```
<link rel="stylesheet" href="{% static "styles.css" %}">

Este código renderizará o seguinte link:

<link rel="stylesheet" href="/static/styles.css">
```

Aqui está um exemplo completo de como usar a diretiva `{% static %}` para referenciar arquivos CSS:

Em `views.py`:


```
from django.contrib.staticfiles.storage import FileSystemStorage

# Define o diretório de armazenamento de arquivos estáticos
STATICFILES_STORAGE = FileSystemStorage(location="static")

# Crie um arquivo CSS
with open("static/styles.css", "w") as f:
    f.write("body { background-color: red; }")

# Renderize a página HTML
def index(request):
    return render(request, "index.html")
```

**- No html**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Index</title>

    <link rel="stylesheet" href="{% static "styles.css" %}">
</head>
<body>
    <h1>Index</h1>
</body>
</html>
```
**5. MEDIA**

A diretiva `{% MEDIA_ROOT %}` é usada para referenciar o diretório de mídia do seu aplicativo Django.

O diretório de mídia é o local onde você armazena arquivos de mídia, como imagens, vídeos e arquivos PDF.

Para usar esta diretiva, você primeiro precisa definir o diretório de mídia do seu aplicativo em seu arquivo `settings.py`. Por exemplo, o seguinte código define o diretório de mídia para media:


```
# settings.py

MEDIA_ROOT = os.path.join(BASE_DIR, "media")
```

Em seguida, você pode usar a diretiva `{% MEDIA_ROOT %}` em seus templates para referenciar o diretório de mídia. Por exemplo, o seguinte código renderizará uma imagem localizada no diretório de mídia:


```
<img src="{% MEDIA_ROOT %}/image.jpg" />
```

Este código renderizará o seguinte link:

```
<img src="/media/image.jpg" />
```

Você também pode usar a diretiva `{% MEDIA_ROOT %}` para referenciar arquivos de mídia em seus templates. Por exemplo, o seguinte código renderizará um arquivo PDF localizado no diretório de mídia:

```
<a href="{% MEDIA_ROOT %}/file.pdf">Download</a>
```
Este código renderizará o seguinte link:

```
<a href="/media/file.pdf">Download</a>
```

Aqui está um exemplo completo de como usar a diretiva `{% MEDIA_ROOT %}` em um template do Django:


```
# settings.py

MEDIA_ROOT = os.path.join(BASE_DIR, "media")

# templates/index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Index</title>
</head>
<body>
    <img src="{% MEDIA_ROOT %}/image.jpg" />
    <a href="{% MEDIA_ROOT %}/file.pdf">Download</a>
</body>
</html>

```

Este exemplo renderizará uma página HTML com uma imagem e um link para um arquivo PDF.

**- Upload de arquivos**

Em seguida, você precisa criar um formulário que permita ao usuário enviar um arquivo. Por exemplo, o seguinte código cria um formulário que permite ao usuário enviar uma imagem:


```
# forms.py
from django import forms

class UploadImageForm(forms.Form):
    image = forms.ImageField(required=True)
```

Em seguida, na `view.py` precisa que aceite o formulário e armazene o arquivo enviado no diretório de mídia. Por exemplo, o seguinte código cria uma view que aceita o formulário e armazena o arquivo enviado no diretório de mídia:

```
from django.shortcuts import render, redirect
from django.core.files.storage import FileSystemStorage

def upload_image(request):
    if request.method == "POST":
        form = UploadImageForm(request.POST, request.FILES)
        if form.is_valid():
            image = form.cleaned_data["image"]
            file_name = image.name
            storage = FileSystemStorage(location=MEDIA_ROOT)
            file_saved = storage.save(file_name, image)
            return redirect("image_uploaded")
    else:
        form = UploadImageForm()
    return render(request, "upload_image.html", {"form": form})
```

Finalmente, você precisa criar um template que renderize a página de upload de arquivos. Por exemplo, o seguinte código cria um template que renderiza a página de upload de arquivos:


```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Upload Image</title>
</head>
<body>
    {% if form.errors %}
        <div class="alert alert-danger">
            {% for error in form.errors %}
                {{ error }}
            {% endfor %}
        </div>
    {% endif %}
    <form action="" method="post" enctype="multipart/form-data">
        {{ form.as_p }}
        <input type="submit" value="Upload" />
    </form>
</body>
</html>
```

Este código renderizará uma página HTML com um formulário que permite ao usuário enviar uma imagem.

Para testar isso, você pode criar um superusuário usando o comando `python manage.py createsuperuser`. Em seguida, você pode fazer login no painel administrativo e visitar a página de upload de imagens.

Se você enviar um arquivo de imagem, ele será armazenado no diretório de mídia. Você pode então acessar o arquivo de imagem usando a diretiva `{% MEDIA_ROOT %}` em seus templates.

Aqui está um exemplo de como usar a diretiva `{% MEDIA_ROOT %}` para renderizar uma imagem enviada pelo usuário:


```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Image Uploaded</title>
</head>
<body>
    <img src="{% MEDIA_ROOT %}/{{ image.name }}" />
</body>
</html>

```
Este código renderizará uma página HTML com uma imagem enviada pelo usuário.

**6. Personalize o formulário de administração-ModelAdmin**

Para adicionar novos campos no admin do Django, você precisa criar uma classe que herda da `classe admin.ModelAdmin`. Esta classe irá definir como os modelos serão exibidos no admin.

Aqui está um exemplo de uma classe ModelAdmin que adiciona um novo campo chamado image ao modelo Book:


```
from django.contrib import admin
from .models import Book

class BookAdmin(admin.ModelAdmin):
    list_display = ("title", "author", "publication_date")
    fields = ("title", "author", "publication_date", "image")

admin.site.register(Book, BookAdmin)
```

Esta classe define dois atributos:

`list_display`: lista os campos que serão exibidos na lista de modelos no admin.
`fields`: lista os campos que serão exibidos na página de edição de modelos no admin.

No caso deste exemplo, estamos adicionando o campo image ao atributo fields. Isso fará com que o campo image seja exibido na página de edição de modelos no admin.

Você também pode usar os seguintes atributos para personalizar a exibição de campos no admin:

- `readonly_fields`: lista os campos que serão exibidos apenas como leitura no admin.
- `search_fields`: lista os campos que serão usados para pesquisar modelos no admin.
- `filter_fields`: lista os campos que serão usados para filtrar modelos no admin.
 
Para obter mais informações sobre como personalizar a exibição de campos no admin, consulte a documentação do [Django](https://docs.djangoproject.com/pt-br/4.2/).

Aqui está um exemplo completo de como adicionar um novo campo ao admin do Django:


```
from django.contrib import admin
from .models import Book

class BookAdmin(admin.ModelAdmin):
    list_display = ("title", "author", "publication_date")
    fields = ("title", "author", "publication_date", "image")
    readonly_fields = ("publication_date",)
    search_fields = ("title", "author")
    filter_fields = ("author",)

admin.site.register(Book, BookAdmin)
```
Este exemplo adiciona um novo campo chamado image ao modelo Book. O campo image é exibido como leitura na lista de modelos e na página de edição de modelos. O campo `publication_date` é exibido apenas como leitura na página de edição de modelos. O campo `title` é usado para pesquisar modelos no admin. O campo author é usado para filtrar modelos no admin.

**7. TEMPLATES**

A diretiva `TEMPLATES` é usada para definir os templates do seu aplicativo. Os templates são arquivos HTML que são usados para renderizar a saída do seu aplicativo.

Alguns recursos avançados de templates incluem:

- `{% extends %}`: Permite que você estenda um template base.
- `{% block %}`: Permite que você defina blocos de conteúdo que podem ser substituídos por templates filho.
- `{% for %}`: Permite que você itere sobre uma coleção de dados.

**8. Decorators ( @login_required e @property em Django )**

Em Django, as diretivas são um recurso que permite adicionar funcionalidades adicionais a views, templates e outros objetos. As diretivas @login_required e @property são duas das diretivas mais usadas em Django.

- **@login_required**

A diretiva `@login_required` é usada para restringir o acesso a uma view a usuários autenticados. Quando uma view é decorada com `@login_required`, o usuário é redirecionado para a página de login se não estiver autenticado.

Para usar a diretiva `@login_required`, primeiro importe-a do pacote django.contrib.auth.decorators. Em seguida, use-a para decorar a view que você deseja proteger.


```
from django.contrib.auth.decorators import login_required

@login_required
def my_view(request):
    # Só usuários autenticados podem acessar esta view

```

Por padrão, a diretiva `@login_required` redireciona o usuário para a página de login definida na configuração LOGIN_URL. Você pode alterar o URL de redirecionamento passando um argumento para a diretiva `@login_required`.


```
@login_required(login_url='/login/custom')
def my_view(request):
    # O usuário é redirecionado para '/login/custom' se não estiver autenticado
```

- **@property**

A diretiva `@property` é usada para criar um método de acesso a uma propriedade de um objeto. A diretiva `@property` é uma forma conveniente de encapsular o acesso a uma propriedade de um objeto.

Para usar a diretiva `@property`, primeiro defina um método que retorna o valor da propriedade. Em seguida, use a diretiva `@property` para decorar o método.


```
class MyModel(models.Model):
    name = models.CharField(max_length=255)

    @property
    def full_name(self):
        return f'{self.name} {self.last_name}'

my_model = MyModel.objects.get(id=1)

print(my_model.full_name)  # 'John Doe'
```

A diretiva @property também pode ser usada para definir propriedades que são calculadas no momento da consulta.


```
class MyModel(models.Model):
    name = models.CharField(max_length=255)

    @property
    def age(self):
        return date.today().year - self.birthdate.year

my_model = MyModel.objects.get(id=1)

print(my_model.age)  # 30
```

As diretivas `@login_required` e `@property` são duas das diretivas mais úteis em Django. A diretiva `@login_required` é usada para restringir o acesso a views a usuários autenticados, enquanto a diretiva `@property` é usada para criar métodos de acesso a propriedades de objetos.

**9. Exportar e Importar Dados**

- **Django Fixture**

O Django tem um recurso chamado "`fixture`". Uma fixture é uma coleção de arquivos que contêm o conteúdo serializado do banco de dados, podendo ser em formato JSON ou XML. Vamos utilizar um arquivo JSON. Ele serve para dar uma carga inicial de dados no sistema ou apenas produzir dados para testes.

**- Como Criar uma Fixtures**

Exportar Dados de um App Inteiro: Execute o comando `python manage.py dumpdata auth`. Todos os dados das tabelas do app auth serão exibidos no terminal em formato de JSON. Para uma visualização mais amigável, você pode trazer esses dados já indentados com o comando:


```
python manage.py dumpdata auth --indent 2
```

Melhor ainda, você pode exportar esses dados identados diretamente para um arquivo JSON, facilitando o deploy:


```
python manage.py dumpdata auth --indent 2 > auth.json
```
Este comando criará na raiz do seu projeto um arquivo `auth.json` com os dados de todas as tabelas do banco identados.

**- Exportar Dados de uma Tabela do Meu App**

É bem parecido com o que já mencionamos, mas aqui basta especificar o model do qual você quer exportar os dados, como por exemplo:


```
python manage.py dumpdata auth.user --indent 2 > user.json
```

O `auth.user` após o `dumpdata` indica a exportação dos dados da tabela user do app auth para o arquivo user.json. Simples, não?
Agora, para exportar dados de vários apps e colocar tudo em uma pasta chamada "`fixtures`", crie essa pasta na raiz do seu projeto e execute o seguinte comando:


```
python manage.py dumpdata auth app1 app2 --indent 2 > fixtures/fake_data.json
```

**- Como Carregar uma Fixture para o Banco?**

O Django irá procurar `fixtures` em três locais:

- No diretório fixtures de cada aplicativo instalado.
- Em qualquer diretório nomeado na opção FIXTURE_DIRS no arquivo de configuração.
- No caminho literal nomeado pela fixture.

O Django carregará qualquer `fixture` que encontrar nesses locais com o nome correspondente. Ele buscará especificamente o arquivo com o nome indicado no comando executado. Por exemplo:


```
python manage.py loaddata fake_data.json
```

**- Conclusão**

Com esses passos são uma convenção de uso das principais diretivas do django, facilitando o seu caso de uso, sobre exportar e importar Dados, você consegue exportar dados iniciais do seu ambiente de desenvolvimento ou dados para testes diretamente para o servidor de produção, agilizando seu processo de deploy e testes. Utilizar `fixtures` no Django é uma prática eficiente que economiza tempo e garante a consistência dos dados entre diferentes ambientes de desenvolvimento.

**- Referência**

[Documentação](https://docs.djangoproject.com/pt-br/4.2/)

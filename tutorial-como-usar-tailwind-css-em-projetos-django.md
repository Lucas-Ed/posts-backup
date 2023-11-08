![](https://res.cloudinary.com/practicaldev/image/fetch/s--RVW413xG--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xc5lzjitde5kywz0dgat.png)

**Requisitos**

- Python 3.7 ou superior
- Node.js 16.13 ou superior
- Django 3.2 ou superior
- Instalando os pré-requisitos

No seu terminal, execute os seguintes comandos para instalar os pré-requisitos:

```
// Cria o ambiente virual
python -m venv venv

// Ativa o ambiente virtual
source venv/bin/activate

// Instala o Django 
pip install django

// Instala o pacote do Tailwind
npm install -g tailwindcss@latest

```

Crie seu projeto Django, como queira, Configure o projeto Django para arquivos estáticos, adicione as seguintes linhas ao arquivo `settings.py` do seu projeto Django:


```
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')

```

**Inicializando Tailwind CSS**

No seu terminal, navegue até a pasta do seu projeto Django e execute o seguinte comando:

```
npx tailwind init
```

Isso irá criar um novo diretório chamado `tailwind.config.js` na raiz do seu projeto.

Crie uma pasta chamada `static` na raiz do seu projeto e dentro dela uma subpasta chamada `css`.
Crie um arquivo chamado `tailwind.css` na pasta css e adicione o código abaixo:

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
Compile o seu arquivo CSS do Tailwind usando o comando: `npx tailwindcss -i static/css/tailwind.css -o static/css/tailwind.css --watch`. Isso vai gerar um arquivo CSS com todas as classes do Tailwind e atualizá-lo sempre que você fizer alguma alteração.

**Adicionando Tailwind CSS ao projeto Django**

Abra o arquivo `base.html` do seu projeto Django e adicione as seguintes linhas ao final do arquivo:

```
<link rel="stylesheet" href="{% static 'tailwind.css' %}">
```

**Usando Tailwind CSS em seus templates**

Para usar Tailwind CSS em seus templates, você pode usar as classes CSS fornecidas pelo framework. Por exemplo, para definir a cor de fundo de um elemento para azul, você pode usar a seguinte classe:

```
<div class="bg-blue-500">
...
</div>

```

Para obter uma lista completa das classes CSS disponíveis, consulte a documentação do [Tailwind CSS.](https://tailwind.build/classes)
Após criados as url's do projeto inicie o exemplo a seguir.

**Exemplo de projeto Django com Tailwind CSS**

O seguinte exemplo mostra como usar Tailwind CSS em um projeto Django:

- `VIEW.PY`
```
from django.shortcuts import render

def home(request):
    return render(request, 'home.html')

def about(request):
    return render(request, 'about.html')


```

- HTML da home da view

```
{% extends 'base.html' %}

{% block content %}
<h1>Página inicial</h1>

<p>Esta é a página inicial do meu projeto Django com Tailwind CSS.</p>

<div class="bg-blue-500">
  <h2>Seção azul</h2>
</div>

{% endblock %}

```

- HTML de About da view


```
{% extends 'base.html' %}

{% block content %}
<h1>Sobre</h1>

<p>Esta é a página sobre do meu projeto Django com Tailwind CSS.</p>

<div class="bg-green-500">
  <h2>Seção verde</h2>
</div>

{% endblock %}

```

Para executar este exemplo, crie um diretório chamado templates na raiz do seu projeto Django e copie os arquivos home.html e about.html para esse diretório. Em seguida, execute o seguinte comando para iniciar o servidor de desenvolvimento:

```
python manage.py runserver
```
Acesse o seguinte endereço em seu navegador para ver o exemplo:

```
http://localhost:8000/
```
**[Extra]- Trabalhando com muitas classes do Tailwind CSS**
Se você tiver muitas classes no seu HTML, pode ser difícil manter as coisas organizadas. Aqui estão algumas dicas para ajudá-lo a organizar melhor suas classes:

- Diretório de classes

Utilizando o arquivo dentro de `static/css/tailwind.css.`
Aqui está um exemplo de como você pode usar essas dicas para organizar suas classes:


```
.default-box{

...

// Suas classes aqui
}

```
No atributo ClassName do html, você apenas chama a classe default-box.


**Conclusão**

Este tutorial mostrou como usar Tailwind CSS em projetos Django.
Tailwind CSS é um framework CSS poderoso que pode ajudá-lo a criar sites e aplicativos web modernos e responsivos com rapidez e facilidade.

[Link](https://kinsta.com/pt/blog/tailwind-css/)
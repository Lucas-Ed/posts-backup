![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTEDL8sYVvNPijI6_gDLpdVTroNkxD4iCWj2egYGCh0ipf-YQKj2nayhi26YMI3eTdhtAw&usqp=CAU)

No Django, as validações de formulários são usadas para garantir que os dados inseridos pelo usuário sejam válidos. Este tutorial irá mostrar como implementar validações de formulários usando a versão 4.2.6 do Django.

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

**Criando um projeto Django**

Para criar um projeto Django, abra um terminal e execute o seguinte comando:

```
django-admin startproject myproject
```
Este comando criará um diretório chamado myproject com os arquivos do django.

**Criando um formulário**

Abra o arquivo `myproject/forms.py` e adicione a seguinte classe de formulário:


```
from django.forms import ModelForm

from myproject.models import User


class UserForm(ModelForm):
    class Meta:
        model = User
        fields = ['username', 'email', 'password']
```

Esta classe de formulário é baseada na `classe ModelForm`, que fornece validações básicas para os campos de um modelo Django.

**Criando uma view para processar o formulário**

Abra o arquivo `myproject/views.py` e adicione a seguinte view:


```
from django.shortcuts import render, redirect

from myproject.forms import UserForm


def create_user(request):
    if request.method == 'POST':
        form = UserForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('index')
    else:
        form = UserForm()

    return render(request, 'create_user.html', {'form': form})
```

Esta view usa a classe de formulário `UserForm` para criar um novo usuário.

**Criando uma página de formulário**

Abra o arquivo `myproject/templates/create_user.html` e adicione o seguinte código HTML:

```
{% extends 'base.html' %}

{% block content %}
    <form action="{% url 'create_user' %}" method="POST">
        {% csrf_token %}

        <input type="text" name="username" placeholder="Nome de usuário">
        <input type="email" name="email" placeholder="Endereço de e-mail">
        <input type="password" name="password" placeholder="Senha">

        <input type="submit" value="Criar">
    </form>
{% endblock %}

```

Esta página contém um formulário que usa os campos da classe de formulário UserForm.

**Testando as validações**

Para testar as validações, inicie o servidor Django executando o seguinte comando no terminal:

```
python manage.py runserver
```

Em seguida, abra um navegador e acesse a URL `http://localhost:8000/create_user/`.

Tente enviar o formulário com dados inválidos, como um nome de usuário vazio ou uma senha com menos de 8 caracteres.

Se tudo estiver correto, o formulário não será enviado e você verá uma mensagem de erro.

**Exemplo**

O seguinte exemplo mostra como adicionar validações personalizadas a um formulário:


```
from django.forms import ModelForm, ValidationError

from myproject.models import User


class UserForm(ModelForm):
    class Meta:
        model = User
        fields = ['username', 'email', 'password']

    def clean_username(self):
        username = self.cleaned_data['username']

        if username.startswith('admin'):
            raise ValidationError(
                [_('O nome de usuário não pode começar com "admin".')]
            )

        return username
```

Esta classe de formulário adiciona uma validação personalizada que verifica se o nome de usuário não começa com a string "admin".

**Conclusão**

Este tutorial mostrou como implementar validações de formulários no Django.

[Sobre Mim.](https://bit.ly/3o0CAdw)
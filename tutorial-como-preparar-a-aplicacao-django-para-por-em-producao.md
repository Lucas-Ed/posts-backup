![](https://images.tcdn.com.br/img/img_prod/240061/django_16_1_20190227092231.png)

**O propósito deste, é compartilhar como configurar o ambiente de desenvolvimento para Produção.**

Antes de enviar sua aplicação para produção, você precisa configurar o ambiente de desenvolvimento.

Configure as variávéis no core da aplicação em `settings.py`.

Altere:

```
// De
DEBUG = True

// Para
DEBUG = False

// De
ALLOWED_HOSTS = [ ]

// Para
ALLOWED_HOSTS = ["*"]
```

- **Configure para servir os arquivos Staticos com WhiteNoise**

Primeiro, com seu virtualenv ativado, precisamos instalar o WhiteNoise utilizando o pip.

```
pip install whitenoise
```

Rode o comando para gerar novamente o arquivo requirements.txt da aplicação:

```
pip freeze > requirements.txt
```

Logo após, devemos adicionar a seguinte linha no arquivo de settings.py:


```
MIDDLEWARE = [
  'django.middleware.security.SecurityMiddleware',
  'whitenoise.middleware.WhiteNoiseMiddleware',
  # Certifique-se que o WhiteNoise seja adicionado acima de todos os middlewares do Django, exceto o de security. 
  # ...
]
```

Por fim, para ativar arquivos de cache e com campactação, adicionamos a seguinte linha (eu gosto de adicionar abaixo de STATIC_URL e STATIC_ROOT para manter um padrão):

```
STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
```

Por fim, rode o coolestatic novamente:


```
python manage.py collectstatic
```

Sua aplicação está pronta para por em produção, epois de configurar o ambiente de desenvolvimento, você pode enviar sua aplicação para produção. Isso inclui criar um servidor da web e configurar o aplicativo para ser executado nele, leve em conta também de configurar as variáveis de ambiente no ambiente de produção a qual ficará hospedada a aplicação.

È só isso, obrigado !!
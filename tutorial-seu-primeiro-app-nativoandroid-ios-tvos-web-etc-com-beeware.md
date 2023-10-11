![](https://beeware.org/contact/media//beeware-wide-2028.png)

A proposta deste framework é escreva uma vez, implante em qualquer lugar, assim como diz o próprio [site](https://beeware.org/) do mesmo.

O aplicativo para fins de estudo, é um aplicativo Hello World usando Beeware e Python

**Objetivo**

O objetivo deste tutorial é ensinar como criar um aplicativo Hello World usando Beeware e Python. Beeware é uma plataforma de desenvolvimento de aplicativos que permite que os desenvolvedores usem suas habilidades em Python para criar aplicativos para várias plataformas, neste tutorial criaremos para desktop, Android e Web.

**BeeWare o que é ?**

BeeWare é um framework de código aberto para criar aplicativos nativos, oferece. Ferramentas para ajudá-lo a escrever código Python com uma interface de usuário rica e nativa; e as bibliotecas e o código de suporte necessários para executar esse código no **iOS, Android, Windows, MacOS, Linux, Web e tvOS**, desse modo o proposito deste framework é  escreva seu projeto e com o mesmo código exporte para várias plataformas.

**Pré-requisitos**

Python 3.11 ou superior

**Vamos começar**

Crie o ambiente virtual

```
python -m venv venv
```

**Ative o ambiente virtual do python**

```bash
source venv/Scripts/Activate
```
**Instalando o Beeware**

Para instalar o Beeware, execute o seguinte comando:

```
python -m pip install briefcase
```

Este comando instalará o Beeware e todas as suas dependências.

**Criando um novo projeto**

Para criar um novo projeto Beeware, execute o seguinte comando:

```
briefcase new
```
Aí você segue as seguintes etapas no teminal:

Adicione as informações como quiser que serão pedidas no terminal, mas na etapa de licença escolha a opção 7, e na opção de selecionar o GUI Toolkit escolha a opção 1 Toga.

Este comando criará um novo diretório chamado helloworld com os seguintes arquivos:

`__init__`.py: Este arquivo é necessário para que o diretório seja importável como um módulo Python.
`__main__`.py: Este arquivo é um módulo executável que inicia o aplicativo.
`app.py`: Este arquivo contém o código do aplicativo.

**Criando o código do aplicativo**

O código do aplicativo Hello World é muito simples, substitua o código padrão de `app.py` por:

```
"""
My first application
"""
import toga
from toga.style import Pack
from toga.style.pack import COLUMN, ROW


def greeting(name):
    if name:
        return f"Olá, {name}"
    else:
        return "Olá, estranho"

class HelloWorld(toga.App):
    def startup(self):
        main_box = toga.Box(style=Pack(direction=COLUMN))

        name_label = toga.Label(
            "Digite seu nome: ",
            style=Pack(padding=(0, 5))
        )
        self.name_input = toga.TextInput(style=Pack(flex=1))

        name_box = toga.Box(style=Pack(direction=ROW, padding=5))
        name_box.add(name_label)
        name_box.add(self.name_input)

        button = toga.Button(
            " Aperte aqui",
            on_press=self.say_hello,
            style=Pack(padding=5)
        )

        main_box.add(name_box)
        main_box.add(button)

        self.main_window = toga.MainWindow(title=self.formal_name)
        self.main_window.content = main_box
        self.main_window.show()

    def say_hello(self, widget):
        self.main_window.info_dialog(
            greeting(self.name_input.value),
            "Este é seu primeiro App criado usando Beeware, parabéns !!!",
        )


def main():
    return HelloWorld()

```

**Executar o aplicativo no modo de desenvolvedor**

- Execute os comandos:

```
<!-- Vá para a pasta do projeto criado -->
cd helloworld

<!-- Rode o projeto localmente-->
briefcase dev
```

Este é o resultado na versão para desktop:

![](https://i.postimg.cc/cHpPHHtx/desktop.gif)

**Embalando para distribuição**

- Criando seu scaffold de aplicativo

Como esta é a primeira vez que estamos empacotando nosso aplicativo, precisamos criar alguns arquivos de configuração e outros andaimes para suportar o processo de empacotamento. No diretório, execute:

```
briefcase create
```

**Criando seu aplicativo**

Agora você pode compilar seu aplicativo. Esta etapa executa qualquer binário compilação que é necessária para que seu aplicativo seja executável em seu plataforma alvo.

```
briefcase build
```

- Executando seu aplicativo criado:

```
briefcase run
```
Isso começará a executar seu aplicativo nativo, usando a saída do comando `build`.

Caso queira o arquivo executável do projeto para instalação em sistema desktop ele fica no diretório:

```
helloworld/build/desktop/app/dist
```

**Construindo seu instalador**

Agora você pode empacotar seu aplicativo para distribuição, usando o comando. O comando package faz qualquer compilação necessária para converter o projeto de andaimes em um produto final e distribuível.

```
briefcase package
```
Agora temos nosso aplicativo empacotado para distribuição em plataformas desktop.

Se desejar atualizar o código inserindo novas funcionalidades, é necessário atualizar com o comando:

``` 
briefcase update
```

Agora que atualizamos o código do instalador, podemos executar para recompilar o aplicativo, executar o aplicativo atualizado e reempacotar o aplicativo para distribuição, execute: `briefcase build` e depois `briefcase runbriefcase package`.

**Levando-o o projeto para dispositivos móveis: Android**

- Execute:

```
briefcase create android

<!-- && -->

briefcase build android
```

Agora já geramos o build para um aplicativo android, você pode executa-lo tanto no dispositivo virtual quanto no fisico.

**Executar o aplicativo em um dispositivo físico**

Se você tiver um telefone ou tablet Android físico, poderá conectá-lo ao seu computador com um cabo USB e, em seguida, use a pasta para direcionar seu físico dispositivo.

O Android requer que você prepare seu dispositivo antes que ele possa ser usado para desenvolvimento. Você precisará fazer 2 alterações nas opções do seu dispositivo:

- Habilitar opções do desenvolvedor

- Ativar depuração USB

Após configurado o aparelho fisíco android, execute o seguinte comando no terminal:

```
briefcase run android
```

Caso queira disponibilizar o apk do projeto, em uma loja de aplicativos ele  fica armazenado em:

```
helloworld/build/android/app/outputs/apk/release
```


Selecione o seu aparelho no terminal e o projeto irá executar em seu celular físico, se desejar gerar o aplicativo para iOS, veja este [tutorial.](https://docs.beeware.org/en/latest/tutorial/tutorial-5/iOS.html)

**Implantando o projeto como um aplicativo Web**

- Execute:

```
briefcase run web
```
Isso abrirá um navegador da Web, apontando para http://127.0.0.1:8080:
Você verá algo como:

![](https://i.postimg.cc/GhBgtfWM/desktop.gif)

Para fazer deploy da versão web de um projeto beeware em um servidor web, você deve carregar os seguintes arquivos da pasta www do diretório:

```
helloworld/build/helloworld/web/www
```

Agora temos este aplicativo no desktop, no celular e na Web, o aplicativo é bastante simples.

Além do Toga que usamos para utilizar os widgets, é possivel usar uma Bridge para usar Widgets Nativo do Java Android, e roda-los dentro de um projeto BeeWare.

**Como isso é possível ?**

É possivel com a biblioteca [Rubicon](https://beeware.org/project/projects/bridges/rubicon/), que faz a ponte entre Python e Java, para mais detalhes veja o [video](https://www.youtube.com/watch?v=sS0UI0yuLYQ&t=228s), no tempo do vídeo 55:55 minutos.

**Conclusão**

Neste tutorial, você aprendeu a criar um aplicativo Hello World usando Beeware e Python. Para obter mais informações, consulte a documentação do [Beeware](https://beeware.org); Este tutorial fornece um bom ponto de partida para aprender a criar aplicativos, você pode usar o código fornecido como base para criar seus próprios aplicativos.
O BeeWare uiliza a bliblioteca Toga, para usar os Widgets, o que seria o equivalente a os components Ui do material do angular(isto é uma analogia !!), [veja aqui](https://toga.readthedocs.io/en/latest/reference/api/index.html) mais widgets.

O código fonte deste tutorial você pode baixar do [github](https://github.com/Lucas-Ed/tutorial-Beeware)

**Referências:**

- [BeeWare](https://beeware.org)

- [Video 1](https://www.youtube.com/watch?v=3MPgToGghx4)

- [Video 2](https://www.youtube.com/watch?v=_Lkixr3CE48&t=17s)

- [Video 3](https://www.youtube.com/watch?v=sS0UI0yuLYQ)

- [Tutorial Calculadora](https://www.section.io/engineering-education/creating-an-application-using-beeware/)
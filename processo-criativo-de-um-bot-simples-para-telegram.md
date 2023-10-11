![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTuRYAFVIZSDEs2kjEV5jg0LlIniQTFWLH2gw&usqp=CAU)

## Processo de criação de um Bot simples em python
O bot calcula a idade do usuário a partir da data de nascimento.

Passo a passo:

**Passo 1:** Configuração do ambiente

Certifique-se de ter o Python instalado em seu sistema. Você pode baixar a versão mais recente do Python no site oficial: https://www.python.org/downloads/

**Passo 2:** Instalação das dependências

Abra o PowerShell e execute os seguintes comandos para instalar as bibliotecas necessárias:

```
pip install telebot

pip install os

pip install python-dotenv
```
**Passo 3:** Criando um novo bot no Telegram

Para criar um novo bot no Telegram, você precisa interagir com o BotFather. Siga as etapas abaixo:

- Abra o aplicativo Telegram e pesquise por "BotFather".
- Inicie uma conversa com o BotFather.
- Digite o comando "/newbot" para criar um novo bot.
- Siga as instruções do BotFather para escolher um nome e um username para o seu bot.
- Após a conclusão, você receberá um token de acesso para o seu bot. Guarde esse token, pois iremos usá-lo posteriormente.

**Passo 4:** Escrevendo o código do bot

Crie um novo arquivo chamado bot.py e adicione o seguinte código:

```
import telebot
import os
from datetime import datetime

from dotenv import load_dotenv

load_dotenv()

API_TOKEN = os.getenv('TELEGRAM_TOKEN')
bot = telebot.TeleBot(API_TOKEN)


@bot.message_handler(commands=['start', 'help'])
def send_welcome(message):
    bot.reply_to(message, "Olá! Por favor, me diga sua data de nascimento no formato DD/MM/AAAA.")


@bot.message_handler(func=lambda message: True)
def calculate_age(message):
    try:
        birth_date = datetime.strptime(message.text, '%d/%m/%Y')
        current_date = datetime.now()
        age = current_date.year - birth_date.year

        bot.reply_to(message, f"Sua idade é {age} anos.")
    except ValueError:
        bot.reply_to(message, "Formato de data inválido. Por favor, use o formato DD/MM/AAAA.")


# Executar o bot
bot.infinity_polling(skip_pending=True)
```
Crie um arquivo chamado .env no mesmo diretório do arquivo bot.py e adicione a seguinte linha:

```
TELEGRAM_TOKEN=<seu_token>

```
Substitua <seu_token> pelo token de acesso do seu bot obtido anteriormente.

**Passo 5:** Executando o bot no PowerShell

Abra o PowerShell e navegue até o diretório onde você salvou os arquivos bot.py e .env.

Em seguida, execute o seguinte comando em seu terminal shell para iniciar o bot:
`python bot.py
`
Agora, seu bot do Telegram está em execução e pronto para responder aos comandos. Você pode testar enviando o comando /start para o bot no Telegram.
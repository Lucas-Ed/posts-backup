O Streamlit é uma biblioteca de Python que permite criar aplicativos da web de maneira rápida e fácil. Com o Streamlit, é possível criar dashboards interativos, relatórios e outros tipos de aplicativos sem ter que lidar com o HTML, CSS ou JavaScript.

![](https://tecnothink.com.br/wp-content/uploads/2020/11/Streamlit_Logo_1.jpg)

Comece em
menos de um minuto:

```
pip install streamlit
```
A estrutura de aplicativos de código aberto do Streamlit é muito fácil de começar, É só uma questão de:
```
streamlit hello
```
dado o comando anterior irá abrir em seu browser na porta: http://localhost:8501
e você verá o seguinte:

![](https://i.postimg.cc/ht6ypsnY/str.png)

Uma vez instalado, é possível começar a criar um aplicativo Streamlit. Para isso, basta criar um arquivo Python e importar a biblioteca Streamlit usando o seguinte código:


```
import streamlit as st

```

Em seguida, você pode usar os componentes do Streamlit para criar o layout do seu aplicativo. Por exemplo, para adicionar um título ao seu aplicativo, basta usar o comando st.title:


```
import streamlit as st

st.title("Meu primeiro aplicativo Streamlit")

```

O Streamlit possui uma série de componentes prontos para uso, como botões, caixas de seleção, campos de entrada de texto e gráficos. Aqui estão alguns exemplos de como esses componentes podem ser usados:


```
import streamlit as st

# Adicionar um título
st.title("Meu primeiro aplicativo Streamlit")

# Adicionar um botão
if st.button("Clique aqui"):
  st.write("Você clicou no botão!")

# Adicionar uma caixa de seleção
opcoes = ["Opção 1", "Opção 2", "Opção 3"]
escolha = st.selectbox("Escolha uma opção:", opcoes)
st.write("Você escolheu: ", escolha)

# Adicionar um campo de entrada de texto
nome = st.text_input("Qual é o seu nome?")
st.write("Olá, ", nome)

# Adicionar um gráfico
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4])
st.pyplot()

```

Para rodar o seu aplicativo, basta usar o comando `streamlit run` seguido do nome do arquivo Python:


```
streamlit run meu_aplicativo.py

```
Isso fará com que o Streamlit abra o seu aplicativo, que criamos de exemplo em um navegador web, você verá o seguinte:

![](https://i.postimg.cc/nMbFZBfc/str-2.png)

Esse é um exemplo de aplicação pra termos um primeiro contato com o Streamlit, esta bliblioteca Python é muito interessante para fazer DataApps, transformando assim aqueles seus algoritmos de DataScience ou Machine learning, em uma poderosa aplicação web, interativa !

## Deploy 
Para fazer o Deploy de um projeto Streamlit, você pode fazer gratuitamente no cloud [share.streamlit](https://share.streamlit.io), lá você pode hospedar até 3 projetos gratuitamente, para fazer o deploy, você deve deixar o projeto em um repositório no seu github, que o share.streamlit, conectará nele, e você selecionará um projeto pro deploy.

## RESUMO
Vimos que a bliblioteca é muito interressante, o básico que você precisa saber é ter-o instalado a bliblioteca na sua máquina, a partir daí só criar o seu algoritmo usando junto, no arquivo os componentes prontos desta bliblioteca, fazendo o seu import no arquivo, após a construção só roda-lo com o comando do Streamlit, e pronto.

## Links:
[1. Documentação ](https://docs.streamlit.io)
[2. Sobre Mim](https://bit.ly/3o0CAdw)
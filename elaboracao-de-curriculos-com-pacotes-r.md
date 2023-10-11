![](https://beatrizmilz.github.io/RLadies-Git-RStudio-2019/img/rstudio.png)

Tinha utilizado esta ferramenta a uns anos atrás para construção do meu currículo pessoal, decidi fazer este artigo para compartilhar o conhecimento,Construiremos um Currículo usando o Rstudio e alguns pacotes, os pacotes pagedown e knitr, que são ferramentas poderosas para criar documentos dinâmicos com R Markdown e CSS. Com eles, você pode inserir códigos e resultados do R em seus documentos, além de personalizar o layout e o estilo com CSS. Neste artigo, vou mostrar como usar esses pacotes para criar um currículo profissional em PDF.

## **Instalando os pacotes**

Para usar os pacotes pagedown e knitr, você precisa instalá-los no RStudio. Você pode fazer isso usando os comandos:

```
install.packages("pagedown")
install.packages("knitr")
```

## **Criando um documento R Markdown**

Para criar um documento R Markdown, você pode usar o menu File -> New File -> R Markdown… no RStudio, dê um nome ao seu documento. Você verá um arquivo com a extensão .Rmd, que contém o código e o texto do seu documento.

## **Usando o pacote pagedown**

O pacote pagedown fornece vários modelos de documentos em PDF, incluindo um modelo de currículo. Para usá-lo, você precisa alterar o campo output do cabeçalho do seu documento para:

```
output:
  pagedown::html_resume:
# configure-o como verdadeiro para uma página HTML independente, mas levará mais tempo para renderizar
    self_contained: True
```
Isso fará com que o seu documento seja convertido para HTML e depois para PDF usando o navegador Google Chrome ou Chromium. Você também pode especificar algumas opções de formatação, como a cor do tema, a fonte e o tamanho da página. Por exemplo:

```
output:
  pagedown::html_resume:
    theme: cosmo
    fontfamily: roboto
    margin: 1cm
```
Você pode ver a lista completa de opções disponíveis na documentação do pacote [aqui.](https://bit.ly/3sT0eQt)

## Usando o pacote knitr
O pacote knitr permite que você insira blocos de código do R (também chamados de chunks) no seu documento, que serão executados e mostrarão os resultados. Para criar um bloco de código, você precisa usar a sintaxe:


```
```{r}
# seu código aqui

```

Você pode colocar qualquer código do R que quiser dentro dos blocos, como atribuir variáveis, fazer cálculos, gerar gráficos, etc. Você também pode controlar como os blocos serão mostrados no documento usando várias opções, como echo, eval, results, fig.width, fig.height, etc. Por exemplo:

```
```{r echo=FALSE, results='asis'}
# esse bloco não mostra o código, apenas o resultado
cat("Meu nome é", Sys.getenv("USER"), ".")
```
Você pode ver a lista completa de opções disponíveis na documentação do pacote [aqui.](https://bit.ly/3sOjXRy)

## Escrevendo o conteúdo do currículo

Agora que você já configurou os pacotes pagedown e knitr, você pode começar a escrever o conteúdo do seu currículo. Você pode usar a linguagem de marcação Markdown para formatar o seu texto com elementos como títulos, listas, links, imagens, etc. Você também pode usar expressões matemáticas em LaTeX usando os símbolos `$...$` ou `$$...$$.` Por exemplo:

```
Contato e informações {#contact}
-------------------------------------------------------------------------------
- <i class="fa fa-envelope"></i> lucas-araras@outlook.com
- <i class="fa fa-github"></i> [github.com/Lucas-Ed](https://bit.ly/2HcqU7j)
- <i class="fab fa-linkedin-in"></i> [linkedin](https://bit.ly/3cxTFI3)
- <i class="fa-brands fa-blogger"></i> [Meu blog.](https://bit.ly/47reCiX)
- <i class="fa fa-phone"></i> +55 (19) 99823-5078
- <i class="fa fa-phone"></i> +55 (19) 3544-5788
- Para mais informações, entre em contato.


```

no campo Main coloque mais dados, como neste exemplo:


```
Main
================================================================================

Lucas Eduardo Rosolem {#title}
--------------------------------------------------------------------------------


<!---Insira aqui um texto introdutório---> 


Educação {data-icon=graduation-cap data-concise=true}
-------------------------------------------------------------------------------


### Pythonando Cursos Ltda
Participação mini curso, intensivão semanal de Python-PSW |8.0.
Desenvolvimento de um sistema de laboratório com Django.

Online

2023

### Samsung (Ocean)
Participação mini curso,
Frontend Web ReactJS-introdutório.

Online

2023

### Samsung (Ocean)
Participação mini curso,
Desenvolvimento Ágil- DevOps Docker.

Online

2023

### Senai-Luiz Varga
Programador Front-End-
**(HTML-JS-ANGULAR-TS)**

Limeira, Brasil

2021

### CEV Treinamentos
Programação HTML5 e PHP

Online

2017

### Microcamp internacional

Lógica de programação
Técnicas de programação em Pascal e
Delphi com mySQL

Araras, Brasil

2006

### People computação

Hardware avançado-Montagem e manutenção de computadores-práticas de redes ponto a ponto. 

Araras, Brasil

2004

```
aqui coloquei apenas os cursos que fiz, você pode customizar como quiser, pode incluir também experiências profissionais.

Gerando o PDF
Para gerar o PDF do seu currículo, você pode usar o botão Knit no RStudio, que irá chamar os pacotes pagedown e knitr para processar o seu documento.

[![kn.png](https://i.postimg.cc/GtCHTg7J/kn.png)](https://postimg.cc/CBcFW7Vz)

Você verá o resultado na janela do navegador e poderá salvar o PDF no seu computador.

[![pdf.png](https://i.postimg.cc/26m1VXXd/pdf.png)](https://postimg.cc/R3sSYGmq)

Para gerar o pdf clique para abrir no browser e salve como pdf.
Você pode usar o meu como referência veja [aqui.](https://bit.ly/3Rxkh1x)

Se preferir também é possivel construir o currículo buscando os dados de uma planilha do google, com o pacote datadrivencv, eu ainda não cheguei a fazer desta forma mas você pode ver como fazer [aqui](http://nickstrayer.me/datadrivencv/); desta maneira só precisa manter atualizado a planilha com os dados a serem usados.

Espero que este artigo tenha sido útil para você aprender a usar os pacotes pagedown e knitr do RStudio para elaborar currículos. Se você quiser saber mais sobre esses pacotes, você pode consultar as referências abaixo. Obrigado por ler! 😊

**Referências**

- [Knitr](https://bookdown.org/yihui/rmarkdown-cookbook/kable.html)

- [Pagedown usage](https://pagedown.rbind.io/#resume)

- [Pagedown package](https://github.com/rstudio/pagedown)

- [datadrivencv](https://github.com/nstrayer/datadrivencv)
![](https://miro.medium.com/v2/resize:fit:1200/1*pD_YMyWDg8A2grOrbaNS6g.jpeg)

***Cron Job*** é um utilitário do sistema operacional Linux que permite agendar a execução de tarefas em um horário específico. Ele é uma ferramenta poderosa que pode ser usada para automatizar uma variedade de tarefas, como backups, limpeza de arquivos, atualizações de software e muito mais.

***Como funciona***

Cron Job funciona usando um arquivo chamado `crontab`. Este arquivo contém uma lista de tarefas que devem ser executadas, bem como o horário em que elas devem ser executadas. O arquivo `crontab` é um arquivo de texto simples que pode ser editado usando um editor de texto, como o Vim ou o Nano.

Estrutura do arquivo `crontab`

O arquivo crontab é dividido em seis campos:

- Minuto: O minuto em que a tarefa deve ser executada.
- Hora: A hora em que a tarefa deve ser executada.
- Dia do mês: O dia do mês em que a tarefa deve ser executada.
- Mês: O mês em que a tarefa deve ser executada.
- Dia da semana: O dia da semana em que a tarefa deve ser executada.
- Comando: O comando que deve ser executado.

***Exemplo***

O seguinte exemplo mostra como agendar a execução do comando `ls -al` às 12:00 da manhã todos os dias:

```
0 12 * * * ls -al
```
Este comando irá executar o comando `ls -al` às 12:00 da manhã todos os dias, independentemente do dia da semana ou do mês.

***Opções avançadas***

Além dos campos básicos, o arquivo `crontab` também suporta uma variedade de opções avançadas, como:

`@reboot`: Executa a tarefa na inicialização do sistema.
`@yearly`: Executa a tarefa uma vez por ano, no dia 1º de janeiro.
`@monthly`: Executa a tarefa uma vez por mês, no primeiro dia do mês.
`@weekly`: Executa a tarefa uma vez por semana, no mesmo dia da semana.
`@daily`: Executa a tarefa uma vez por dia, no mesmo horário.
`@hourly`: Executa a tarefa uma vez por hora, no mesmo minuto.

***Configurando Cron Job***

Para configurar um Cron Job, você precisa editar o arquivo `crontab`. Você pode fazer isso usando um editor de texto, como o Vim ou o Nano.

Para editar o arquivo crontab, abra um terminal e execute o seguinte comando:

```
crontab -e
```

Isso abrirá o arquivo `crontab` no editor de texto padrão.

Adicione a tarefa que você deseja agendar ao arquivo `crontab`.

Para salvar as alterações, pressione `Ctrl+X` e digite `Y` para confirmar.

***Testando Cron Job***

Para testar um Cron Job, você pode usar o comando `crontab -l` para exibir a lista de tarefas agendadas.

Você também pode usar o comando `crontab -r` para remover todas as tarefas agendadas.

***Geradores de sintaxe Crontab***
Agora que você já se familiarizou com a sintaxe do cron e percebeu que não é nada tão assustador quanto parecia ser, saiba que você não precisa gerar seus arquivos crontab de forma manual sempre, não precisa memorizar. Há alguns geradores de sintaxe crontab baseados na web disponíveis para tornar esse trabalho ainda mais fácil.

**Crontab guru**
O [Crontab guru](https://crontab.guru/) é um aplicativo web que auxiliará você na criação de cron jobs. Funciona de maneira bastante simples, basta inserir suas entradas no site e ele criará instantaneamente uma sintaxe crontab.

**Crontab Generator**
O [Crontab Generator](https://crontab-generator.org/) é outro app web que ajudará na criação de cron jobs. Trata-se de um formulário que possui várias entradas, você deve escolher todos os campos obrigatórios no formulário e, por fim, gerar sua expressão crontab de forma rápida e fácil.

**Cron e shell script, uma excelente combinação**

Utilizando o cron, você também pode agendar um programa shell script, como, por exemplo, um script que faz backup de tudo que é necessário todos as sextas às 00:00:

```
0 0 * * 5 /bin/sh backup.sh
```
Porém, antes de criar um shell script que faça um backup e agendá-lo com o cron, é necessário, é claro, que você saiba como escrever um programa em shell script. Para isso, o Diolinux Play criou um curso de Shell Script avançado totalmente grátis. Inscreva-se agora mesmo se você quer aprender tudo sobre Shell Script para automatizar suas tarefas do cotidiano e tornar o seu dia a dia mais produtivo, veja [aqui](https://diolinux.com.br/curso-de-shell-linux-avancado-gratis).

***Conclusão***

Cron Job é uma ferramenta poderosa que pode ser usada para automatizar uma variedade de tarefas. Com um pouco de conhecimento, você pode usar o Cron Job para simplificar sua vida e melhorar a eficiência do seu sistema Linux.

***Referências***

- Cron Job | Diolinux: https://diolinux.com.br/tutoriais/entenda-o-que-e-cron-job.html
- Crontab | Manual do Linux: https://man7.org/linux/man-pages/man5/crontab.5.html
- Contrab | Hostinger  : https://www.hostinger.com.br/tutoriais/cron-job-guia
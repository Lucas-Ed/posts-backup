
# 📧 Como Enviar E-mails Usando PHPMailer e Gmail no XAMPP (Ambiente de Desenvolvimento & Produção)

Enviar e-mails é essencial em muitas aplicações web. Neste guia completo, você vai aprender a configurar **PHPMailer** no ambiente de desenvolvimento com **XAMPP** e como fazer a transição correta para **produção**, com foco em segurança e boas práticas.

---

## 📦 Instalação do PHPMailer

Independente do ambiente, o primeiro passo é instalar a biblioteca via **Composer**:

```bash
composer require phpmailer/phpmailer
```

---

## 🧪 Ambiente de Desenvolvimento com XAMPP

### 1. Configuração de sendmail do xampp, ativado-o na instalação.
Na etapa de instalação do xampp é importante deixar a caixinha FakeSendmail selecionada igual na imagem abaixo:
![](https://i.postimg.cc/mgg4CzMc/Capturar.jpg)

### 2. Configurando o `php.ini`

Edite o arquivo:

```
C:\xampp\php\php.ini
```

Localize a seção `[mail function]` e altere:

```ini
[mail function]
SMTP=smtp.gmail.com
smtp_port=587
sendmail_from=seu-email@gmail.com
sendmail_path="\"C:\xampp\sendmail\sendmail.exe\" -t"
```

> **Dica**: Substitua `seu-email@gmail.com` pelo seu e-mail real.

---

### 3. Configurando o `sendmail.ini`

Abra:

```
C:\xampp\sendmail\sendmail.ini
```

Troque o conteúdo do arquivo sendmail.ini por:

```ini
[sendmail]
smtp_server=smtp.gmail.com
smtp_port=587
smtp_ssl=tls
auth_username=seu-email@gmail.com
auth_password=sua-senha-de-app-do-gmail
```

> ✅ Use sempre uma **senha de app** gerada na sua conta Google:  
> [Gerar senha de app](https://myaccount.google.com/apppasswords)
> Exemplo de uma senha de APP do gmail: erfi yeod uyua wiag

---

### 4. Script PHP para Teste

Crie um arquivo `enviar-email.php`:

```php
<?php
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\Exception;

require 'vendor/autoload.php';

$mail = new PHPMailer(true);

try {
    $mail->isSMTP();
    $mail->Host = 'smtp.gmail.com';
    $mail->SMTPAuth = true;
    $mail->Username = 'seu-email@gmail.com';
    $mail->Password = 'sua-senha-de-app-do-gmail';
    $mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;
    $mail->Port = 587;

    $mail->setFrom('seu-email@gmail.com', 'Seu Nome');
    $mail->addAddress('destinatario@exemplo.com');

    $mail->isHTML(true);
    $mail->Subject = 'Teste PHPMailer';
    $mail->Body = '<b>Funcionando!</b>';

    $mail->send();
    echo 'E-mail enviado com sucesso!';
} catch (Exception $e) {
    echo "Erro ao enviar e-mail: {$mail->ErrorInfo}";
}
?>
```

Execute via terminal:

```bash
php enviar-email.php
```

---

## 🚀 Como Configurar em Ambiente de Produção

Em produção, **não usamos `sendmail.exe` nem configuramos o `php.ini` diretamente**. Em vez disso:

### ✅ O que muda:

| Aspecto                          | Desenvolvimento (XAMPP)          | Produção (Servidor Real)                     |
|----------------------------------|----------------------------------|----------------------------------------------|
| SMTP                             | Gmail (via sendmail.exe)         | Gmail, Amazon SES, Mailgun, SMTP próprio     |
| Configuração de e-mail           | php.ini + sendmail.ini           | Somente via PHPMailer (código PHP)           |
| Armazenamento de credenciais     | Hardcoded no script (ruim!)      | Variáveis de ambiente (.env) ou secrets vault|
| Segurança                        | Básica                           | Obrigatório TLS/SSL e senhas protegidas      |

---

### 📁 Exemplo com Variáveis de Ambiente

**Nunca exponha sua senha no código!** Use `.env` ou similar com [vlucas/phpdotenv](https://github.com/vlucas/phpdotenv).

```bash
# .env
MAIL_USERNAME=seu-email@gmail.com
MAIL_PASSWORD=sua-senha-de-app
```

No código PHP:

```php
$dotenv = Dotenv\Dotenv::createImmutable(__DIR__);
$dotenv->load();

$mail->Username = $_ENV['MAIL_USERNAME'];
$mail->Password = $_ENV['MAIL_PASSWORD'];
```

---

### 🛡️ Regras de Segurança em Produção

- ✅ Sempre use `STARTTLS` ou `SMTPS` (porta 465);
- ❌ Nunca exponha senhas no código;
- ✅ Use logs para registrar falhas, mas **nunca** exiba erros para o usuário final;
- ✅ Configure SPF/DKIM/DMARC no domínio se usar e-mails personalizados.

---

## ✅ Conclusão

Agora você está preparado para enviar e-mails com PHPMailer tanto em **ambientes locais com XAMPP**, quanto em **servidores de produção seguros**. Evite práticas inseguras como senhas no código e use serviços confiáveis de SMTP para garantir entrega e reputação.

---

### 🔗 Recursos úteis

- [PHPMailer no GitHub](https://github.com/PHPMailer/PHPMailer)
- [Composer](https://getcomposer.org/)
- [Gmail App Passwords](https://myaccount.google.com/apppasswords)
- [phpdotenv](https://github.com/vlucas/phpdotenv)
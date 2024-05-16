---
title: SSL/TLS por padrão
description: Saiba como usar o SSL por padrão no AEM 6.5.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
exl-id: 574e2fc2-6ebf-49b6-9b65-928237a8a34d
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 9b766fe6e253782be3bc47849b4857216274ae20
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# SSL/TLS por padrão{#ssl-tls-by-default}

Em um esforço para melhorar continuamente a segurança do AEM, o Adobe introduziu um recurso chamado SSL por padrão. O objetivo é incentivar o uso de HTTPS para se conectar a instâncias AEM.

## Habilitar SSL/TLS por padrão {#enabling-ssl-tls-by-default}

Você pode começar a configurar SSL/TLS por padrão clicando na mensagem relevante da Caixa de entrada na tela inicial do AEM. Para acessar a Caixa de entrada, pressione o ícone de sino no canto superior direito da tela. Em seguida, clique em **Exibir todos**. Isso exibirá uma lista de todos os alertas ordenados em uma exibição de lista.

Na lista, selecione e abra a variável **Configurar HTTPS** alerta:

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>Se a variável **Configurar HTTPS** alerta não estiver presente na Caixa de entrada, você poderá navegar diretamente para o Assistente HTTPS acessando *<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*

Um usuário de serviço chamado **ssl-service** foi criada para este recurso. Depois de abrir o alerta, você será guiado pelo seguinte assistente de configuração:

1. Primeiro, configure as Credenciais de armazenamento. Estas são as credenciais para o **ssl-service** armazenamento de chaves do usuário do sistema que conterá a chave privada e o armazenamento de confiança para o ouvinte de HTTPS.

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. Depois de inserir as credenciais, clique em **Próxima** no canto superior direito da página. Em seguida, faça upload da chave privada e do certificado associados para a conexão SSL/TLS.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >Para obter informações sobre como gerar uma chave privada e um certificado para usar com o assistente, consulte [este procedimento](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard) abaixo.

1. Por fim, especifique o nome de host HTTPS e a porta TCP para o ouvinte HTTPS.

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## Automatização de SSL/TLS por padrão {#automating-ssl-tls-by-default}

Há três maneiras de automatizar o SSL/TLS por padrão.

### Via POST HTTP {#via-http-post}

O primeiro método envolve publicar no servidor SSLSetup que está sendo usado pelo assistente de configuração:

```shell
POST /libs/granite/security/post/sslSetup.html
```

Você pode usar a seguinte carga no POST para automatizar a configuração:

```xml
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePassword"

test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePassword"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="privatekeyFile"; filename="server.der"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="certificateFile"; filename="server.crt"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="httpsPort"
8443
```

O servlet, como qualquer servlet POST sling, responderá com 200 OK ou um código de status HTTP de erro. Você pode encontrar detalhes sobre o status no corpo do HTML da resposta.

Abaixo estão exemplos de uma resposta bem-sucedida e um erro.

**EXEMPLO DE SUCESSO** (status = 200):

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>OK</title>
</head>
<body>
<h1>OK</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>200</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>SSL successfully configured</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>OK</dd>
<dt class='foundation-form-response-description'>Description</dt>
<dd>HTTPS has been configured on port 8443. The private key and
certificate were stored in the key store of the user ssl-service.
Take note of the key store password you provided. You need
it for any subsequent updating of the private key or certificate.</dd>
</dl>
<h2>Links</h2>
<ul class='foundation-form-response-links'>
<li><a class='foundation-form-response-redirect' href='/'>Done</a></li>
</ul>
</body>
</html>
```

**EXEMPLO DE ERRO** (status = 500):

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>Error</title>
</head>
<body>
<h1>Error</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>500</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>The provided file is not a valid key, DER format expected</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>Error</dd>
</dl>
</body>
</html>
```

### Através do pacote {#via-package}

Como alternativa, você pode automatizar a configuração de SSL/TLS carregando um pacote que já contém os seguintes itens necessários:

* O keystore do usuário do serviço ssl. Está localizado em */home/users/system/security/ssl-service/keystore* no repositório.
* A variável `GraniteSslConnectorFactory` configuração

### Geração de um par de chave privada/certificado para uso com o assistente {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

Abaixo você encontrará um exemplo para criar um certificado autoassinado no formato DER que o Assistente SSL/TLS pode usar. Instale o OpenSSL com base no sistema operacional, abra o prompt de comando do OpenSSL e altere o diretório para a pasta onde deseja gerar a Chave privada/Certificado.

>[!NOTE]
>
>O uso de um certificado autoassinado serve apenas para fins de amostra. Não use na produção.

1. Primeiro, crie a chave privada:

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. Em seguida, gere uma Solicitação de assinatura de certificado (CSR) usando a chave privada:

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj "/CN=localhost"
   ```

1. Gere o certificado SSL/TLS e assine-o com a chave privada. Neste exemplo, expirará daqui a um ano:

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

1. Converta a chave privada para o formato DER. Isso ocorre porque o assistente SSL requer que a chave esteja no formato DER:

   ```shell
   openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
   ```

1. Por fim, carregue o **localhostprivate.der** como a Chave privada e **localhost.crt** como o Certificado SSL/TLS na etapa 2 do Assistente gráfico SSL/TLS descrito no início desta página.

### Atualização da configuração SSL/TLS via cURL {#updating-the-ssl-tls-configuration-via-curl}

>[!NOTE]
>
>Consulte [Uso do cURL com AEM](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/curl.html) para obter uma lista centralizada de comandos cURL úteis no AEM.

Você também pode automatizar a configuração de SSL/TLS usando a ferramenta cURL. Você pode fazer isso publicando os parâmetros de configuração neste URL:

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

Abaixo estão os parâmetros que você pode usar para alterar as várias configurações no assistente de configuração:

* `-F "keystorePassword=password"` - a senha do keystore;

* `-F "keystorePasswordConfirm=password"` - confirme a senha do keystore;

* `-F "truststorePassword=password"` - a senha do truststore;

* `-F "truststorePasswordConfirm=password"` - confirme a senha do truststore;

* `-F "privatekeyFile=@localhostprivate.der"` - especifique a chave privada;

* `-F "certificateFile=@localhost.crt"` - especificar o certificado;

* `-F "httpsHostname=host.example.com"`- especificar o nome do host;
* `-F "httpsPort=8443"` - a porta em que o ouvinte HTTPS funcionará.

>[!NOTE]
>
>A maneira mais rápida de executar o cURL para automatizar a configuração SSL/TLS é a partir da pasta em que os arquivos DER e CRT estão. Como alternativa, você pode especificar o caminho completo na variável `privatekeyFile` e certificateFile.
>
>Você também precisa ser autenticado para executar a atualização. Portanto, anexe o comando cURL à `-u user:passeword` parâmetro.
>
>Um comando cURL post correto deve ter esta aparência:

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### Vários certificados usando cURL {#multiple-certificates-using-curl}

Você pode enviar ao servlet uma cadeia de certificados repetindo o parâmetro certificateFile da seguinte maneira:

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

Depois de executar o comando, verifique se todos os certificados chegaram ao keystore. Verifique a **Armazenamento de chaves** entradas de:
[http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service)

### Habilitação de uma conexão TLS 1.3 {#enabling-tls-connection}

1. Ir para o Console da Web
1. Em seguida, navegue até **OSGi** - **Configuração** - **Fábrica de conectores SSL do Adobe Granite**
1. Vá para a **Conjuntos de cifras incluídos** e adicione as seguintes entradas. Você pode confirmar cada adição pressionando o botão &quot;**+**&quot; à esquerda do campo, depois de adicionar cada um em:

   * `TLS_AES_256_GCM_SHA384`
   * `TLS_AES_128_GCM_SHA256`
   * `TLS_CHACHA20_POLY1305_SHA256`
   * `TLS_AES_128_CCM_SHA256`
   * `TLS_AES_128_CCM_8_SHA256`

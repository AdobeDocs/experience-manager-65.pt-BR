---
title: Ferramenta de servidor proxy (proxy.jar)
description: Saiba mais sobre a Ferramenta de servidor proxy (proxy.jar) na Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 3df50303-5cdd-4df0-abec-80831d2ccef7
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# Ferramenta de servidor proxy (proxy.jar){#proxy-server-tool-proxy-jar}

O servidor proxy atua como um servidor intermediário que transmite solicitações entre um cliente e um servidor. O servidor proxy rastreia todas as interações cliente-servidor e gera um log de toda a comunicação TCP. Isso permite monitorar exatamente o que está acontecendo, sem precisar acessar o servidor principal.

Você pode encontrar o servidor proxy na pasta de instalação apropriada:

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

Você pode usar o servidor proxy para monitorar toda a interação cliente-servidor, independentemente do protocolo de comunicação subjacente. Por exemplo, você pode monitorar os seguintes protocolos:

* HTTP para páginas da Web
* HTTPS para páginas da Web seguras
* SMTP para mensagens de email
* LDAP para gerenciamento de usuários

Por exemplo, você pode posicionar o servidor proxy entre dois aplicativos que se comunicam por meio de uma rede TCP/IP; por exemplo, um navegador da Web e AEM. Isso permite monitorar exatamente o que acontece quando você solicita uma página AEM.

## Iniciando a Ferramenta de Servidor Proxy {#starting-the-proxy-server-tool}

A ferramenta pode ser encontrada na pasta /opt/helpers da instalação do AEM. Para iniciar, digite:

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### Opções {#options}

* **q (modo silencioso)** Não grava as solicitações na janela do console. Use-a se não quiser retardar a conexão ou se registrar a saída em um arquivo (consulte a opção -logfile ).
* **b (Modo binário)** Se estiver procurando combinações específicas de bytes no tráfego, ative o modo binário. A saída contém as saídas hexadecimal e de caractere.
* **t (entradas do log de carimbo de data e hora)** Adiciona um carimbo de data/hora a cada saída de log. O carimbo de data e hora é expresso em segundos, portanto, pode não ser adequado para a verificação de solicitações únicas. Use-a para localizar eventos que ocorreram em um horário específico se você usar o servidor proxy por um período mais longo.
* **logfile &lt;filename> (gravar no arquivo de log)** Grava a conversa cliente-servidor em um arquivo de log. Esse parâmetro também funciona no modo silencioso.
* **i &lt;numindentions> (adicionar recuo)** Cada conexão ativa é recuada para melhorar a leitura. O padrão é 16 níveis. (Novo no proxy.jar versão 1.16).

## Usos da ferramenta Servidor proxy {#uses-of-the-proxy-server-tool}

Os cenários a seguir ilustram algumas das finalidades para as quais a Ferramenta de Servidor Proxy pode ser usada:

**Verificar se há cookies e seus valores**

O exemplo de entrada de log a seguir mostra todos os cookies e seus valores enviados pelo cliente na sexta conexão aberta desde o início do proxy:

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**Verificação de Cabeçalhos e seus Valores** O exemplo de entrada de log a seguir mostra que o servidor pode fazer uma conexão keep-alive e o cabeçalho de comprimento de conteúdo foi definido corretamente:

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**Verificando se a opção Keep-Alive funciona**

**Manter ativo** significa que um cliente reutiliza a conexão com o servidor para transportar vários arquivos (código da página, imagens, folhas de estilos e assim por diante). Sem o keep-alive, o cliente precisa estabelecer uma nova conexão para cada solicitação.

Para verificar se o keep-alive funciona:

1. Inicie o servidor proxy.
1. Solicitar uma página.

* Se o keep-alive estiver funcionando, o contador de conexões nunca deverá ultrapassar 5 a 10 conexões.
* Se o keep-alive não estiver funcionando, o contador de conexões aumentará rapidamente.

**Localizando solicitações perdidas**

Se você perder solicitações em uma configuração de servidor complexa, por exemplo, com um firewall e um Dispatcher, poderá usar o servidor proxy para descobrir onde a solicitação foi perdida. Se houver um firewall:

1. Iniciar um proxy antes de um firewall
1. Iniciar outro proxy após um firewall
1. Use-os para ver até que ponto as solicitações estão chegando.

**Solicitações Deslocadas**

Se você tiver solicitações de alteração de vez em quando:

1. Inicie um proxy.jar.
1. Aguarde ou grave o log de acesso em um arquivo - com cada entrada tendo um carimbo de data e hora.
1. Quando a solicitação começa a travar, você pode ver quantas conexões estavam abertas e qual solicitação está causando problemas.

## O formato das mensagens de registro {#the-format-of-log-messages}

As entradas de log produzidas por proxy.jar têm o seguinte formato:

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

Por exemplo, uma solicitação de página da Web pode ter a seguinte aparência:

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C significa que essa entrada vem do cliente (é uma solicitação para uma página da Web)
* 0 é o número da conexão (o contador de conexões começa em 0)
* #00000 o deslocamento no fluxo de bytes. Esta é a primeira entrada, portanto, o deslocamento é 0.
* [GET &lt;?>] é o conteúdo da solicitação, no exemplo de um dos cabeçalhos HTTP (url).

Quando uma conexão é fechada, as seguintes informações são registradas:

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Isso mostra o número de bytes transmitidos entre cliente e servidor na sexta conexão e na velocidade média.

## Um exemplo de saída de log {#an-example-of-log-output}

Revise um modelo simples que produz o seguinte código quando solicitado:

```xml
<html>
  <head>
    <title>Welcome</title>
  </head>
  <body>
    Welcome to Playground<br>
    <img src="/logo.gif">
  </body>
</html>
```

Se o AEM estiver em execução no localhost:4303, inicie o servidor proxy da seguinte maneira:

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

Você pode acessar o servidor (`localhost:4303`) sem o servidor proxy, mas se você acessá-lo via `localhost:4444`, o servidor proxy registra a comunicação. Abra um navegador e acesse uma página criada com o modelo acima. Depois disso, verifique o arquivo de log.

>[!NOTE]
>
>Até a versão 1.14 do proxy.jar, as entradas de log de uma conexão não são sincronizadas, o que significa que as entradas de log de uma conexão cliente/servidor não são necessárias na ordem sequencial correta. As versões mais recentes (>=1.14) do servidor proxy não apresentam esse problema.

Ao iniciar, as seguintes informações são gravadas no log:

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

Os seguintes campos de cabeçalho são listados no início da primeira conexão (0), que está solicitando a página HTML principal:

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

O cliente solicita uma conexão keep-alive, para que o servidor possa enviar vários arquivos pela mesma conexão:

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

O servidor proxy é uma boa ferramenta para verificar se os cookies estão configurados corretamente ou não. Aqui, você vê o seguinte:

* cookie cq3session gerado por AEM
* o cookie show mode switch gerado pelo CFC
* um cookie chamado JSESSIONID; isso é criado automaticamente pelo JSP se não for explicitamente desativado usando &lt;%@ page session=&quot;false&quot; %>:

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

O servidor fechará a conexão 0 após a solicitação. O keep-alive não é possível, pois a solicitação tem um ponto de interrogação. Isso significa que o servidor não pode retornar uma versão em cache e, portanto, não pode determinar o comprimento do conteúdo neste ponto, que é necessário para uma conexão keep-alive.

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

Aqui, o servidor começa a enviar o código de HTML na conexão 0:

```xml
S-0-#000234 -> [<html> ]
S-0-#000242 -> [.<head> ]
S-0-#000251 -> [..<title>Welcome</title> ]
S-0-#000277 -> [.</head> ]
S-0-#000287 -> [.<body> ]
S-0-#000296 -> [..Welcome to Playground<br> ]
S-0-#000325 -> [..<img src="/author/logo.gif"> ]
S-0-#000357 -> [.</body> ]
S-0-#000367 -> [</html>]
```

A conexão 0 é fechada imediatamente após o arquivo HTML ter sido fornecido:

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

Agora, a saída é iniciada para a conexão 1, que baixa a imagem contida no código HTML:

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

Novamente, o cliente solicita uma conexão keep-alive:

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

Para a conexão 1, o servidor pode fornecer keep-alive, porque a imagem é estática e, portanto, a duração do conteúdo é conhecida.

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

O servidor retorna o comprimento do conteúdo da imagem na conexão 1:

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

Agora que a duração do conteúdo foi estabelecida, o servidor envia os dados da imagem na conexão 1:

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

Depois que o tempo limite do keep-alive é atingido, a conexão 1 também é fechada:

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

O exemplo acima é comparativamente simples, porque as duas conexões ocorrem sequencialmente:

* primeiro, o servidor retorna o código HTML
* em seguida, o navegador solicita a imagem e abre uma nova conexão

Na prática, uma página pode gerar muitas solicitações paralelas para imagens, folhas de estilos, arquivos JavaScript e assim por diante. Isso significa que os logs têm entradas sobrepostas de conexões abertas paralelas. Nesse caso, o Adobe recomenda usar a opção -i para melhorar a legibilidade.

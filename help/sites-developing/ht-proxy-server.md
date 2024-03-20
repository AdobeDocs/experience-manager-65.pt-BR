---
title: Como usar a ferramenta Servidor proxy
description: O servidor proxy atua como um servidor intermediário que retransmite solicitações entre um cliente e um servidor
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 7222a0c3-cdb9-4c73-9d53-26f00792e439
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---

# Como usar a ferramenta Servidor proxy{#how-to-use-the-proxy-server-tool}

O servidor proxy atua como um servidor intermediário que transmite solicitações entre um cliente e um servidor. O servidor proxy rastreia todas as interações cliente-servidor e gera um log de toda a comunicação TCP. Isso permite monitorar exatamente o que está acontecendo, sem precisar acessar o servidor principal.

Você pode encontrar o servidor proxy na sua instalação AEM aqui:

`crx-quickstart/opt/helpers/proxy-2.1.jar`

Você pode usar o servidor proxy para monitorar toda a interação cliente-servidor, independentemente do protocolo de comunicação subjacente. Por exemplo, você pode monitorar os seguintes protocolos:

* HTTP para páginas da Web
* HTTPS para páginas da Web seguras
* SMTP para mensagens de email
* LDAP para gerenciamento de usuários

Por exemplo, você pode posicionar o servidor proxy entre dois aplicativos que se comunicam por meio de uma rede TCP/IP; por exemplo, um navegador da Web e AEM. Isso permite monitorar exatamente o que acontece quando você solicita uma página do CQ.

## Iniciando a Ferramenta de Servidor Proxy {#starting-the-proxy-server-tool}

Iniciar o servidor na linha de comando:

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**Parâmetros**

`<host>`

Esse é o endereço do host da instância do CRX à qual você deseja se conectar. Se a instância estiver no computador local, isso será `localhost`.

`<remoteport>`

Esta é a porta do host da instância do CRX de destino. Por exemplo, o padrão de uma instalação de AEM recém-instalada é **`4502`** e o padrão para uma instância de autor AEM recém-instalada é `4502`.

`<localport>`

Essa é a porta no computador local à qual você deseja se conectar para acessar a instância do CRX por meio do proxy.

**Opções**

`-q` (modo silencioso)

Não grava a saída na janela do console. Use-a se não quiser retardar a conexão ou se registrar a saída em um arquivo (consulte a opção -logfile ).

`-b`(modo binário)

Se estiver procurando combinações específicas de bytes no tráfego, ative o modo binário. A saída conterá a saída hexadecimal e de caracteres.

`-t` (entradas de log de carimbo de data e hora)

Adiciona um carimbo de data/hora a cada saída de log. O carimbo de data e hora é expresso em segundos, portanto, pode não ser adequado para a verificação de solicitações únicas. Use-a para localizar eventos que ocorreram em um horário específico se você usar o servidor proxy por um período mais longo.

`-logfile <filename>`(gravar no arquivo de log)

Grava a conversa cliente-servidor em um arquivo de log. Esse parâmetro também funciona no modo silencioso.

**`-i <numIndentions>`**(adicionar recuo)

Cada conexão ativa é recuada para melhorar a leitura. O padrão é 16 níveis. Esse recurso foi introduzido com o `proxy.jar version 1.16`.

### Formato do Log {#log-format}

As entradas de log produzidas por proxy-2.1.jar têm o seguinte formato:

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

Por exemplo, uma solicitação de página da Web pode ter a seguinte aparência:

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C significa que essa entrada vem do cliente (é uma solicitação para uma página da Web)
* 0 é o número da conexão (o contador de conexões começa em 0)
* #00000 o deslocamento no fluxo de bytes. Esta é a primeira entrada, portanto, o deslocamento é 0.
* `[GET <?>]` é o conteúdo da solicitação, no exemplo de um dos cabeçalhos HTTP (url).

Quando uma conexão é fechada, as seguintes informações são registradas:

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Isso mostra o número de bytes transmitidos entre o cliente ( `C`) e o servidor ( `S`) na sexta conexão e na velocidade média.

**Um exemplo de saída de log**

Como exemplo, considere uma página que produz o seguinte código quando solicitado:

### Exemplo {#example}

Como exemplo, considere um documento html simples no repositório em

`/content/test.html`

Ao lado de um arquivo de imagem em

`/content/test.jpg`

O conteúdo de `test.html` é:

```xml
<html>
<head>
    <title>Test</title>
</head>
<body>
    Test<br>
    <img src="test.jpg">
</body>
</html>
```

Supondo que a instância AEM esteja em execução `localhost:4502`, o proxy é iniciado assim:

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

A instância do CQ/CRX agora pode ser acessada por meio do proxy em `localhost:4444` e toda a comunicação por meio desta porta é registrada em `test.log`.

Agora, se você observar a saída do proxy, verá a interação entre o navegador e a instância do AEM.

Na inicialização, o proxy gera o seguinte:

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

Agora abra um navegador e acesse a página de teste:

`http://localhost:4444/content/test.html`

E você vê que o navegador faz uma `GET` solicitação para a página:

```shell
C-0-#000000 -> [GET /content/test.html HTTP/1.1 ]
C-0-#000033 -> [Host: localhost:4444 ]
C-0-#000055 -> [Connection: keep-alive ]
C-0-#000079 -> [User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11 ]
C-0-#000212 -> [Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 ]
C-0-#000285 -> [Accept-Encoding: gzip,deflate,sdch ]
C-0-#000321 -> [Accept-Language: en-US,en;q=0.8 ]
C-0-#000354 -> [Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3 ]
C-0-#000402 -> [Cookie: login-token=179ba6bd-e0a7-4909-a965-e11c7f2bc2fc%3a618bd8a8-fbaf-43c5-827d-c84c62248c5e_22ee860cc9036fee%3acrx.default%3b21148fb0-eb6c]
C-0-#000543 -> [-43c9-a2b9-c8d40618d8ae%3ad87a3d1a-5e9a-4d5a-bab1-0ee60ad6d8df_d0e4ddce0fcd84b6%3acrx.default%3b5cb95227-ea51-47bf-850b-68ad1dfd7297%3af3bbb6]
C-0-#000684 -> [59-7913-4285-8857-832c087bafd5_c484727d3b3665ad%3acrx.default; ys-cq-siteadmin-tree=o%3Awidth%3Dn%253A240%5EselectedPath%3Ds%253A/content ]
C-0-#000824 -> [ ]
```

A instância do AEM responde com o conteúdo do arquivo `test.html`:

```shell
S-0-#000000 -> [HTTP/1.1 200 OK ]
S-0-#000017 -> [Connection: Keep-Alive ]
S-0-#000041 -> [Server: Day-Servlet-Engine/4.1.24  ]
S-0-#000077 -> [Content-Type: text/html;charset=utf-8 ]
S-0-#000116 -> [Content-Length: 104 ]
S-0-#000137 -> [Date: Mon, 16 Jul 2012 11:23:38 GMT ]
S-0-#000174 -> [Last-Modified: Mon, 16 Jul 2012 11:19:27 GMT ]
S-0-#000220 -> [ ]
S-0-#000222 -> [<html>]
S-0-#000229 -> [<head>]
S-0-#000236 -> [    <title>Test</title>]
S-0-#000260 -> [</head> ]
S-0-#000269 -> [<body>]
S-0-#000276 -> [ Test<br>]
S-0-#000286 -> [    <img src="test.jpg">]
S-0-#000311 -> [</body>]
S-0-#000319 -> [</html>]
```

### Usos do servidor proxy {#uses-of-the-proxy-server}

Os cenários a seguir ilustram algumas das finalidades para as quais o Servidor Proxy pode ser usado:

**Verificar se há cookies e seus valores**

O exemplo de entrada de log a seguir mostra todos os cookies e seus valores enviados pelo cliente na sexta conexão aberta desde que o proxy foi iniciado:

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**Verificação de Cabeçalhos e seus Valores**

O exemplo de entrada de log a seguir mostra que o servidor pode fazer uma conexão keep-alive e o cabeçalho de comprimento de conteúdo foi definido corretamente:

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**Verificando se a opção Keep-Alive funciona**

Keep-alive é um recurso do HTTP que permite que um cliente reutilize a conexão TCP com o servidor para fazer várias solicitações (para o código da página, imagens, folhas de estilos e assim por diante). Sem o keep-alive, o cliente precisa estabelecer uma nova conexão para cada solicitação.

Para verificar se o keep-alive funciona:

* Inicie o servidor proxy.
* Solicitar uma página.
* Se o keep-alive estiver funcionando, o contador de conexões nunca deverá ultrapassar 5 a 10 conexões.
* Se o keep-alive não estiver funcionando, o contador de conexões aumentará rapidamente.

**Localizando solicitações perdidas**

Se você perder solicitações em uma configuração de servidor complexa, por exemplo, com um firewall e um Dispatcher, poderá usar o servidor proxy para descobrir onde a solicitação foi perdida. Se houver um firewall:

* Iniciar um proxy antes de um firewall
* Iniciar outro proxy após um firewall
* Use-os para ver até que ponto as solicitações estão chegando.

**Solicitações Deslocadas**

Se você tiver solicitações de alteração de vez em quando:

* Inicie o proxy.
* Aguarde ou grave o log de acesso em um arquivo com cada entrada com um carimbo de data e hora.
* Quando a solicitação for interrompida, você poderá ver quantas conexões estavam abertas e qual solicitação está causando problemas.

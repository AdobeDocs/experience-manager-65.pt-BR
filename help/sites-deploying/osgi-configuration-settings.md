---
title: Configurações do OSGi
description: Este artigo detalha as definições de configuração do OSGi (listadas de acordo com o pacote) que são relevantes para a implementação do projeto. A lista serve de orientação e não é exaustiva.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '3360'
ht-degree: 0%

---

# Configurações do OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) é um elemento fundamental na pilha tecnológica do AEM. É usado para controlar os pacotes compostos de AEM e sua configuração.

OSGi &quot;*O fornece as primitivas padronizadas que permitem que os aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados*&quot;.

Essa funcionalidade permite o fácil gerenciamento de pacotes, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são tratadas automaticamente. Cada componente OSGi (consulte a [Especificação OSGi](https://docs.osgi.org/specification/)) está contido em um dos vários pacotes. Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses pacotes; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

As seguintes configurações de OSGi (listadas de acordo com o pacote) são relevantes para a implementação do projeto. Nem todas as configurações listadas precisam ser ajustadas, algumas são mencionadas para ajudar você a entender como o AEM opera.

>[!CAUTION]
>
>A lista destina-se a servir de orientação e não é exaustiva. Nem todos os pacotes estão listados, nem todos os parâmetros para alguns dos pacotes que estão.
>
>A configuração necessária varia de projeto para projeto.
>
>Consulte o console da Web para obter valores usados e informações detalhadas sobre parâmetros.

>[!NOTE]
>
>A ferramenta de comparação da configuração do OSGi, parte da [Ferramentas AEM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html), pode ser usado para listar as configurações OSGi padrão.

>[!NOTE]
>
>Outros pacotes podem ser necessários para áreas específicas de funcionalidade dentro do AEM. Nesses casos, os detalhes da configuração podem ser encontrados na página relacionada à funcionalidade apropriada.

**Ouvinte de Evento de Replicação AEM** Configurar:

* A variável **Modos de execução**, em que os eventos de replicação são distribuídos aos ouvintes. Por exemplo, se definido como autor, é o sistema que &quot;inicia&quot; a replicação.

* Adicionar o modo de execução **publicar** se o código do projeto processar eventos de replicação (replicação reversa) em um ambiente de publicação. Por exemplo, quando o Dispatcher é usado para liberar do ambiente de publicação ou quando ocorre a replicação padrão para outras instâncias de publicação.

**Ouvinte de alteração do repositório AEM** Configurar:

* A variável **Caminhos**, locais para acompanhar eventos do repositório prontos para distribuição.

**Repositório do cliente do CRX Sling** Configurar o acesso ao repositório de conteúdo subjacente.

* A variável **Senha do administrador** deve ser alterado após a instalação para garantir que o [segurança](/help/sites-administering/security-checklist.md) da sua instância.
* Outras alterações não devem ser necessárias e deve-se tomar cuidado, pois podem afetar o acesso ao repositório.

**Console de gerenciamento do Apache Felix OSGi** Configurar:

* **Plug-ins**, os itens de navegação principais (plug-ins do console) estarão disponíveis na **Console de gerenciamento Web Apache Felix** como itens de menu de nível superior. Desative as que não forem necessárias, pois cada uma exige espaço e recursos.

>[!CAUTION]
>
>Certifique-se de configurar o seguinte:
>
>**Nome do usuário** e **Senha**, as credenciais para acessar o próprio Console de gerenciamento da Web Apache Felix.
>A senha deve ser alterada após a instalação inicial para garantir que o [segurança](/help/sites-administering/security-checklist.md) da sua instância.

>[!NOTE]
>
>Essa configuração deve ser feita usando o Felix Console, pois é necessária na inicialização - antes que o repositório esteja disponível.

**Agente de dados de solicitação personalizável do Apache Sling** Configurar:

* **Nome do logger** e **Formato do Log** para configurar a localização e o formato do registro de solicitações e acessos (padrão: `request.log`). Esse arquivo de log é essencial ao analisar o desempenho ou a funcionalidade de depuração relacionada à cadeia da Web. Ele está emparelhado com o [Logger de solicitação do Apache Sling](#apacheslingrequestlogger).

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) e [Log do Sling](https://sling.apache.org/documentation/development/logging.html).

**Pool de threads de evento do Apache Sling** Configurar:

* **Tamanho mínimo do pool** e **Tamanho máximo do pool**, o tamanho do pool usado para armazenar threads de eventos.

* **Tamanho da fila**, o tamanho máximo da fila de threads se o pool estiver esgotado.
O valor recomendado é `-1` porque define a fila como ilimitada. Se um limite for definido, poderão ocorrer perdas quando ele for excedido.

* A alteração dessas configurações pode ajudar no desempenho em cenários com um alto número de eventos. Por exemplo, uso intenso de DAM do AEM ou Fluxo de trabalho.
* Os valores específicos para o seu cenário devem ser estabelecidos por meio de testes.
* Essas configurações podem afetar o desempenho da sua instância, portanto, não as altere sem motivo e devida consideração.

**Apache Sling GET Servlet** Configure alguns aspectos da renderização:

* **Índice automático** para ativar/desativar a renderização de diretório para navegação.
* **Ativar** (ou desativar) representações padrão, como **HTML**, **Texto sem formatação**, **JSON** ou **XML**.
Não desative o JSON.

>[!NOTE]
>
>Essa configuração é definida automaticamente para instâncias de produção se você executar o AEM no [Modo de produção pronto](/help/sites-administering/production-ready.md).

**Manipulador de JavaScript do Apache Sling** Configure as definições para a compilação de arquivos .java como scripts (servlets).

Certas configurações podem afetar o desempenho. Desative essas configurações sempre que possível, especialmente para uma instância de produção.

* **VM de origem** e **VM de destino**, defina a versão do JDK usada como a JVM de tempo de execução

* para instâncias de produção:

   * disable **Gerar informações de depuração**

**Instalador do Apache Sling JCR** Esses parâmetros provavelmente não precisam de configuração, mas podem ser úteis ao desenvolver ou depurar. Por exemplo, as pastas de instalação podem ser úteis para fazer check-in ou check-out ou para criar um pacote.

* **Expressão regular de nome das pastas de instalação** e **Profundidade máxima da hierarquia de pastas de instalação** - especifique onde e em qual profundidade as pastas do repositório são pesquisadas em busca de recursos a serem instalados. Quando um curinga é usado (como em .&#42;/install) todas as correspondências apropriadas são pesquisadas, por exemplo, `/libs/sling/install` e `/libs/cq/core/install`.

* **Caminho de pesquisa**, lista de caminhos em que o jcrinstall procura recursos a serem instalados, juntamente com um número indicando o fator de ponderação desse caminho.

**Manipulador de eventos de trabalho do Apache Sling** Configure parâmetros que gerenciam o agendamento de trabalhos:

* **Intervalo de repetição**, **Máximo de tentativas**, **Máximo de Trabalhos Paralelos**, **Confirmar tempo de espera**, entre outros.

* Alterar essas configurações pode melhorar o desempenho em cenários com um alto número de trabalhos; por exemplo, uso intenso de DAM e Workflows de AEM.
* Os valores específicos para o seu cenário devem ser estabelecidos por meio de testes.
* Não altere essas configurações sem motivo; altere somente após a devida consideração.

**Manipulador de script JSP do Apache Sling** Configure as definições relevantes de desempenho para o manipulador de script JSP. Para melhorar o desempenho, você deve desativar o máximo possível.

Em particular para instâncias de produção:

* disable **Gerar informações de depuração**
* disable **Manter Java™ gerado**
* disable **Conteúdo mapeado**
* disable **Exibir fragmentos de origem**

>[!NOTE]
>
>Essa configuração é definida automaticamente para instâncias de produção se você executar o AEM no [Modo de produção pronto](/help/sites-administering/production-ready.md).

**Configuração de registro do Apache Sling** Configurar:

* **Nível de registro** e **Arquivo de log**, para definir a localização e o nível de log da configuração de log central (error.log). O nível pode ser definido como um de `DEBUG`, `INFO`, `WARN`, `ERROR`, e `FATAL`.

* **Número de arquivos de log** e **Limite do arquivo de log** para definir o tamanho e a rotação da versão do arquivo de log.

* **Padrão de mensagem** define o formato das mensagens de log.

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md#global-logging) e [Log do Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuração do logger de log do Apache Sling (configuração de fábrica)** Configurar:

* **Nível de registro**, **Arquivo de log** e **Formato da mensagem** para definir detalhes do arquivo de log e mensagens.

* **Logger** para definir a categoria; por exemplo, registre apenas para com.day.cq.

* Ao usar **Configurações de fábrica**, qualquer número de configurações adicionais pode ser adicionado para atender aos vários níveis de log e categorias necessários.
* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens de TRACE para um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, para ter mensagens sobre um serviço específico registrado em um arquivo de log individual para facilitar o monitoramento.

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) e [Log do Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuração do gravador de log do Apache Sling (configuração de fábrica)** Configurar:

* **Arquivo de log** para definir a existência de um arquivo de log.
* **Número de arquivos de log** para definir a rotação da versão.

* O gravador pode ser usado por um **Configuração do logger de log do Apache Sling** configuração.

* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens de TRACE para um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, para ter mensagens sobre um serviço específico registrado em um arquivo de log individual para facilitar o monitoramento.

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) e [Log do Sling](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Main Servlet** Configurar:

* **Número de chamadas por solicitação** e **Profundidade da recursão** para proteger seu sistema contra recursão infinita e chamadas de script excessivas.

**Serviço de tipo MIME do Apache Sling** Configurar:

* **Tipos MIME** para adicionar tipos exigidos pelo projeto ao sistema. Isso permite uma `GET` solicitação em um arquivo para definir o cabeçalho de tipo de conteúdo correto para vincular o tipo de arquivo e o aplicativo.

**Filtro referenciador do Apache Sling** Para resolver problemas de segurança conhecidos com a falsificação de solicitação entre sites (CSRF) no CRX WebDAV e no Apache Sling, você deve configurar o filtro Referenciador.

O serviço de filtro referenciador é um serviço OSGi que permite configurar:

* quais métodos http devem ser filtrados
* se um cabeçalho de referenciador vazio é permitido
* e uma lista de servidores permitidos além do host do servidor.

Consulte a [Lista de verificação de segurança - Problemas com a falsificação da solicitação entre sites](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obter mais detalhes.

>[!NOTE]
>
>O Filtro referenciador do Apache Sling depende da instalação de um pacote de correção rápida.

**Logger de solicitação do Apache Sling** Configurar:

* vários parâmetros para definir como as solicitações são registradas.
* **Habilitar Log de Solicitação**, para ativar ou desativar.

* **Habilitar Log de Acesso**, para ativar ou desativar.

Emparelhado com o [Agente de dados de solicitação personalizável do Apache Sling](#apacheslingcustomizablerequestdatalogger).

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) e [Log do Sling](https://sling.apache.org/documentation/development/logging.html).

**Fábrica do Apache Sling Resource Resolver** Configure os aspectos centrais da resolução de recursos do Sling:

* **Caminhos de pesquisa de recursos**, adicione qualquer caminho específico do projeto (mas não remova `/libs` ou `/apps`).

* **URLs virtuais** para definir os mapeamentos de URL personalizado.

* **Mapeamentos de URL** para definir aliases. Por exemplo, de `/content` para `/`.

* **Localização do mapeamento**, a configuração do mapeador externalizada em `/etc/map`.

* Use a instalação local (por exemplo, use `https://localhost:4502/system/console/jcrresolver`) para determinar qual Resource Resolver está ativo.

Consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Configure essas opções no repositório.
>
>Caso contrário, as alterações feitas no **Mapeamentos de URL** o uso do console Felix pode ser substituído pelo AEM na próxima inicialização.

**Resolvedor de Apache Sling Servlet/Script e Manipulador de erros** O Sling Servlet e o Script Resolver têm várias tarefas:

1. É usado como o `ServletResolver` para selecionar o Servlet ou Script que chamará para lidar com a solicitação.

1. Atua como o `SlingScriptResolver`.

1. Ele gerencia o tratamento de erros implementando o `ErrorHandler` usando o mesmo algoritmo para selecionar servlets e scripts de tratamento de erros que são usados para resolver servlets e scripts de processamento de solicitações.

Vários parâmetros podem ser definidos, incluindo:

* **Caminhos de execução** - Lista os caminhos para procurar scripts executáveis. Ao configurar caminhos específicos, você pode limitar quais scripts podem ser executados. Se nenhum caminho estiver configurado, o padrão será usado ( `/` = root), permitindo a execução de todos os scripts.
Se um valor de caminho configurado terminar com uma barra, a subárvore inteira será pesquisada. Sem essa barra à direita, o script só é executado se for uma correspondência exata.

* **Script de usuário** - Essa propriedade opcional pode especificar a conta de usuário do repositório usada para ler os scripts. Se nenhuma conta for especificada, a variável `admin` é usado por padrão.

* **Extensões padrão** - A lista de extensões para as quais o comportamento padrão é usado. O último segmento de caminho do tipo de recurso pode ser usado como o nome do script.

**Configuração de proxy de componentes HTTP do Apache** - A configuração de proxy para todo o código usando o cliente HTTP do Apache, usada quando um HTTP é criado. Por exemplo, sobre replicação.

Ao criar uma configuração, não altere a configuração de fábrica. Em vez disso, crie uma configuração de fábrica para esse componente usando o gerenciador de configurações disponível aqui: **https://localhost:4502/system/console/configMgr/**. A configuração de proxy está disponível em **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>No AEM 6.0 e versões anteriores, o proxy era configurado no Day Commons HTTP Client. A partir do AEM 6.1 e versões posteriores, a configuração de proxy foi movida para a &quot;Configuração de proxy de componentes HTTP do Apache&quot; em vez da configuração &quot;Day Commons HTTP Client&quot;.

**Day CQ Antispam** Configure o serviço antisspam (Akismet) usado. Esse recurso exige que você registre o seguinte:

* **Provedor**
* **Chave de API**
* **URL registrado**

**Gerenciador de biblioteca de HTML do Adobe Granite** Configure para controlar o manuseio de bibliotecas de clientes (css ou js) incluindo, por exemplo, como a estrutura subjacente é vista.

* Para instâncias de produção:

   * habilitar **Minify** (para remover CRLF e caracteres de espaço em branco).
   * habilitar **Gzip** (para permitir que os arquivos sejam compactados e acessados com uma solicitação).
   * disable **Depurar**
   * disable **Tempo**

* Para o desenvolvimento de JS (especialmente quando há firebugging/depuração):

   * disable **Minify**
   * habilitar **Depurar** para separar os arquivos para depuração e usar com o fire bug.
   * habilitar **Tempo** se estiver interessado em tempo útil.
   * habilitar **Depurar** para ver as mensagens de log do console JS.

>[!CAUTION]
>
>Ao alterar a configuração de **Minify** ou **Gzip**, exclua o conteúdo do cache clientlibs. Consulte [Artigo da knowledge base](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html) para obter detalhes.

>[!NOTE]
>
>Essa configuração é definida automaticamente para instâncias de produção se você executar o AEM no [Modo de produção pronto](/help/sites-administering/production-ready.md).

**Manipulador de autenticação de cabeçalho HTTP CQ diário** Configurações em todo o sistema para o método de autenticação básico da solicitação HTTP.

Ao usar [grupos de usuários fechados](/help/sites-administering/cug.md), você pode configurar, entre outros, o seguinte:

* **Território HTTP**
* A variável **Página de logon padrão**

**Serviço Day CQ Verificador de links** Marque e, se necessário, configure:

* **Período do Agendador** para definir o intervalo em que os links externos devem ser verificados automaticamente.

* Marcar **Intervalo de Tolerância de Link Incorreto** para o período após o qual um link externo malsucedido é considerado ruim.
* **Padrões de substituição de verificação de link**, para definir os caminhos que serão excluídos da verificação de links.

**Tarefa do Verificador de Links CQ Diário** Defina as configurações de uma única tarefa do verificador de links (uma tarefa que verifica um link externo):

* Verifique os intervalos definidos em **Intervalo de teste de link correto** e **Intervalo de teste de link incorreto**

* Os vários parâmetros relacionados a proxies para acesso à Internet e NTLM necessários para acesso externo ao verificar um link.

**Serviço de email Day CQ** Configurar o nome do host e os detalhes de acesso do servidor de e-mail. Consulte a seção Configurando o Serviço de E-mail.

**Informativo MCM CQ do dia** Defina as várias configurações usadas com o informativo.

**Day CQ Root Mapping** Configurar:

* **Caminho de destino** para definir onde uma solicitação de &quot; `/`&quot; é redirecionado para.

Há duas interfaces do usuário disponíveis no AEM:

* a interface habilitada para toque é a interface padrão
* e a interface clássica obsoleta ainda está totalmente operacional

Usando o mapeamento de raiz AEM, é possível configurar a interface do usuário que você deseja ter como padrão para sua instância:

* Para ter a interface habilitada para toque como a interface padrão, **Caminho de destino** A deve apontar para o seguinte:

  ```shell
     /projects.html
  ```

* Para ter a interface clássica como padrão, a variável **Caminho de destino** A deve apontar para o seguinte:

  ```shell
     /welcome.html
  ```

>[!NOTE]
>
>Em uma instalação padrão, a interface otimizada para toque é a interface padrão.

**Manipulador de autenticação SSO do Adobe Granite** - Configurar detalhes de SSO (Logon único). Esses detalhes geralmente são necessários nas configurações do autor corporativo, geralmente com LDAP.

Várias propriedades de configuração estão disponíveis:

* **Caminho**
O caminho para o qual este manipulador de autenticação está ativo. Se esse parâmetro for deixado em branco, o manipulador de autenticação será desativado. Por exemplo, o caminho / faz com que o manipulador de autenticação seja usado para todo o repositório.

* **Classificação do serviço**
O valor de Classificação do OSGi Framework Service é usado para indicar a ordem usada para chamar esse serviço. Esse valor é um `int` valor em que valores mais altos designam maior precedência.
O valor padrão é `0`.

* **Nomes do cabeçalho**
Os nomes dos cabeçalhos que podem conter uma ID de usuário.

* **Nomes de cookies**
Os nomes dos cookies que podem conter uma ID de usuário.

* **Nomes de Parâmetros**
Os nomes dos parâmetros de solicitação que podem fornecer a ID do usuário.

* **Mapa do usuário**
Para usuários selecionados, o nome de usuário extraído da solicitação HTTP pode ser substituído por outro no objeto de credenciais. O mapeamento é definido aqui. Se o nome do usuário `admin` for exibido em ambos os lados do mapa, o mapeamento será ignorado. O caractere &quot;=&quot; deve ser escapado com um &quot;\&quot; à esquerda.

* **Formato**
Indica o formato em que a ID de usuário é fornecida. Uso:

   * `Basic` se a ID do usuário estiver codificada no formato de Autenticação Básica HTTP
   * `AsIs` se a ID do usuário for fornecida em texto sem formatação ou qualquer valor de expressão regular aplicada, deverá ser usado como está ou qualquer expressão regular

**Filtro de depuração WCM CQ diário** Isso é útil ao desenvolver, pois permite o uso de sufixos como ?debug=layout ao acessar uma página. Por exemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout fornece informações de layout que podem ser de interesse do desenvolvedor.

* Para garantir desempenho e segurança, desative em instâncias de produção.

**Filtro WCM CQ do dia** Configurar:

* **Modo WCM** para definir o modo padrão.
* Em uma instância de autor, esse modo pode ser `edit`, `disable,preview`ou `analytics`.
Os outros modos podem ser acessados pelo sidekick ou pelo sufixo `?wcmmode=disabled` O pode ser usado para emular um ambiente de produção.

* Em uma instância de publicação, esse modo deve ser definido como `disabled` para garantir que nenhum outro modo esteja acessível.

>[!NOTE]
>
>Essa configuração é definida automaticamente para instâncias de produção se você executar o AEM no [Modo de produção pronto](/help/sites-administering/production-ready.md).

**Configurador do verificador de link WCM CQ diário** Configurar:

* **Lista de configurações de regravação** para especificar uma lista de locais para configurações do verificador de links baseados em conteúdo. As configurações podem ser baseadas no modo de execução. Esse fato é importante para distinguir entre ambientes de autor e publicação, pois as configurações do verificador de links podem ser diferentes.

**Fábrica do gerenciador de página do WCM CQ do dia** Configurar:

* **Verificação de ativação da subárvore de páginas** para um usuário (sem permissões de replicação) excluir ou mover páginas (mesmo se as páginas não estiverem ativadas).

**Processador de página WCM CQ diário** Configurar:

* **Caminhos**, uma lista de locais onde o sistema escuta as modificações de página antes de acionar um `jcr:Event`.

**Rastreador de impressões de página do Adobe** Para uma instância do autor, configure como o seguinte:

* **sling.auth.requirements**: defina o valor dessa propriedade como `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Essa configuração permite solicitações anônimas para o serviço de rastreamento.

>[!NOTE]
>
>Consulte [Impressões de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obter mais informações.

**Estatísticas de página WCM CQ do dia** Para uma instância de publicação, configure:

* **URL para enviar dados** para configurar o URL usado para rastrear estatísticas de página (é essencial se uma solicitação do rastreador passar pelo Dispatcher); por exemplo, o padrão é `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script de rastreamento habilitado** para ativar ( `true`) ou desativar ( `false`) a inclusão do script de rastreamento nas páginas. O valor padrão é `false`.

>[!NOTE]
>
>Consulte [Impressões de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obter mais informações.

**Gerenciador de versão Day CQ WCM** Controle se e como as versões são gerenciadas em seu sistema:

* **Criar versão na ativação**, ativado em uma instalação padrão
* **Ativar limpeza**

* **Limpar caminhos**, os caminhos que uma ação de pesquisa pesquisa pesquisa.
* **Caminhos de controle de versão implícitos**, os caminhos em que o controle de versão implícito está ativo.

* **Idade máxima da versão**, a idade máxima (em dias) de uma versão

* **Número máximo de versões**, o número máximo de versões a serem mantidas

Consulte [Limpeza de versão](/help/sites-deploying/version-purging.md) para obter mais informações.

**Serviço de notificação por email do fluxo de trabalho do Day CQ** Defina as configurações de email para notificações enviadas por um fluxo de trabalho.

**Fábrica de analisador de HTML de reescrita CQ**

Controla o Analisador de HTML para o reescritor CQ.

* **Tags adicionais a processar** - Você pode adicionar ou remover tags HTML a serem processadas pelo analisador. Por padrão, as seguintes tags são processadas: A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD.
* **Preservar Camel Case** - Por padrão, o analisador de HTML converte atributos em caso de camelo (por exemplo, `eBay`) para letras minúsculas (por exemplo, `ebay`). Você pode desativar essa configuração para preservar os atributos de camel case. Essa configuração é útil ao usar estruturas de front-end, como o Angular 2.

**Pool de Conexões JDBC do Day Commons** Configure o acesso a um banco de dados externo que está sendo usado como uma fonte de conteúdo.

Uma configuração de fábrica, para que várias instâncias possam ser configuradas.

**Reescrita CDN** A comunicação entre o AEM e uma CDN deve ser assegurada para que os ativos/binários sejam entregues a um usuário final de forma segura. Esse processo envolve as duas tarefas a seguir:

* Acessar o recurso do AEM por meio da CDN na primeira vez (ou depois que ele expirou no cache).
* Acessar o recurso em cache na CDN com segurança. Depois que o recurso é armazenado em cache no CDN, a solicitação não vai para o AEM e todos os usuários que têm acesso a esse recurso em devem ser fornecidos pelo CDN.

O AEM fornece um reescritor para reescrever URLs de ativos internos em URLs CDN externos. Ele substitui links a serem transmitidos para o CDN, incluindo uma assinatura JWS e um tempo de expiração para permitir que o ativo seja acessado com segurança. Esse recurso deve ser usado em instâncias de autor.

O fluxo total é o seguinte:

1. O usuário se autentica com AEM e solicita uma página com ativos.
1. A página solicitada contém um ativo semelhante a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. O Rewriter transforma o link em um URL CDN contendo uma Assinatura JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. O navegador do usuário encaminha a solicitação de ativo para o servidor CDN
1. O CDN deve ser configurado para encaminhar a solicitação ao AEM junto com o `cdn_sign` parâmetro.
1. Um Manipulador de autenticação valida a `cdn_sign` e retorna o ativo ao CDN, que é então entregue ao usuário

O fluxo entre o navegador do usuário, o CDN e o AEM pode ser visualizado da seguinte maneira.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Esse recurso só é ativado para instâncias de autor AEM.

**CDNConfigServiceImpl** Fornece configurações de CDN

O recurso de reescrita CDN pode ser habilitado fornecendo **Nome de domínio de distribuição CDN** na configuração para com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

O serviço também contém outras opções de configuração, como ativar/desativar a reescrita de CDN, prefixos de caminho para os quais a reescrita de CDN é executada, valores TTL e protocolo (HTTP ou HTTPS).

**CDNRewriter** Um reescritor para reescrever URLs de imagens internas em URLs CDN

A variável **Atributos da tag** O valor em com.adobe.cq.cdn.rewriter.impl.CDNRewriter pode ser definido para que somente os links de imagem seletiva sejam regravados.

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
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3360'
ht-degree: 0%

---

# Configurações do OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia do AEM. É usado para controlar os pacotes compostos de AEM e sua configuração.

O OSGi &quot;*fornece os primitivos padronizados que permitem que os aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados &quot;*&quot;.

Essa funcionalidade permite o fácil gerenciamento de pacotes, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são tratadas automaticamente. Cada componente OSGi (consulte a [Especificação OSGi](https://docs.osgi.org/specification/)) está contido em um dos vários pacotes. Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses pacotes; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

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
>A ferramenta de comparação da configuração do OSGi, parte das [Ferramentas do AEM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html?lang=pt-BR), pode ser usada para listar as configurações padrão do OSGi.

>[!NOTE]
>
>Outros pacotes podem ser necessários para áreas específicas de funcionalidade dentro do AEM. Nesses casos, os detalhes da configuração podem ser encontrados na página relacionada à funcionalidade apropriada.

**Ouvinte de Eventos de Replicação do AEM** Configurar:

* Os **Modos de Execução**, nos quais os eventos de replicação são distribuídos aos ouvintes. Por exemplo, se definido como autor, é o sistema que &quot;inicia&quot; a replicação.

* Adicione o modo de execução **publicar** se o código do projeto processar eventos de replicação (replicação reversa) em um ambiente de publicação. Por exemplo, quando o Dispatcher é usado para liberar do ambiente de publicação ou quando ocorre a replicação padrão para outras instâncias de publicação.

**Ouvinte de alteração do repositório AEM** Configurar:

* Os **Caminhos**, locais para ouvir eventos do repositório prontos para distribuição.

**Repositório do cliente do CRX Sling** Configure o acesso ao repositório de conteúdo subjacente.

* A **Senha do Administrador** deve ser alterada após a instalação para garantir a [segurança](/help/sites-administering/security-checklist.md) da sua instância.
* Outras alterações não devem ser necessárias e deve-se tomar cuidado, pois podem afetar o acesso ao repositório.

**Console de Gerenciamento OSGi do Apache Felix** Configurar:

* **Plug-ins**, os itens de navegação principais (plug-ins de console) a serem disponibilizados no **Console de Gerenciamento Web do Apache Felix** como itens de menu de nível superior. Desative as que não forem necessárias, pois cada uma exige espaço e recursos.

>[!CAUTION]
>
>Certifique-se de configurar o seguinte:
>
>**Nome do Usuário** e **Senha**, as credenciais para acessar o próprio Console de Gerenciamento da Web do Apache Felix.
>A senha deve ser alterada após a instalação inicial para garantir a [segurança](/help/sites-administering/security-checklist.md) de sua instância.

>[!NOTE]
>
>Essa configuração deve ser feita usando o Felix Console, pois é necessária na inicialização - antes que o repositório esteja disponível.

**Logger De Dados De Solicitação Personalizável Do Apache Sling** Configure:

* **Nome do Agente** e **Formato do Log** para configurar o local e o formato do log de solicitações e acessos (padrão: `request.log`). Esse arquivo de log é essencial ao analisar o desempenho ou a funcionalidade de depuração relacionada à cadeia da Web. Ele está emparelhado com o [Logger de solicitação do Apache Sling](#apacheslingrequestlogger).

Consulte [Log de AEM](/help/sites-deploying/configure-logging.md) e [Log de Sling](https://sling.apache.org/documentation/development/logging.html).

**Pool de Threads de Evento do Apache Sling** Configurar:

* **Tamanho Mínimo do Pool** e **Tamanho Máximo do Pool**, o tamanho do pool usado para conter threads de evento.

* **Tamanho da Fila**, o tamanho máximo da fila de threads se o pool estiver esgotado.
O valor recomendado é `-1` porque ele define a fila como ilimitada. Se um limite for definido, poderão ocorrer perdas quando ele for excedido.

* A alteração dessas configurações pode ajudar no desempenho em cenários com um alto número de eventos. Por exemplo, uso intenso de DAM do AEM ou Fluxo de trabalho.
* Os valores específicos para o seu cenário devem ser estabelecidos por meio de testes.
* Essas configurações podem afetar o desempenho da sua instância, portanto, não as altere sem motivo e devida consideração.

**Apache Sling GET Servlet** Configure alguns aspectos da renderização:

* **Índice Automático** para habilitar/desabilitar a renderização de diretório para navegação.
* **Habilitar** (ou desabilitar) representações padrão, como **HTML**, **Texto sem Formatação**, **JSON** ou **XML**.
Não desative o JSON.

>[!NOTE]
>
>Essa configuração é definida automaticamente para instâncias de produção se você executar o AEM no [Modo de Produção Pronta](/help/sites-administering/production-ready.md).

**Apache Sling JavaScript Handler** Defina as configurações para a compilação de arquivos .java como scripts (servlets).

Certas configurações podem afetar o desempenho. Desative essas configurações sempre que possível, especialmente para uma instância de produção.

* **VM do Source** e **VM de Destino**, defina a versão do JDK usada como JVM de tempo de execução

* para instâncias de produção:

   * desabilitar **Gerar Informações de Depuração**

**Instalador do Apache Sling JCR** Esses parâmetros provavelmente não precisam de configuração, mas podem ser úteis ao desenvolver ou depurar. Por exemplo, as pastas de instalação podem ser úteis para fazer check-in ou check-out ou para criar um pacote.

* **Nome das pastas de instalação regexp** e **Profundidade máxima da hierarquia de pastas de instalação** - especifique onde e em que profundidade as pastas do repositório serão pesquisadas em busca de recursos a serem instalados. Quando um curinga é usado (como em .&#42;/instalar) todas as correspondências apropriadas são pesquisadas, por exemplo, `/libs/sling/install` e `/libs/cq/core/install`.

* **Caminho de pesquisa**, lista de caminhos em que o jcrinstall procura recursos a serem instalados, juntamente com um número que indica o fator de ponderação desse caminho.

**Manipulador de eventos de trabalho do Apache Sling** Configure os parâmetros que gerenciam o agendamento de trabalhos:

* **Intervalo de novas tentativas**, **Máximo de novas tentativas**, **Máximo de trabalhos paralelos**, **Tempo de espera de confirmação**, entre outros.

* Alterar essas configurações pode melhorar o desempenho em cenários com um alto número de trabalhos; por exemplo, uso intenso de DAM e Workflows de AEM.
* Os valores específicos para o seu cenário devem ser estabelecidos por meio de testes.
* Não altere essas configurações sem motivo; altere somente após a devida consideração.

**Manipulador de script JSP do Apache Sling** Defina configurações relevantes para o desempenho do manipulador de script JSP. Para melhorar o desempenho, você deve desativar o máximo possível.

Em particular para instâncias de produção:

* desabilitar **Gerar Informações de Depuração**
* desabilitar **Manter Java™** Gerado
* desabilitar **Conteúdo Mapeado**
* desabilitar **Exibir Fragmentos do Source**

>[!NOTE]
>
>Essa configuração é definida automaticamente para instâncias de produção se você executar o AEM no [Modo de Produção Pronta](/help/sites-administering/production-ready.md).

**Configuração de log do Apache Sling** Configurar:

* **Nível de Log** e **Arquivo de Log**, para definir o local e o nível de log da configuração de log central (error.log). O nível pode ser definido como `DEBUG`, `INFO`, `WARN`, `ERROR` e `FATAL`.

* **Número de Arquivos de Log** e **Limite de Arquivos de Log** para definir o tamanho e a rotação de versão do arquivo de log.

* **Padrão de Mensagem** define o formato das mensagens de log.

Consulte [Log de AEM](/help/sites-deploying/configure-logging.md#global-logging) e [Log de Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuração do Agente de Log do Apache Sling (Configuração de Fábrica)** Configurar:

* **Nível de Log**, **Arquivo de Log** e **Formato da Mensagem** para definir detalhes do arquivo de log e mensagens.

* **Logger** para definir a categoria; por exemplo, registrar apenas para com.day.cq.

* Ao usar as **Configurações de Fábrica**, qualquer número de configurações adicionais pode ser adicionado para atender aos vários níveis de log e categorias necessários.
* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens de TRACE para um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, para ter mensagens sobre um serviço específico registrado em um arquivo de log individual para facilitar o monitoramento.

Consulte [Log de AEM](/help/sites-deploying/configure-logging.md) e [Log de Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuração do Gravador de Log do Apache Sling (Configuração de Fábrica)** Configurar:

* **Arquivo de log** para definir a existência de um arquivo de log.
* **Número de Arquivos de Log** para definir a rotação de versão.

* O gravador pode ser usado por uma configuração **Apache Sling Logging Logger Configuration**.

* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens de TRACE para um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, para ter mensagens sobre um serviço específico registrado em um arquivo de log individual para facilitar o monitoramento.

Consulte [Log de AEM](/help/sites-deploying/configure-logging.md) e [Log de Sling](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Main Servlet** Configurar:

* **Número de Chamadas por Solicitação** e **Profundidade da Recursão** para proteger o sistema contra recursão infinita e chamadas de script em excesso.

**Serviço de tipo MIME do Apache Sling** Configurar:

* **Tipos MIME** para adicionar tipos que são exigidos pelo seu projeto ao sistema. Isso permite que uma solicitação `GET` em um arquivo defina o cabeçalho de tipo de conteúdo correto para vincular o tipo de arquivo e o aplicativo.

**Filtro do referenciador Apache Sling** Para resolver problemas de segurança conhecidos com o CSRF (Falsificação de solicitação entre sites) no CRX WebDAV e Apache Sling, você deve configurar o filtro Referenciador.

O serviço de filtro referenciador é um serviço OSGi que permite configurar:

* quais métodos http devem ser filtrados
* se um cabeçalho de referenciador vazio é permitido
* e uma lista de servidores permitidos além do host do servidor.

Consulte a [Lista de Verificação de Segurança - Problemas com a Falsificação de Solicitação Entre Sites](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obter mais detalhes.

>[!NOTE]
>
>O Filtro referenciador do Apache Sling depende da instalação de um pacote de correção rápida.

**Logger de solicitação do Apache Sling** Configurar:

* vários parâmetros para definir como as solicitações são registradas.
* **Habilitar Log de Solicitação**, para habilitar ou desabilitar.

* **Habilitar Log de Acesso**, para habilitar ou desabilitar.

Emparelhado com o [Logger de dados de solicitação personalizável do Apache Sling](#apacheslingcustomizablerequestdatalogger).

Consulte [Log de AEM](/help/sites-deploying/configure-logging.md) e [Log de Sling](https://sling.apache.org/documentation/development/logging.html).

**Fábrica do Apache Sling Resource Resolver** Configure os aspectos centrais da resolução de recursos Sling:

* **Caminhos de Pesquisa de Recursos**, adicione quaisquer caminhos específicos do projeto (mas não remova `/libs` ou `/apps`).

* **URLs virtuais** para definir seus mapeamentos de URLs personalizados.

* **Mapeamentos de URL** para definir qualquer alias. Por exemplo, de `/content` a `/`.

* **Localização do Mapeamento**, a configuração do mapeador foi externalizada em `/etc/map`.

* Use sua instalação local (por exemplo, use o `https://localhost:4502/system/console/jcrresolver`) para determinar qual Resource Resolver está ativo.

Consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Configure essas opções no repositório.
>
>Caso contrário, as alterações feitas em **Mapeamentos de URL** usando o console Felix poderão ser substituídas pelo AEM na próxima inicialização.

**Apache Sling Servlet/Script Resolver e Error Handler** O Sling Servlet e o Script Resolver têm várias tarefas:

1. É usado como `ServletResolver` para selecionar o Servlet ou Script que chamará para lidar com a solicitação.

1. Ele age como o `SlingScriptResolver`.

1. Ele gerencia a manipulação de erros implementando a interface `ErrorHandler` usando o mesmo algoritmo para selecionar servlets e scripts de manipulação de erros usado para resolver servlets e scripts de processamento de solicitações.

Vários parâmetros podem ser definidos, incluindo:

* **Caminhos de Execução** - Lista os caminhos para procurar scripts executáveis. Ao configurar caminhos específicos, você pode limitar quais scripts podem ser executados. Se nenhum caminho estiver configurado, o padrão será usado ( `/` = raiz), permitindo a execução de todos os scripts.
Se um valor de caminho configurado terminar com uma barra, a subárvore inteira será pesquisada. Sem essa barra à direita, o script só é executado se for uma correspondência exata.

* **Usuário de Script** - Esta propriedade opcional pode especificar a conta de usuário do repositório usada para ler os scripts. Se nenhuma conta for especificada, o usuário `admin` será usado por padrão.

* **Extensões Padrão** - A lista de extensões para as quais o comportamento padrão é usado. O último segmento de caminho do tipo de recurso pode ser usado como o nome do script.

**Configuração de proxy de componentes HTTP do Apache** - A configuração de proxy de todo o código usando o cliente HTTP do Apache, usada quando um HTTP é criado. Por exemplo, sobre replicação.

Ao criar uma configuração, não altere a configuração de fábrica. Em vez disso, crie uma configuração de fábrica para esse componente usando o gerenciador de configurações disponível aqui: **https://localhost:4502/system/console/configMgr/**. A configuração de proxy está disponível em **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>No AEM 6.0 e versões anteriores, o proxy era configurado no Day Commons HTTP Client. A partir do AEM 6.1 e versões posteriores, a configuração de proxy foi movida para a &quot;Configuração de proxy de componentes HTTP do Apache&quot; em vez da configuração &quot;Day Commons HTTP Client&quot;.

**Day CQ Antispam** Configure o serviço antisspam (Akismet) usado. Esse recurso exige que você registre o seguinte:

* **Provedor**
* **Chave de API**
* **URL registrada**

**Gerenciador de biblioteca de HTML do Adobe Granite** Configure para controlar a manipulação de bibliotecas de clientes (css ou js) incluindo, por exemplo, como a estrutura subjacente é vista.

* Para instâncias de produção:

   * habilitar **Minify** (para remover caracteres CRLF e espaços em branco).
   * habilite o **Gzip** (para permitir que os arquivos sejam compactados e acessados com uma solicitação).
   * desabilitar **Depuração**
   * desabilitar **Horário**

* Para o desenvolvimento de JS (especialmente quando há firebugging/depuração):

   * desabilitar **Minify**
   * habilite **Depurar** para separar os arquivos para depuração e usar com o fire bug.
   * habilite **Timing** se estiver interessado em sincronização.
   * habilite o console **Debug** para ver as mensagens de log do console JS.

>[!CAUTION]
>
>Ao alterar a configuração para **Minify** ou **Gzip**, exclua o conteúdo do cache clientlibs. Consulte o [artigo da Base de Dados de Conhecimento](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=pt-BR) para obter detalhes.

>[!NOTE]
>
>Essa configuração é definida automaticamente para instâncias de produção se você executar o AEM no [Modo de Produção Pronta](/help/sites-administering/production-ready.md).

Manipulador de Autenticação de Cabeçalho HTTP CQ de **Dias** Configurações do sistema para o método de autenticação básico da solicitação HTTP.

Ao usar [grupos de usuários fechados](/help/sites-administering/cug.md), você pode configurar, entre outros, o seguinte:

* **Território HTTP**
* A **Página de Logon Padrão**

**Serviço Verificador de Links CQ do Dia** Verifique e, se necessário, configure:

* **Período do Agendador** para definir o intervalo no qual os links externos devem ser verificados automaticamente.

* Verifique **Intervalo de Tolerância de Link Incorreto** para o período após o qual um link externo malsucedido é considerado incorreto.
* **Padrões de Substituição de Verificação de Link**, para definir quaisquer caminhos a serem excluídos da verificação de link.

**Tarefa do Verificador de Links CQ do Dia** Defina as configurações de uma única tarefa do verificador de links (uma tarefa que verifica um link externo):

* Verifique os intervalos definidos em **Intervalo de Teste de Link Bom** e **Intervalo de Teste de Link Incorreto**

* Os vários parâmetros relacionados a proxies para acesso à Internet e NTLM necessários para acesso externo ao verificar um link.

**Day CQ Mail Service** Configure o nome do host e os detalhes de acesso do servidor de email. Consulte a seção Configurando o Serviço de E-mail.

**Informativo MCM CQ do dia** Defina as várias configurações usadas com o informativo.

**Day CQ Root Mapping** Configurar:

* **Caminho de Destino** para definir para onde uma solicitação para &quot; `/`&quot; é redirecionada.

Há duas interfaces do usuário disponíveis no AEM:

* a interface habilitada para toque é a interface padrão
* e a interface clássica obsoleta ainda está totalmente operacional

Usando o mapeamento de raiz AEM, é possível configurar a interface do usuário que você deseja ter como padrão para sua instância:

* Para ter a interface habilitada para toque como a interface padrão, o **Caminho de Destino** deve apontar para o seguinte:

  ```shell
     /projects.html
  ```

* Para ter a interface clássica como a interface padrão, o **Caminho de Destino** deve apontar para o seguinte:

  ```shell
     /welcome.html
  ```

>[!NOTE]
>
>Em uma instalação padrão, a interface otimizada para toque é a interface padrão.

**Manipulador de Autenticação de SSO do Adobe Granite** - Configurar detalhes de SSO (Logon Único). Esses detalhes geralmente são necessários nas configurações do autor corporativo, geralmente com LDAP.

Várias propriedades de configuração estão disponíveis:

* **Caminho**
O caminho para o qual este manipulador de autenticação está ativo. Se esse parâmetro for deixado em branco, o manipulador de autenticação será desativado. Por exemplo, o caminho / faz com que o manipulador de autenticação seja usado para todo o repositório.

* **Classificação do serviço**
O valor de Classificação do OSGi Framework Service é usado para indicar a ordem usada para chamar esse serviço. Este valor é um valor de `int`, no qual valores mais altos designam maior precedência.
O valor padrão é `0`.

* **Nomes de Cabeçalho**
Os nomes dos cabeçalhos que podem conter uma ID de usuário.

* **Nomes de Cookies**
Os nomes dos cookies que podem conter uma ID de usuário.

* **Nomes de Parâmetros**
Os nomes dos parâmetros de solicitação que podem fornecer a ID do usuário.

* **Mapa de usuários**
Para usuários selecionados, o nome de usuário extraído da solicitação HTTP pode ser substituído por outro no objeto de credenciais. O mapeamento é definido aqui. Se o nome de usuário `admin` aparecer em ambos os lados do mapa, o mapeamento será ignorado. O caractere &quot;=&quot; deve ser escapado com um &quot;\&quot; à esquerda.

* **Formato**
Indica o formato em que a ID de usuário é fornecida. Uso:

   * `Basic` se a ID do usuário estiver codificada no formato de Autenticação Básica HTTP
   * `AsIs` se a ID de usuário for fornecida em texto sem formatação ou qualquer valor de expressão regular aplicada, deverá ser usada como está ou qualquer expressão regular

**Filtro de depuração WCM CQ do dia** Isso é útil no desenvolvimento, pois permite o uso de sufixos como ?debug=layout ao acessar uma página. Por exemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout fornece informações de layout que podem ser de interesse do desenvolvedor.

* Para garantir desempenho e segurança, desative em instâncias de produção.

**Filtro WCM CQ de Dias** Configurar:

* **WCM Mode** para definir o modo padrão.
* Em uma instância de autor, este modo pode ser `edit`, `disable,preview` ou `analytics`.
Os outros modos podem ser acessados do sidekick ou o sufixo `?wcmmode=disabled` pode ser usado para emular um ambiente de produção.

* Em uma instância de publicação, esse modo deve ser definido como `disabled` para garantir que nenhum outro modo esteja acessível.

>[!NOTE]
>
>Essa configuração é definida automaticamente para instâncias de produção se você executar o AEM no [Modo de Produção Pronta](/help/sites-administering/production-ready.md).

**Configurador do Verificador de Links CQ de Dias** Configurar:

* **Lista de configurações de regravação** para especificar uma lista de locais para configurações do verificador de links baseado em conteúdo. As configurações podem ser baseadas no modo de execução. Esse fato é importante para distinguir entre ambientes de autor e publicação, pois as configurações do verificador de links podem ser diferentes.

**Fábrica do gerenciador de páginas do WCM CQ do dia** Configurar:

* **Verificação de Ativação da Subárvore de Página** para um usuário (sem permissões de replicação) excluir ou mover páginas (mesmo que as páginas não estejam ativadas).

**Processador de página WCM CQ do dia** Configurar:

* **Caminhos**, uma lista de locais onde o sistema escuta as modificações de página antes de acionar um `jcr:Event`.

**Rastreador de impressões de página do Adobe** Para uma instância de autor, configure como a seguinte:

* **sling.auth.requirements**: definir o valor desta propriedade como `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Essa configuração permite solicitações anônimas para o serviço de rastreamento.

>[!NOTE]
>
>Consulte [Impressões de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obter mais informações.

**Estatísticas de página WCM CQ do dia** Para uma instância de publicação, configure:

* **URL para enviar dados** para configurar a URL usada para rastrear estatísticas de página (é essencial se uma solicitação do rastreador passar pela Dispatcher); por exemplo, o padrão é `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script de rastreamento habilitado** para habilitar ( `true`) ou desabilitar ( `false`) a inclusão do script de rastreamento nas páginas. O valor padrão é `false`.

>[!NOTE]
>
>Consulte [Impressões de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obter mais informações.

**Gerenciador de versão do WCM do CQ do dia** Controle se e como as versões são gerenciadas em seu sistema:

* **Criar versão na ativação**, habilitada em uma instalação padrão
* **Habilitar Limpeza**

* **Caminhos de Limpeza**, os caminhos pesquisados por uma ação de pesquisa.
* **Caminhos de controle de versão implícito**, os caminhos em que o controle de versão implícito está ativo.

* **Idade Máxima da Versão**, a idade máxima (em dias) de uma versão

* **Número Máximo de Versões**, o número máximo de versões a serem mantidas

Consulte [Limpeza de versão](/help/sites-deploying/version-purging.md) para obter mais informações.

**Serviço de notificação por email do fluxo de trabalho do CQ de dias** Defina as configurações de email para notificações enviadas por um fluxo de trabalho.

**Fábrica de Analisador de HTML de Reescrita CQ**

Controla o Analisador de HTML para o reescritor CQ.

* **Marcas Adicionais a Serem Processadas** - Você pode adicionar ou remover marcas HTML a serem processadas pelo analisador. Por padrão, as seguintes tags são processadas: A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD.
* **Preservar Camel Case** - Por padrão, o analisador de HTML converte atributos em camel case (por exemplo, `eBay`) para lower case (por exemplo, `ebay`). Você pode desativar essa configuração para preservar os atributos de camel case. Essa configuração é útil ao usar estruturas de front-end, como o Angular 2.

**Pool de Conexões JDBC do Day Commons** Configure o acesso a um banco de dados externo que está sendo usado como fonte de conteúdo.

Uma configuração de fábrica, para que várias instâncias possam ser configuradas.

**Reescritor de CDN** A comunicação entre AEM e um CDN deve ser assegurada para que os ativos/binários sejam entregues a um usuário final de forma segura. Esse processo envolve as duas tarefas a seguir:

* Acessar o recurso do AEM por meio da CDN na primeira vez (ou depois que ele expirou no cache).
* Acessar o recurso em cache na CDN com segurança. Depois que o recurso é armazenado em cache no CDN, a solicitação não vai para o AEM e todos os usuários que têm acesso a esse recurso em devem ser fornecidos pelo CDN.

O AEM fornece um reescritor para reescrever URLs de ativos internos em URLs CDN externos. Ele substitui links a serem transmitidos para o CDN, incluindo uma assinatura JWS e um tempo de expiração para permitir que o ativo seja acessado com segurança. Esse recurso deve ser usado em instâncias de autor.

O fluxo total é o seguinte:

1. O usuário se autentica com AEM e solicita uma página com ativos.
1. A página solicitada contém um ativo semelhante a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. O Rewriter transforma o link em um URL CDN contendo uma Assinatura JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. O navegador do usuário encaminha a solicitação de ativo para o servidor CDN
1. O CDN deve ser configurado para encaminhar a solicitação ao AEM junto com o parâmetro `cdn_sign`.
1. Um Manipulador de autenticação valida o parâmetro `cdn_sign` e retorna o ativo para o CDN, que é então entregue ao usuário

O fluxo entre o navegador do usuário, o CDN e o AEM pode ser visualizado da seguinte maneira.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Esse recurso só é ativado para instâncias de autor AEM.

**CDNConfigServiceImpl** Fornece configurações de CDN

O recurso de reescrita CDN pode ser habilitado fornecendo-se o **nome de domínio de distribuição CDN** na configuração para com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

O serviço também contém outras opções de configuração, como ativar/desativar a reescrita de CDN, prefixos de caminho para os quais a reescrita de CDN é executada, valores TTL e protocolo (HTTP ou HTTPS).

**CDNRewriter** Um reescritor para reescrever URLs de imagens internas em URLs CDN

O valor **Atributos da Marca** em com.adobe.cq.cdn.rewriter.impl.CDNRewriter pode ser definido para que somente os links de imagens seletivas sejam regravados.

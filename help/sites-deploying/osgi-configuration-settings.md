---
title: Configurações do OSGi
seo-title: OSGi Configuration Settings
description: Este artigo detalha as configurações do OSGi (listadas de acordo com o pacote) que são relevantes para a implementação do projeto. A lista atua como uma diretriz e não é exaustiva.
seo-description: This article details the OSGi configuration settings (listed according to bundle) that are relevant to project implementation. The list acts as a guideline and it is not exhaustive.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: 9a3f26b6709461a911e833f7e340d11c759c7dae
workflow-type: tm+mt
source-wordcount: '3558'
ht-degree: 0%

---

# Configurações do OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia de AEM. É usado para controlar os pacotes compostos de AEM e sua configuração.

OSGi &quot;*O fornece os primitivos padronizados que permitem que os aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados*&quot;.

Isso permite o gerenciamento fácil de pacotes, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são manipuladas automaticamente. Cada componente OSGi (consulte o [Especificação OSGi](https://www.osgi.org/Specifications/HomePage)) está contido em um dos vários pacotes. Ao trabalhar com AEM, há vários métodos de gerenciamento das configurações desses pacotes; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

As seguintes configurações de configuração do OSGi (listadas de acordo com o pacote) são relevantes para a implementação do projeto. Nem todas as configurações listadas precisam de ajuste, algumas são mencionadas para ajudar você a entender como o AEM opera.

>[!CAUTION]
>
>A lista destina-se a atuar como uma diretriz e não é exaustiva. Nem todos os pacotes são listados, nem todos os parâmetros para alguns dos pacotes que são.
>
>A configuração necessária varia de projeto para projeto.
>
>Consulte o console da Web para obter os valores usados e informações detalhadas sobre os parâmetros.

>[!NOTE]
>
>A ferramenta Diff de configuração do OSGi, parte da [Ferramentas AEM](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html), pode ser usado para listar as configurações padrão do OSGi.

>[!NOTE]
>
>Podem ser necessários outros pacotes para áreas de funcionalidade específicas no AEM. Nesses casos, os detalhes de configuração podem ser encontrados na página relacionada à funcionalidade apropriada.

**Ouvinte de Evento de Replicação de AEM** Configurar:

* O **Modos de Execução**, em que os eventos de replicação serão distribuídos aos ouvintes. Por exemplo, se definido como autor, esse é o sistema que &quot;iniciará&quot; a replicação.

* O modo de execução **publicar** precisa ser adicionado se o código do projeto processar eventos de replicação (replicação inversa) em um ambiente de publicação. Por exemplo, quando o dispatcher é usado para liberar do ambiente de publicação ou quando ocorre a replicação padrão para outras instâncias de publicação.

**AEM Ouvinte de alteração do repositório** Configurar:

* O **Caminhos**, locais para detectar eventos de repositório prontos para distribuição.

**Repositório de Cliente Sling CRX** Configure o acesso ao repositório de conteúdo subjacente.

* O **Senha do administrador** deve ser alterada após a instalação para garantir que a função [segurança](/help/sites-administering/security-checklist.md) da sua instância.
* Outras alterações não devem ser necessárias e devem ser tomadas precauções, pois podem afetar o acesso ao repositório.

**Serviço de Correio Wiki** Defina as configurações de email para emails enviados por um wiki.

**Console de Gerenciamento do Apache Felix OSGi** Configurar:

* **Plug-ins**, os principais itens de navegação (plug-ins do console) que estarão disponíveis na variável **Console de Gerenciamento da Web Apache Felix** como itens de menu de nível superior. Desative qualquer item que não seja necessário, pois cada um requer espaço e recursos.

>[!CAUTION]
>
>Certifique-se de configurar o seguinte:
>
>**Nome do usuário** e **Senha**, as credenciais para acessar o próprio Apache Felix Web Management Console.
>A senha deve ser alterada após a instalação inicial para garantir que o [segurança](/help/sites-administering/security-checklist.md) da sua instância.

>[!NOTE]
>
>Essa configuração deve ser feita usando o Felix Console, conforme necessário na inicialização - antes que o repositório esteja disponível.

**Apache Sling Customizable Request Data Logger** Configurar:

* **Nome do logger** e **Formato de registro** para configurar o local e o formato do registro de solicitação e acesso (padrão: `request.log`). Esse arquivo de log é essencial ao analisar o desempenho ou a funcionalidade de depuração relacionada à cadeia da Web.
Isso é emparelhado com a variável [Logon de solicitação do Apache Sling](#apacheslingrequestlogger).

Para obter mais informações, consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) e [Registro do Sling](https://sling.apache.org/site/logging.html).

**Pool de Thread de Eventos do Apache Sling** Configurar:

* **Tamanho Mín. do Pool** e **Tamanho máximo do pool**, o tamanho do pool usado para armazenar threads de evento.

* **Tamanho da fila**, o tamanho máximo da fila de thread se o pool estiver esgotado.
O valor recomendado é `-1` já que isso define a fila como ilimitada; se um limite for definido, as perdas podem ocorrer quando ele for excedido.

* Alterar essas configurações pode ajudar no desempenho em cenários com um alto número de eventos; por exemplo, uso intenso de DAM ou Fluxo de trabalho AEM.
* Os valores específicos do seu cenário devem ser estabelecidos usando testes.
* Essas configurações podem afetar o desempenho da sua instância, portanto, não as altere sem motivo e consideração.

**Servlet de GET Apache Sling** Configure alguns aspectos da renderização:

* **Índice automático** para ativar/desativar a renderização do diretório para navegação.
* **Habilitar** (ou desativar) representações padrão, como **HMTL**, **Texto sem formatação**, **JSON** ou **XML**.
Você não deve desativar o JSON.

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar AEM em [Modo Pronto para produção](/help/sites-administering/production-ready.md).

**Manipulador de script Java do Apache Sling** Defina as configurações para a compilação de arquivos .java como scripts (servlets).

Certas configurações podem afetar o desempenho, elas devem ser desativadas sempre que possível, principalmente para uma instância de produção.

* S **VM de origem** e **VM de destino**, defina a versão do JDK como a usada como JVM em tempo de execução

* para instâncias de produção:

   * disable **Gerar informações de depuração**

**Instalador do Apache Sling JCR** Esses parâmetros provavelmente não precisam de configuração, mas podem ser úteis para saber ao desenvolver ou depurar. Por exemplo, a(s) pasta(s) de instalação pode(m) ser útil para fazer check-in/out ou criar um pacote.

* **Nome das pastas de instalação regexp** e **Profundidade máxima da hierarquia de pastas de instalação** - especifique onde e a que profundidade as pastas do repositório são pesquisadas para que os recursos sejam instalados. Quando um curinga é usado (como em .*/install) todas as correspondências apropriadas serão pesquisadas, por exemplo, `/libs/sling/install` e `/libs/cq/core/install`.

* **Caminho de pesquisa**, a lista de caminhos que o jcrinstall procura recursos a serem instalados, juntamente com um número que indica o fator de ponderação para esse caminho.

**Manipulador de evento de trabalho do Apache Sling** Configure parâmetros que gerenciam a programação de tarefas:

* **Intervalo de tentativas**, **Máximo de Tentativas**, **Máximo de trabalhos paralelos**, **Ativar Tempo de Espera**, entre outros.

* Alterar essas configurações pode melhorar o desempenho em cenários com um alto número de tarefas; por exemplo, uso intenso de AEM DAM e workflows.
* Os valores específicos do seu cenário devem ser estabelecidos usando testes.
* Não altere essas configurações sem motivo, só sendo alterado após a devida consideração.

**Manipulador de script JSP do Apache Sling** Defina as configurações relevantes para o desempenho do manipulador de script JSP. Para melhorar o desempenho, você deve desativar o máximo possível.

Em especial para instâncias de produção:

* disable **Gerar informações de depuração**
* disable **Manter Java gerado**
* disable **Conteúdo mapeado**
* disable **Exibir fragmentos de origem**

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar AEM em [Modo Pronto para produção](/help/sites-administering/production-ready.md).

**Configuração de registro do Apache Sling** Configurar:

* **Nível de log** e **Arquivo de log**, para definir o local e o nível de log da configuração de log central (error.log). O nível pode ser definido como um dos `DEBUG`, `INFO`, `WARN`, `ERROR` e `FATAL`.

* **Número de arquivos de log** e **Limite do arquivo de log** para definir o tamanho e a rotação da versão do arquivo de log.

* **Padrão de mensagem** define o formato das mensagens de log.

Para obter mais informações, consulte [Registro de AEM](/help/sites-deploying/configure-logging.md#global-logging) e [Registro do Sling](https://sling.apache.org/site/logging.html).

**Configuração do Apache Sling Logging Logger (Configuração de Fábrica)** Configurar:

* **Nível de log**, **Arquivo de log** e **Formato de mensagem** para definir detalhes do arquivo de log e das mensagens.

* **Logger** definir a categoria; por exemplo, registre somente para com.day.cq.

* Ao usar **Configurações de fábrica**, qualquer número de configurações adicionais pode ser adicionado para atender aos vários níveis de log e categorias necessárias.
* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens de TRACE para um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, ter mensagens sobre um serviço específico registradas em um arquivo de log individual para facilitar o monitoramento.

Para obter mais informações, consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) e [Registro do Sling](https://sling.apache.org/site/logging.html).

**Configuração do Apache Sling Logging Writer (Configuração de Fábrica)** Configurar:

* **Arquivo de log** para definir a existência de um arquivo de log.
* **Número de arquivos de log** para definir a rotação da versão.

* O autor pode ser usado por um **Configuração do Apache Sling Logging Logger** configuração.

* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens de TRACE para um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, ter mensagens sobre um serviço específico registradas em um arquivo de log individual para facilitar o monitoramento.

Para obter mais informações, consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) e [Registro do Sling](https://sling.apache.org/site/logging.html).

**Servlet principal Apache Sling** Configurar:

* **Número de chamadas por solicitação** e **Profundidade de recorrência** para proteger seu sistema contra chamadas de recursão infinitas e de script excessivo.

**Apache Sling MIME Type Service** Configurar:

* **Tipos MIME** para adicionar os requisitos exigidos pelo seu projeto ao sistema. Isso permite que uma `GET` em um arquivo para definir o cabeçalho de tipo de conteúdo correto para vincular o tipo de arquivo e o aplicativo.

**Filtro de referenciador do Apache Sling** Para solucionar problemas de segurança conhecidos com a falsificação de solicitação entre sites (CSRF) no CRX WebDAV e no Apache Sling, é necessário configurar o filtro Referenciador .

O serviço de filtro do referenciador é um serviço OSGi que permite configurar:

* quais métodos http devem ser filtrados
* se um cabeçalho de referenciador vazio é permitido
* e uma lista de servidores a serem permitidos além do host do servidor.

Consulte a [Lista de verificação de segurança - Problemas com a falsificação de solicitação entre sites](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obter mais detalhes.

>[!NOTE]
>
>O Apache Sling Referrer Filter depende da instalação de um pacote de correção rápida.

**Logon de solicitação do Apache Sling** Configurar:

* vários parâmetros para definir como as solicitações são registradas.
* **Ativar registro de solicitações**, para ativar ou desativar.

* **Ativar registro de acesso**, para ativar ou desativar.

Isso é emparelhado com a variável [Apache Sling Customizable Request Data Logger](#apacheslingcustomizablerequestdatalogger).

Para obter mais informações, consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) e [Registro do Sling](https://sling.apache.org/site/logging.html).

**Fábrica do Resolvedor de Recursos do Apache Sling** Configure os aspectos centrais da resolução de recursos do Sling:

* **Caminho de pesquisa de recursos**(s), adicione caminhos específicos do projeto (mas não remova `/libs` ou `/apps`).

* **URLs virtuais** para definir os mapeamentos de URL personalizados.

* **Mapeamentos de URL** definir quaisquer aliases; por exemplo, de `/content` para `/`.

* **Localização do mapeamento**, a configuração do mapeador externalizada em `/etc/map`.

* Use sua instalação local (por exemplo, use `https://localhost:4502/system/console/jcrresolver`) para determinar qual Resolvedor de Recursos está ativo.

Para obter mais informações, consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Especificamente, essas opções devem ser configuradas no repositório.
>
>Alterações feitas de outra forma em **Mapeamentos de URL** o uso do console Felix pode ser substituído pelo AEM na próxima inicialização.

**Apache Sling Servlet/Script Resolver e Manipulador de Erros** O Sling Servlet e o Script Resolver têm várias tarefas:

1. É usado como o `ServletResolver` para selecionar o Servlet ou Script para chamar para lidar com a solicitação.

1. Atua como a `SlingScriptResolver`.

1. Ele gerencia o tratamento de erros ao implementar o `ErrorHandler` interface usando o mesmo algoritmo para selecionar erros ao manipular servlets e scripts usados para resolver servlets e scripts de processamento de solicitação.

Vários parâmetros podem ser definidos, incluindo:

* **Caminhos de execução** lista os caminhos para procurar scripts executáveis; ao configurar caminhos específicos, você pode limitar quais scripts podem ser executados. Se nenhum caminho estiver configurado, o padrão será usado ( `/` = root), isso permite a execução de todos os scripts.
Se um valor de caminho configurado terminar com uma barra, a subárvore inteira será pesquisada. Sem essa barra à direita, o script só será executado se for uma correspondência exata.

* **Usuário do script** - essa propriedade opcional pode especificar a conta de usuário do repositório usada para ler os scripts. Se nenhuma conta for especificada, a variável `admin` O usuário é usado por padrão.

* **Extensões padrão** A lista de extensões para as quais o comportamento padrão será usado. Isso significa que o último segmento de caminho do tipo de recurso pode ser usado como o nome do script.

**Day Commons GFX Font Helper** Ao renderizar gráficos, você pode usar DrawText para incorporar o texto. Para isso, você também pode instalar suas próprias fontes:

* Defina as **Caminho da fonte** a ser pesquisado por fontes específicas do projeto.
Por exemplo, `/apps/myapp/fonts`.

**Configuração de proxy de componentes HTTP do Apache** Configuração de proxy para todos os códigos usando o cliente HTTP Apache, usado quando um HTTP é feito; por exemplo, na replicação.

Ao criar uma nova configuração, não faça alterações na configuração de fábrica, mas crie uma nova configuração de fábrica para este componente usando o gerenciador de configuração disponível aqui: **https://localhost:4502/system/console/configMgr/**. A configuração de proxy está disponível em **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>No AEM 6.0 e versões anteriores, o proxy foi configurado no Day Commons HTTP Client. A partir AEM 6.1 e versões posteriores, a configuração de proxy foi movida para a &quot;Configuração de proxy de componentes HTTP do Apache&quot; em vez da configuração &quot;Cliente HTTP do Day Commons&quot;.

**Day CQ Antispam** Configure o serviço antisspam (Akismet) usado. Isso requer que você registre o:

* **Provedor**
* **Chave da API**
* **URL registrado**

**Gerenciador de biblioteca de HTML do Adobe Granite** Configure isso para controlar o manuseio de bibliotecas de clientes (css ou js); incluindo, por exemplo, como a estrutura subjacente é vista.

* Para instâncias de produção:

   * habilitar **Minimizar** (para remover caracteres CRLF e espaço em branco).
   * habilitar **Gzip** (para permitir que os arquivos sejam compactados e acessados com uma solicitação).
   * disable **Depurar**
   * disable **Tempo**

* Para desenvolvimento de JS (especialmente quando firebugging/debugging):

   * disable **Minimizar**
   * habilitar **Depurar** para separar os arquivos para depuração e uso com firebug.
   * habilitar **Tempo** no caso de interesse em tempo oportuno.
   * habilitar **Depurar** para ver as mensagens de log do console JS.

>[!CAUTION]
>
>Ao alterar a configuração de **Minimizar** ou **Gzip** também será necessário excluir o conteúdo de `/var/clientlibs`. Esta é uma versão em cache das clientlibs e será recriada quando a próxima solicitação for feita.

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar AEM em [Modo Pronto para produção](/help/sites-administering/production-ready.md).

**Manipulador de autenticação de cabeçalho HTTP CQ do dia** Configurações do sistema para o método de autenticação básico da solicitação HTTP.

Ao usar [grupos de usuários fechados](/help/sites-administering/cug.md) você pode configurar (entre outros):

* **Realm HTTP**
* O **Página de logon padrão**

**Serviço Day CQ Link Checker** Marque e, se necessário, configure:

* **Período do Scheduler** para definir o intervalo em que os links externos devem ser verificados automaticamente.

* Verificar **Intervalo de Tolerância de Link Incorreto** para o período após o qual um link externo malsucedido é considerado ruim.
* **Padrões de Substituição de Verificação de Link**, para definir quaisquer caminhos a serem excluídos da verificação de link.

**Tarefa Day CQ Link Checker** Defina as configurações para uma única tarefa do verificador de links (uma tarefa que verifica um link externo):

* Verifique os intervalos definidos em **Intervalo de teste de link bom** e **Intervalo de teste de link inválido**

* Os vários parâmetros relacionados a proxies para acesso à Internet e NTLM que são necessários para acesso externo ao verificar um link.

**Day CQ Mail Service** Configure o nome do host e os detalhes de acesso do servidor de email. Consulte a seção Configuração do serviço de email .

**Informativo do Day CQ MCM** Configure as várias configurações usadas com o boletim informativo.

**Mapeamento raiz do CQ do dia** Configurar:

* **Caminho do Target** para definir onde uma solicitação para &quot; `/`&quot; será redirecionado para.

Há duas interfaces de usuário disponíveis no AEM:

* a interface de usuário habilitada para toque é a interface de usuário padrão
* e a interface clássica obsoleta ainda está totalmente operacional

Usando AEM Mapeamento de Raiz, você pode configurar a interface que deseja ter como padrão para sua instância:

* Para ter a interface habilitada para toque como a interface padrão do usuário **Caminho do Target** deve indicar:

   ```
      /projects.html
   ```

* Para ter a interface clássica como a interface padrão do usuário do **Caminho do Target** deve indicar:

   ```
      /welcome.html
   ```

>[!NOTE]
>
>Em uma instalação padrão, a interface otimizada para toque é a interface padrão.

**Manipulador de Autenticação SSO do Adobe Granite** Configurar detalhes do Logon único (SSO); geralmente, elas são necessárias em configurações de autor corporativo, geralmente em conjunto com o LDAP.

Várias propriedades de configuração estão disponíveis:

* **Caminho**
Caminho para o qual este manipulador de autenticação está ativo. Se este parâmetro for deixado em branco, o manipulador de autenticação será desativado. Por exemplo, o caminho / faz com que o manipulador de autenticação seja usado para todo o repositório.

* **Classificação do serviço**
O valor de Classificação do Serviço de Estrutura OSGi é usado para indicar a ordem usada para chamar este serviço. Isso é uma 
`int` , sempre que valores mais elevados designem uma precedência mais elevada.
O valor padrão é `0`.

* **Nomes de Cabeçalho**
O(s) nome(s) dos cabeçalhos que podem conter uma ID de usuário.

* **Nomes de cookies**
Os nomes dos cookies que podem conter uma ID de usuário.

* **Nomes de Parâmetros**
O(s) nome(s) dos parâmetros de solicitação que podem fornecer a ID do usuário.

* **Mapa do usuário**
Para usuários selecionados, o nome de usuário extraído da solicitação HTTP pode ser substituído por um diferente no objeto de credenciais. O mapeamento é definido aqui. Se o nome do usuário 
`admin` for exibido em qualquer lado do mapa, o mapeamento será ignorado. Esteja ciente de que o caractere &quot;=&quot; deve ser evitado com um &quot;\&quot; à esquerda.

* **Formato**
Indica o formato em que a ID de usuário é fornecida. Uso:

   * `Basic` se a ID do usuário estiver codificada no formato HTTP Basic Authentication
   * `AsIs` se a ID de usuário for fornecida em texto simples ou qualquer expressão regular aplicada, o valor deve ser usado como está ou qualquer expressão regular

**Filtro de depuração do Day CQ WCM** Isso é útil ao desenvolver, pois permite o uso de sufixos como ?debug=layout ao acessar uma página. Por exemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout fornecerá informações de layout que podem ser de interesse do desenvolvedor.

* Desative isso em instâncias de produção para garantir desempenho e segurança.

**Filtro Day CQ WCM** Configurar:

* **Modo WCM **para definir o modo padrão.
* Em uma instância do autor, pode ser que `edit`, `disable,preview` ou `analytics`.
Os outros modos podem ser acessados do sidekick ou do sufixo `?wcmmode=disabled` pode ser usada para emular um ambiente de produção.

* Em uma instância de publicação, isso deve ser definido como `disabled` para garantir que nenhum outro modo seja acessível.

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar AEM em [Modo Pronto para produção](/help/sites-administering/production-ready.md).

**Configurador do Verificador de Links WCM CQ do Dia** Configurar:

* **Lista de configurações de reescrita** para especificar uma lista de locais para configurações do linkchecker baseadas em conteúdo. As configurações podem ser baseadas no modo de execução; isso é importante para distinguir entre ambientes de autor e publicação, pois as configurações do linkchecker podem ser diferentes.

**Fábrica do gerenciador de página do Day CQ WCM** Configurar:

* **Verificação de Ativação de Subárvore de Página** para um usuário (sem permissões de replicação) excluir ou mover páginas (mesmo se as páginas não estiverem ativadas).

**Processador de página CQ WCM do dia** Configurar:

* **Caminhos**, uma lista de locais em que o sistema escuta modificações de página antes de acionar uma `jcr:Event`.

**Rastreador de impressões de página do Adobe** Para uma instância de autor, configure:

* **sling.auth.requirements**: defina o valor dessa propriedade como `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Essa configuração permitirá solicitações anônimas para o serviço de rastreamento.

>[!NOTE]
>
>Consulte [Impressões da página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obter mais informações.

**Estatísticas de página do WCM CQ do dia** Para uma instância de publicação, configure:

* **URL para enviar dados** configurar o URL usado para rastrear as estatísticas da página (é essencial se uma solicitação do rastreador passar pelo dispatcher); por exemplo, o padrão é `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script de rastreamento ativado** para ativar ( `true`) ou desativar ( `false`) a inclusão do script de rastreamento nas páginas. O valor padrão é `false`.

>[!NOTE]
>
>Consulte [Impressões da página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obter mais informações.

**Gerenciador de versão do Day CQ WCM** Controle se e como as versões são gerenciadas em seu sistema:

* **Criar versão na ativação**, ativada em uma instalação padrão
* **Habilitar limpeza**

* **Eliminar caminhos**, os caminhos que uma ação de pesquisa pesquisará
* **Caminhos de controle de versão implícitos**, os caminhos onde o controle de versão implícito está ativo.

* **Idade máxima da versão**, a idade máxima (em dias) de uma versão

* **Versões do número máximo**, o número máximo de versões a serem mantidas

Consulte [Limpeza de versão](/help/sites-deploying/version-purging.md) para obter mais informações.

**Serviço de Notificação por Email do Workflow CQ Dia** Defina as configurações de email para notificações enviadas por um workflow.

**Fábrica de analisador do HTML de regravação CQ**

Controla o analisador de HTML para a reescrita do CQ.

* **Tags adicionais a serem processadas** - Você pode adicionar ou remover tags HTML para serem processadas pelo analisador. Por padrão, as seguintes tags são processadas: A,IMG,ÁREA,FORMULÁRIO,BASE,LINK,SCRIPT,CORPO,HEAD.
* **Preservar Camel Case** - Por padrão, o analisador de HTML converte atributos em camel case (por exemplo, eBay) em minúsculas (por exemplo, ebay). Você pode desativar o para preservar os atributos de maiúsculas e minúsculas do camel. Isso é útil ao usar estruturas de primeiro plano, como o Angular 2.

**Pool de Conexões JDBC do Day Commons** Configure o acesso a um banco de dados externo que está sendo usado como fonte de conteúdo.

Esta é uma configuração de fábrica, portanto várias instâncias podem ser configuradas.

**Serviço de sessões do Adobe CQ Media DPS** Gerencie Sessões do DPS para usar com Publicações.

Em particular, você pode definir a variável `dps.session.service.url.name`: o padrão está definido como [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**Gravador CDN** A comunicação entre AEM e uma CDN deve ser assegurada para que os ativos/binários sejam entregues ao usuário final de forma segura. Isso envolve duas tarefas:

* Acessar o recurso do AEM por meio da CDN na primeira vez (ou após expirar no cache).
* Acessar o recurso armazenado em cache no CDN com segurança, pois uma vez que o recurso é armazenado em cache no CDN, a solicitação não irá para o AEM e todos os usuários que têm acesso a esse recurso no devem ser fornecidos do CDN.

AEM fornece um regravador para regravar URLs de ativos internos em URLs CDN externos. Ele reescreve links a serem passados para a CDN, incluindo uma assinatura JWS e expira o tempo para permitir que o ativo seja acessado com segurança. Esse recurso deve ser usado em instâncias do autor.

O fluxo global é o seguinte:

1. O usuário é autenticado com AEM e solicita uma página com ativos.
1. A página solicitada contém um ativo semelhante a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. O regravador transforma o link para um URL CDN contendo uma Assinatura JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. O navegador do usuário encaminha a solicitação de ativo para o servidor CDN
1. A CDN deve ser configurada para encaminhar a solicitação para o AEM junto com o `cdn_sign` parâmetro.
1. Um Manipulador de Autenticação valida o `cdn_sign` e retorna o ativo para a CDN, que é então entregue ao usuário

O fluxo entre o navegador do usuário, o CDN e o AEM pode ser visualizado da seguinte maneira.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>No momento, esse recurso é ativado apenas para instâncias AEM autor.

**CDNConfigServiceImpl** Fornece configurações de CDN

O recurso de regravação de CDN pode ser ativado ao fornecer **Nome do domínio de distribuição CDN** na configuração para com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

O serviço também contém outras opções de configuração, como ativar/desativar a reescrita de CDN, prefixos de caminho para os quais a reescrita de CDN é executada, valores TTL e protocolo (HTTP ou HTTPS).

**CDNRewriter** Um regravador para regravar URLs de imagens internas em URLs CDN

O **Atributos de tag** em com.adobe.cq.cdn.rewriter.impl.CDNRewriter pode ser definido para que somente os links de imagem seletiva sejam reescritos.

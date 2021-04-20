---
title: Configurações do OSGi
seo-title: Configurações do OSGi
description: Este artigo detalha as configurações do OSGi (listadas de acordo com o pacote) que são relevantes para a implementação do projeto. A lista atua como uma diretriz e não é exaustiva.
seo-description: Este artigo detalha as configurações do OSGi (listadas de acordo com o pacote) que são relevantes para a implementação do projeto. A lista atua como uma diretriz e não é exaustiva.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3806'
ht-degree: 0%

---


# Configurações do OSGi{#osgi-configuration-settings}

[](https://www.osgi.org/) O OSGi é um elemento fundamental na pilha de tecnologia de AEM. É usado para controlar os pacotes compostos de AEM e sua configuração.

O OSGi &quot;*fornece os primitivos padronizados que permitem que aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados*&quot;.

Isso permite o gerenciamento fácil de pacotes, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são manipuladas automaticamente. Cada componente OSGi (consulte a [Especificação OSGi](https://www.osgi.org/Specifications/HomePage)) está contido em um dos vários pacotes. Ao trabalhar com AEM, há vários métodos de gerenciamento das configurações desses pacotes; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

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
>A ferramenta Diff de configuração do OSGi, parte das [Ferramentas AEM](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html), pode ser usada para listar as configurações padrão do OSGi.

>[!NOTE]
>
>Podem ser necessários outros pacotes para áreas de funcionalidade específicas no AEM. Nesses casos, os detalhes de configuração podem ser encontrados na página relacionada à funcionalidade apropriada.

**AEM Replication Event** ListenerConfigure:

* O **Run Modes**, no qual os eventos de replicação serão distribuídos aos ouvintes. Por exemplo, se definido como autor, esse é o sistema que &quot;iniciará&quot; a replicação.

* O modo de execução **publish** precisa ser adicionado se o código do projeto processar eventos de replicação (replicação inversa) em um ambiente de publicação. Por exemplo, quando o dispatcher é usado para liberar do ambiente de publicação ou quando ocorre a replicação padrão para outras instâncias de publicação.

**AEM Repository change** listenerConfigure:

* Os **Caminhos** locais para acompanhar eventos de repositório prontos para distribuição.

**CRX Sling Client** RepositoryConfigure o acesso ao repositório de conteúdo subjacente.

* O **Admin Password** deve ser alterado após a instalação para garantir a [segurança](/help/sites-administering/security-checklist.md) da sua instância.
* Outras alterações não devem ser necessárias e devem ser tomadas precauções, pois podem afetar o acesso ao repositório.

**Wiki Mail** ServiceDefina as configurações de email para emails enviados por um wiki.

**Console de gerenciamento do Apache Felix OSGiConfigurar:** 

* **Plug-ins**, os principais itens de navegação (plug-ins do console) que estarão disponíveis no  **Apache Felix Web Management** Consoleas como itens de menu de nível superior. Desative qualquer item que não seja necessário, pois cada um requer espaço e recursos.

>[!CAUTION]
>
>Certifique-se de configurar o seguinte:
>
>**Nome** de usuário e  **senha**, as credenciais para acessar o próprio Apache Felix Web Management Console.
>A senha deve ser alterada após a instalação inicial para garantir a [segurança](/help/sites-administering/security-checklist.md) da sua instância.

>[!NOTE]
>
>Essa configuração deve ser feita usando o Felix Console, conforme necessário na inicialização - antes que o repositório esteja disponível.

**Apache Sling Customizable Request Data** LoggerConfigure:

* **Nome** do registrador e  **Formato** de log para configurar o local e o formato do registro de solicitação e acesso (padrão:  `request.log`). Esse arquivo de log é essencial ao analisar o desempenho ou a funcionalidade de depuração relacionada à cadeia da Web.
Isso é emparelhado com o [Apache Sling Request Logger](#apacheslingrequestlogger).

Para obter mais informações, consulte [AEM Registro](/help/sites-deploying/configure-logging.md) e [Registro de Sling](https://sling.apache.org/site/logging.html).

**Apache Sling Event Thread** PoolConfigurar:

* **Tamanho mín. do pool** e  **máx. do pool**, o tamanho do pool usado para conter encadeamentos de evento.

* **Tamanho da fila**, o tamanho máximo da fila de encadeamento se o pool estiver esgotado.
O valor recomendado é `-1`, pois isso define a fila como ilimitada; se um limite for definido, as perdas podem ocorrer quando ele for excedido.

* Alterar essas configurações pode ajudar no desempenho em cenários com um alto número de eventos; por exemplo, uso intenso de DAM ou Fluxo de trabalho AEM.
* Os valores específicos do seu cenário devem ser estabelecidos usando testes.
* Essas configurações podem afetar o desempenho da sua instância, portanto, não as altere sem motivo e consideração.

**Apache Sling GET** ServletConfigure alguns aspectos da renderização:

* **** Indexação automática do anexo ativar/desativar renderização de diretório para navegação.
* **Ative**  (ou desative) renderizações padrão, como  **HMTL**,  **Texto simples**,  **** JSONou  **XML**.
Você não deve desativar o JSON.

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar AEM no [Modo de Pronto para Produção](/help/sites-administering/production-ready.md).

**Apache Sling Java Script** HandlerConfigure as configurações para a compilação de arquivos .java como scripts (servlets).

Certas configurações podem afetar o desempenho, elas devem ser desativadas sempre que possível, principalmente para uma instância de produção.

* S **Source VM** e **Target VM**, defina a versão do JDK como a usada como JVM em tempo de execução

* para instâncias de produção:

   * desativar **Gerar Informações de Depuração**

**Instalador do Apache Sling JCR** Esses parâmetros provavelmente não precisam de configuração, mas podem ser úteis para saber quando desenvolver ou depurar. Por exemplo, a(s) pasta(s) de instalação pode(m) ser útil para fazer check-in/out ou criar um pacote.

* **Nome das pastas de instalação** re-expanda  **Profundidade máxima da hierarquia de pastas de instalação**  - especifique onde e a que profundidade as pastas do repositório são procuradas para que os recursos sejam instalados. Quando um curinga é usado (como em .*/install) todas as correspondências apropriadas serão pesquisadas, por exemplo, `/libs/sling/install` e `/libs/cq/core/install`.

* **Caminho** de pesquisa, lista de caminhos que o jcrinstall procura recursos a serem instalados, juntamente com um número que indica o fator de ponderação para esse caminho.

**Apache Sling Job Event** HandlerConfigurar parâmetros que gerenciam a programação de trabalhos:

* **Intervalo** de repetição,  **Máximo de Tentativas**,  **Máximo de Trabalhos Paralelos**,  **Tempo de Espera de Confirmação**, entre outros.

* Alterar essas configurações pode melhorar o desempenho em cenários com um alto número de tarefas; por exemplo, uso intenso de AEM DAM e workflows.
* Os valores específicos do seu cenário devem ser estabelecidos usando testes.
* Não altere essas configurações sem motivo, só sendo alterado após a devida consideração.

**Apache Sling JSP Script** HandlerConfigure as configurações relevantes para o desempenho do manipulador de script JSP. Para melhorar o desempenho, você deve desativar o máximo possível.

Em especial para instâncias de produção:

* desativar **Gerar Informações de Depuração**
* desative **Manter Java Gerado**
* desativar **Conteúdo Mapeado**
* desativar **Exibir Fragmentos de Origem**

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar AEM no [Modo de Pronto para Produção](/help/sites-administering/production-ready.md).

**Configuração** de registro do Apache SlingConfigure:

* **Log** Leveland  **Log File**, para definir o local e o nível de log da configuração central do log (error.log). O nível pode ser definido como `DEBUG`, `INFO`, `WARN`, `ERROR` e `FATAL`.

* **Número de** arquivos de log e  **limites de arquivo de** log para definir o tamanho e a rotação da versão do arquivo de log.

* **O** Padrão de mensagem define o formato das mensagens de log.

Para obter mais informações, consulte [AEM Registro](/help/sites-deploying/configure-logging.md#global-logging) e [Registro de Sling](https://sling.apache.org/site/logging.html).

**Configuração do Apache Sling Logging Logger (Configuração de Fábrica)** Configurar:

* **Nível de log**,  **Arquivo de** log e  **** Formatação de mensagem para definir detalhes do arquivo de log e das mensagens.

* **** Logger para definir a categoria; por exemplo, registre somente para com.day.cq.

* Ao usar **Configurações de fábrica**, qualquer número de configurações adicionais pode ser adicionado para atender aos vários níveis de log e categorias necessários.
* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens de TRACE para um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, ter mensagens sobre um serviço específico registradas em um arquivo de log individual para facilitar o monitoramento.

Para obter mais informações, consulte [AEM Registro](/help/sites-deploying/configure-logging.md) e [Registro de Sling](https://sling.apache.org/site/logging.html).

**Configuração do Apache Sling Logging Writer (Configuração de Fábrica)** Configurar:

* **Log** File para definir a existência de um arquivo de log.
* **Número de** arquivos de log para definir a rotação da versão.

* O gravador pode ser usado por uma configuração **Apache Sling Logging Logger Configuration**.

* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens de TRACE para um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, ter mensagens sobre um serviço específico registradas em um arquivo de log individual para facilitar o monitoramento.

Para obter mais informações, consulte [AEM Registro](/help/sites-deploying/configure-logging.md) e [Registro de Sling](https://sling.apache.org/site/logging.html).

**Apache Sling Main** ServletConfigure:

* **Número de chamadas por** solicitação e  **profundidade de** recursão para proteger seu sistema contra chamadas de recursão infinitas e de script excessivo.

**Apache Sling MIME Type** ServiceConfigure:

* **Tipos MIME** para adicionar os exigidos pelo seu projeto ao sistema. Isso permite que uma solicitação `GET` em um arquivo defina o cabeçalho de tipo de conteúdo correto para vincular o tipo de arquivo e o aplicativo.

**Apache Sling Referrer** FilterPara resolver problemas de segurança conhecidos com CSRF (Cross-Site Request Forgery) no CRX WebDAV e Apache Sling, é necessário configurar o filtro Referenciador .

O serviço de filtro do referenciador é um serviço OSGi que permite configurar:

* quais métodos http devem ser filtrados
* se um cabeçalho de referenciador vazio é permitido
* e uma lista de servidores a serem permitidos além do host do servidor.

Consulte a [Lista de verificação de segurança - Problemas com falsificação de solicitação entre sites](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obter mais detalhes.

>[!NOTE]
>
>O Apache Sling Referrer Filter depende da instalação de um pacote de correção rápida.

**Apache Sling Request** LoggerConfigure:

* vários parâmetros para definir como as solicitações são registradas.
* **Ative o Log de solicitações**, para ativar ou desativar.

* **Ative o Log de acesso** para ativar ou desativar.

Isso é emparelhado com o [Apache Sling Customizable Request Data Logger](#apacheslingcustomizablerequestdatalogger).

Para obter mais informações, consulte [AEM Registro](/help/sites-deploying/configure-logging.md) e [Registro de Sling](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver** FatoryConfigure os aspectos centrais da resolução de recursos do Sling:

* **Caminhos**(s) de pesquisa de recursos, adicione quaisquer caminhos específicos do projeto (mas não remova  `/libs` ou  `/apps`).

* **URLs virtuais** para definir os mapeamentos de URL personalizados.

* **Mapeamentos** de URL para definir aliases; por exemplo, de  `/content` a  `/`.

* **Localização do mapeamento**, a configuração do mapeador externalizada no  `/etc/map`.

* Use a instalação local (por exemplo, use `https://localhost:4502/system/console/jcrresolver`) para determinar qual Resolvedor de Recursos está ativo.

Para obter mais informações, consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Especificamente, essas opções devem ser configuradas no repositório.
>
>Caso contrário, as alterações feitas em **Mapeamentos de URL** usando o console Felix podem ser substituídas por AEM na próxima inicialização.

**Apache Sling Servlet/Script Resolver and Error** HandlerO Sling Servlet e o Script Resolver têm várias tarefas:

1. Ele é usado como o `ServletResolver` para selecionar o Servlet ou Script para chamar para lidar com a solicitação.

1. Atua como o `SlingScriptResolver`.

1. Ele gerencia a manipulação de erros ao implementar a interface `ErrorHandler` usando o mesmo algoritmo para selecionar servlets e scripts que manipulam erros, como é usado para resolver servlets e scripts de processamento de solicitações.

Vários parâmetros podem ser definidos, incluindo:

* **Os** Caminhos de execução listam os caminhos para procurar scripts executáveis; ao configurar caminhos específicos, você pode limitar quais scripts podem ser executados. Se nenhum caminho estiver configurado, o padrão será usado ( `/` = root), isso permitirá a execução de todos os scripts.
Se um valor de caminho configurado terminar com uma barra, a subárvore inteira será pesquisada. Sem essa barra à direita, o script só será executado se for uma correspondência exata.

* **Usuário do script**  - essa propriedade opcional pode especificar a conta de usuário do repositório usada para ler os scripts. Se nenhuma conta for especificada, o usuário `admin` será usado por padrão.

* **Extensões padrão** A lista de extensões para as quais o comportamento padrão será usado. Isso significa que o último segmento de caminho do tipo de recurso pode ser usado como o nome do script.

**Day Commons GFX Font** HelperAo renderizar gráficos, você pode usar DrawText para incorporar texto. Para isso, você também pode instalar suas próprias fontes:

* Defina o **Caminho da fonte** a ser pesquisado para procurar fontes específicas do projeto.
Por exemplo, `/apps/myapp/fonts`.

**Configuração** ConfigurationProxy de Componentes HTTP do Apache para todos os códigos que usam o cliente HTTP do Apache, usado quando um HTTP é feito; por exemplo, na replicação.

Ao criar uma nova configuração, não faça alterações na configuração de fábrica, mas crie uma nova configuração de fábrica para este componente usando o gerenciador de configuração disponível aqui: **https://localhost:4502/system/console/configMgr/**. A configuração de proxy está disponível em **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>No AEM 6.0 e versões anteriores, o proxy foi configurado no Day Commons HTTP Client. A partir AEM 6.1 e versões posteriores, a configuração de proxy foi movida para a &quot;Configuração de proxy de componentes HTTP do Apache&quot; em vez da configuração &quot;Cliente HTTP do Day Commons&quot;.

**Day CQ** AntispamConfigure o serviço antisspam (Akismet) usado. Isso requer que você registre o:

* **Provedor**
* **Chave da API**
* **URL registrado**

**Adobe Granite HTML Library** ManagerConfigure isso para controlar a manipulação de bibliotecas de clientes (css ou js); incluindo, por exemplo, como a estrutura subjacente é vista.

* Para instâncias de produção:

   * habilite **Minify** (para remover caracteres CRLF e espaço em branco).
   * habilite **Gzip** (para permitir que os arquivos sejam compactados e acessados com uma solicitação).
   * desativar **Depurar**
   * desativar **Tempo**

* Para desenvolvimento de JS (especialmente quando firebugging/debugging):

   * desativar **Minimizar**
   * habilite **Depurar** para separar os arquivos para depuração e uso com firebug.
   * ative **Timing** no caso de interesse em tempo.
   * ative o console **Debug** para ver as mensagens de log do console JS.

>[!CAUTION]
>
>Ao alterar a configuração para **Minimizar** ou **Gzip**, também será necessário excluir o conteúdo de `/var/clientlibs`. Esta é uma versão em cache das clientlibs e será recriada quando a próxima solicitação for feita.

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar AEM no [Modo de Pronto para Produção](/help/sites-administering/production-ready.md).

**Configurações gerais do Day CQ HTTP Header Authentication** HandlerSystem para o método de autenticação básico da solicitação HTTP.

Ao usar [grupos de usuários fechados](/help/sites-administering/cug.md) você pode configurar (entre outros):

* **Realm HTTP**
* A **Página de Logon Padrão**

**Day CQ Link Checker** ServiceCheck e, se necessário, configure:

* **Período do agendador** para definir o intervalo em que os links externos devem ser verificados automaticamente.

* Verifique **Bad Link Tolerance Interval** para o período após o qual um link externo malsucedido é considerado ruim.
* **Padrões** de substituição de verificação de link, para definir quaisquer caminhos a serem excluídos da verificação de link.

**Configurações do Day CQ Link Checker** TaskConfigure para uma única tarefa de verificador de link (uma tarefa que verifica um link externo):

* Verifique os intervalos definidos em **Good Link Test Interval** e **Bad Link Test Interval**

* Os vários parâmetros relacionados a proxies para acesso à Internet e NTLM que são necessários para acesso externo ao verificar um link.

**Day CQ Mail** ServiceConfigure o nome do host e os detalhes de acesso do servidor de email. Consulte a seção Configuração do serviço de email .

**Informativo do MCM CQ do diaConfigure as várias configurações usadas com o informativo.** 

**Mapeamento Raiz** do Day CQConfigure:

* **Target** Pathto define para onde uma solicitação para &quot;  `/`&quot; será redirecionada.

Há duas interfaces de usuário disponíveis no AEM:

* a interface de usuário habilitada para toque é a interface de usuário padrão
* e a interface clássica obsoleta ainda está totalmente operacional

Usando AEM Mapeamento de Raiz, você pode configurar a interface que deseja ter como padrão para sua instância:

* Para ter a interface habilitada para toque como a interface padrão, o **Caminho do Target** deve apontar para:

   ```
      /projects.html
   ```

* Para ter a interface clássica como a interface padrão, o **Caminho do Target** deve apontar para:

   ```
      /welcome.html
   ```

>[!NOTE]
>
>Em uma instalação padrão, a interface otimizada para toque é a interface padrão.

**Adobe Granite SSO Authentication** HandlerConfigurar detalhes de Single Sign On (SSO); geralmente, elas são necessárias em configurações de autor corporativo, geralmente em conjunto com o LDAP.

Várias propriedades de configuração estão disponíveis:

* ****
PathPath para o qual esse manipulador de autenticação está ativo. Se este parâmetro for deixado em branco, o manipulador de autenticação será desativado. Por exemplo, o caminho / faz com que o manipulador de autenticação seja usado para todo o repositório.

* **O valor Classificação do Serviço**
RankingOSGi Framework é usado para indicar a ordem usada para chamar este serviço. Isso é uma 
`int` , sempre que valores mais elevados designem uma precedência mais elevada.
O valor padrão é `0`.

* ****
Nomes de CabeçalhoOs nomes dos cabeçalhos que podem conter uma ID de usuário.

* ****
Nomes de cookiesOs nomes dos cookies que podem conter uma ID de usuário.

* ****
Nomes de ParâmetrosO(s) nome(s) dos parâmetros de solicitação que podem fornecer a ID do usuário.

* **User**
MapPara usuários selecionados, o nome de usuário extraído da solicitação HTTP pode ser substituído por um diferente no objeto de credenciais. O mapeamento é definido aqui. Se o nome do usuário 
`admin` for exibido em qualquer lado do mapa, o mapeamento será ignorado. Esteja ciente de que o caractere &quot;=&quot; deve ser evitado com um &quot;\&quot; à esquerda.

* ****
FormatoIndica o formato no qual a ID de usuário é fornecida. Uso:

   * `Basic` se a ID do usuário estiver codificada no formato HTTP Basic Authentication
   * `AsIs` se a ID de usuário for fornecida em texto simples ou qualquer expressão regular aplicada, o valor deve ser usado como está ou qualquer expressão regular

**** Filtro de depuração do WCM CQ do diaÉ útil no desenvolvimento, pois permite o uso de sufixos como ?debug=layout ao acessar uma página. Por exemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout fornecerá informações de layout que podem ser de interesse do desenvolvedor.

* Desative isso em instâncias de produção para garantir desempenho e segurança.

**Configuração do** filtro WCM CQ do dia:

* **Modo WCM **para definir o modo padrão.
* Em uma instância de autor, pode ser `edit`, `disable,preview` ou `analytics`.
Os outros modos podem ser acessados do sidekick, ou o sufixo `?wcmmode=disabled` pode ser usado para emular um ambiente de produção.

* Em uma instância de publicação, isso deve ser definido como `disabled` para garantir que nenhum outro modo esteja acessível.

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar AEM no [Modo de Pronto para Produção](/help/sites-administering/production-ready.md).

**Day CQ WCM Link Checker** ConfiguratorConfigurar:

* **Lista de** configurações de regravação para especificar uma lista de locais para configurações do linkchecker baseadas em conteúdo. As configurações podem ser baseadas no modo de execução; isso é importante para distinguir entre ambientes de autor e publicação, pois as configurações do linkchecker podem ser diferentes.

**Processador de página do WCM CQ do diaConfigurar:** 

* **Caminhos**, uma lista de locais em que o sistema escuta modificações de página antes de acionar um  `jcr:Event`.

**Adobe Page Impressions** TrackerPara uma instância de autor, configure:

* **sling.auth.requirements**: defina o valor dessa propriedade como  `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Essa configuração permitirá solicitações anônimas para o serviço de rastreamento.

>[!NOTE]
>
>Consulte [Impressões de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obter mais informações.

**Página** Estatísticas do WCM CQ do diaPara obter uma instância de publicação, configure:

* **URL para enviar** dados para configurar o URL usado para rastrear estatísticas de página (é vital se uma solicitação do rastreador passar pelo dispatcher); por exemplo, o padrão é  `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script de rastreamento** habilitado para ativar (  `true`) ou desativar (  `false`) a inclusão do script de rastreamento nas páginas. O valor padrão é `false`.

>[!NOTE]
>
>Consulte [Impressões de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obter mais informações.

**Day CQ WCM Version** ManagerControl se, e como, as versões são gerenciadas em seu sistema:

* **Criar versão na ativação**, ativada em uma instalação padrão
* **Habilitar limpeza**

* **Eliminar caminhos**, os caminhos que uma ação de pesquisa procurará
* **Caminhos** de controle de versão implícitos, os caminhos nos quais o controle de versão implícito está ativo.

* **Idade máxima da versão**, a idade máxima (em dias) de uma versão

* **Número máximo de versões**, o número máximo de versões a serem mantidas

Consulte [Limpeza de versão](/help/sites-deploying/version-purging.md) para obter mais informações.

**Day CQ Workflow Email Notification** ServiceConfigure as configurações de email para notificações enviadas por um workflow.

**Day CQSE HTTP** ServiceControl o CQ Servlet Engine:

* **NIO para HTTP, **Se deve ou não usar NIO para HTTP. O padrão é true. Usado somente se HTTP estiver habilitado.
* **Tempo limite da conexão, **Tempo limite da conexão em milissegundos. Essa propriedade se aplica às conexões HTTP e HTTPS. O padrão é 60 segundos.

* **Ative HTTPS** , se HTTPS estiver ou não ativada. O padrão é false.
* **Tempo limite da sessão**, tempo de vida padrão de uma sessão HTTP especificado em minutos. Se o tempo limite for 0 ou inferior, as sessões nunca expirarão. O padrão é 10 minutos.
* **Registro de Depuração**, Escreva ou não mensagens de nível DEBUG. O padrão é false.
* **Solicitar tamanho do buffer**, tamanho do buffer para solicitações em bytes. O padrão é 8 KB.
* **Número máximo de threads**, Número máximo de threads a serem usados para lidar com solicitações. O padrão é 200.

As seguintes propriedades só se aplicam se o HTTPS estiver ativado.

* **Porta** HTTPS, Porta para escuta de solicitação HTTPS. O padrão é 433.
* **NIO para HTTPS**, independentemente de usar ou não NIO para HTTP. O padrão é o valor da propriedade NIO for HTTP .
* **Armazenamento de chaves**, Caminho absoluto para o Armazenamento de chaves a ser usado para HTTPS. Obrigatório se HTTPS estiver ativado.
* **Senha do Armazenamento de chaves**, Senha para acessar o Armazenamento de chaves.
* **Alias da chave**, Alias da chave secreta no Armazenamento de chaves.
* **Senha** da chave, Senha para desbloquear a chave secreta no Armazenamento de chaves.
* **Certificado** do cliente, requisito para que o cliente forneça um certificado válido. O padrão é nenhum.

Consulte também [Ativando HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obter detalhes sobre as opções relacionadas ao SSL e uma descrição completa sobre como habilitar HTTPS para CQSE.

**Fábrica de analisador HTML de regravação do CQ**

Controla o analisador HTML para a reescrita do CQ.

* **Tags adicionais para processar**  - Você pode adicionar ou remover tags HTML para serem processadas pelo analisador. Por padrão, as seguintes tags são processadas: A,IMG,ÁREA,FORMULÁRIO,BASE,LINK,SCRIPT,CORPO,HEAD.
* **Preservar Camel Case**  - Por padrão, o analisador de HTML converte atributos em camel case (por exemplo, eBay) em minúsculas (por exemplo, ebay). Você pode desativar o para preservar os atributos de maiúsculas e minúsculas do camel. Isso é útil ao usar estruturas de primeiro plano, como o Angular 2.

**Day Commons JDBC Connections** PoolConfigure o acesso a um banco de dados externo que está sendo usado como uma fonte de conteúdo.

Esta é uma configuração de fábrica, portanto várias instâncias podem ser configuradas.

**Adobe CQ Media DPS Sessions** ServiceGerencie Sessões DPS para uso com Publicações.

Em particular, você pode definir o `dps.session.service.url.name`: o padrão está definido como [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN** RewriterA comunicação entre o AEM e uma CDN deve ser assegurada para que os ativos/binários sejam entregues ao usuário final de forma segura. Isso envolve duas tarefas:

* Acessar o recurso do AEM por meio da CDN na primeira vez (ou após expirar no cache).
* Acessar o recurso armazenado em cache no CDN com segurança, pois uma vez que o recurso é armazenado em cache no CDN, a solicitação não irá para o AEM e todos os usuários que têm acesso a esse recurso no devem ser fornecidos do CDN.

AEM fornece um regravador para regravar URLs de ativos internos em URLs CDN externos. Ele reescreve links a serem passados para a CDN, incluindo uma assinatura JWS e expira o tempo para permitir que o ativo seja acessado com segurança. Esse recurso deve ser usado em instâncias do autor.

O fluxo global é o seguinte:

1. O usuário é autenticado com AEM e solicita uma página com ativos.
1. A página solicitada contém um ativo semelhante a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. O regravador transforma o link para um URL CDN contendo uma Assinatura JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. O navegador do usuário encaminha a solicitação de ativo para o servidor CDN
1. O CDN deve ser configurado para encaminhar a solicitação para AEM junto com o parâmetro `cdn_sign`.
1. Um Manipulador de Autenticação valida o parâmetro `cdn_sign` e retorna o ativo ao CDN, que é então entregue ao usuário

O fluxo entre o navegador do usuário, o CDN e o AEM pode ser visualizado da seguinte maneira.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>No momento, esse recurso é ativado apenas para instâncias AEM autor.

**** CDNConfigServiceImplFornece configurações de CDN

O recurso de regravação de CDN pode ser ativado fornecendo **CDN distribution domain name** na configuração para com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

O serviço também contém outras opções de configuração, como ativar/desativar a reescrita de CDN, prefixos de caminho para os quais a reescrita de CDN é executada, valores TTL e protocolo (HTTP ou HTTPS).

**** CDNRewriterUma regravação para regravar URLs de imagem interna em URLs CDN

O valor **Tag Attributes** em com.adobe.cq.cdn.rewriter.impl.CDNRewriter pode ser definido para que somente os links de imagem seletiva sejam regravados.

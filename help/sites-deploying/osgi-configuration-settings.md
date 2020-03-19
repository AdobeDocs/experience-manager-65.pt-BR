---
title: Configurações do OSGi
seo-title: Configurações do OSGi
description: Este artigo detalha as configurações do OSGi (listadas de acordo com o pacote) que são relevantes para a implementação do projeto. A lista atua como orientação e não é exaustiva.
seo-description: Este artigo detalha as configurações do OSGi (listadas de acordo com o pacote) que são relevantes para a implementação do projeto. A lista atua como orientação e não é exaustiva.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
translation-type: tm+mt
source-git-commit: 0849cfdd0e4f9a614c455214e6520ead07ae6da0

---


# Configurações do OSGi{#osgi-configuration-settings}

[O OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia do AEM. É usado para controlar os pacotes compostos do AEM e suas configurações.

O OSGi &quot;*fornece as primitivas padronizadas que permitem que os aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados*&quot;.

Isso permite o gerenciamento fácil de pacotes, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são tratadas automaticamente. Cada componente OSGi (consulte a Especificação [](https://www.osgi.org/Specifications/HomePage)OSGi) está contido em um dos vários pacotes. When working with AEM there are several methods of managing the configuration settings for such bundles; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

As seguintes configurações OSGi (listadas de acordo com o pacote) são relevantes para a implementação do projeto. Nem todas as configurações listadas precisam de ajuste, algumas são mencionadas para ajudá-lo a entender como o AEM opera.

>[!CAUTION]
>
>A lista destina-se a servir de orientação e não é exaustiva. Nem todos os pacotes são listados, nem todos os parâmetros para alguns dos pacotes que são.
>
>A configuração necessária varia de projeto para projeto.
>
>Consulte o console da Web para obter os valores usados e informações detalhadas sobre os parâmetros.

>[!NOTE]
>
>A ferramenta Dif de configuração do OSGi, parte das Ferramentas [do](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)AEM, pode ser usada para listar as configurações padrão do OSGi.

>[!NOTE]
>
>Outros pacotes podem ser necessários para áreas específicas de funcionalidade no AEM. Nesses casos, os detalhes de configuração podem ser encontrados na página relacionada à funcionalidade apropriada.

**Configuração do ouvinte** de eventos de replicação do AEM:

* Os modos **de** execução, nos quais os eventos de replicação serão distribuídos aos ouvintes. Por exemplo, se definido como autor, esse é o sistema que &quot;iniciará&quot; a replicação.

* A **publicação** do modo de execução precisa ser adicionada se o código do projeto processar eventos de replicação (replicação reversa) em um ambiente de publicação. Por exemplo, quando o dispatcher é usado para liberar do ambiente de publicação ou quando ocorre replicação padrão para outras instâncias de publicação.

**AEM Repository change listener** Configurar:

* Os **Caminhos**, os locais para acompanhar os eventos do repositório prontos para distribuição.

**Repositório** do cliente Sling CRX Configure o acesso ao repositório de conteúdo subjacente.

* A senha **de** administrador deve ser alterada após a instalação para garantir a [segurança](/help/sites-administering/security-checklist.md) da sua instância.
* Outras alterações não devem ser necessárias e devem ser tomadas precauções, uma vez que podem afetar o acesso ao repositório.

**Serviço** Wiki Mail Configure as configurações de email para emails enviados por um wiki.

**Configuração do console** de gerenciamento do Apache Felix OSGi:

* **Plug-ins**, os itens de navegação principais (plug-ins do console) estarão disponíveis no console **de gerenciamento da Web do** Apache Felix como itens de menu de nível superior. Desative qualquer item de que você não precise, pois cada um requer espaço e recursos.

>[!CAUTION]
>
>Certifique-se de configurar o seguinte:
>
>**Nome** de usuário e **senha**, as credenciais para acessar o Console de gerenciamento da Web do Apache Felix.
>A senha deve ser alterada após a instalação inicial para garantir a [segurança](/help/sites-administering/security-checklist.md) da sua instância.

>[!NOTE]
>
>Essa configuração deve ser feita usando o Console do Felix, conforme necessário na inicialização - antes que o repositório esteja disponível.

**Configuração do Registrador** de Dados de Solicitação Personalizável do Apache Sling:

* **Nome** do registrador e Formato **de** log para configurar o local e o formato do registro de solicitação e acesso (padrão: `request.log`). Esse arquivo de log é essencial ao analisar o desempenho ou a funcionalidade de depuração relacionada à cadeia da Web.
Isso é emparelhado com o [Apache Sling Request Logger](#apacheslingrequestlogger).

Para obter mais informações, consulte Registro [de AEM e Registro de](/help/sites-deploying/configure-logging.md) Sling [](https://sling.apache.org/site/logging.html).

**Apache Sling Event Thread Pool** Configurar:

* **Tamanho** mín. do pool e Tamanho **** máx. do pool, o tamanho do pool usado para armazenar threads de evento.

* **Tamanho**da fila, o tamanho máximo da fila de encadeamento se o pool estiver esgotado.
O valor recomendado é definido `-1` como ilimitado; se um limite for definido, as perdas podem ocorrer quando for excedido.

* A alteração dessas configurações pode ajudar no desempenho em cenários com um grande número de eventos; por exemplo, uso intenso do AEM DAM ou Fluxo de trabalho.
* Valores específicos do seu cenário devem ser estabelecidos por meio de testes.
* Essas configurações podem afetar o desempenho da sua instância, portanto, não as altere sem motivo e consideração.

**Apache Sling GET Servlet** Configure alguns aspectos da renderização:

* **Índice** automático para ativar/desativar a renderização de diretório para navegação.
* **Ative** (ou desative) execuções padrão, como **HMTL**, **Texto** simples, **JSON** ou **XML**.
Você não deve desativar o JSON.

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar o AEM no modo [](/help/sites-administering/production-ready.md)Production Ready.

**Apache Sling Java Script Handler** Define as configurações para a compilação de arquivos .java como scripts (servlets).

Determinadas configurações podem afetar o desempenho; elas devem ser desativadas sempre que possível, principalmente para uma instância de produção.

* VM **de** origem e VM **de** destino, defina a versão do JDK como a usada como JVM de tempo de execução

* para instâncias de produção:

   * desativar **Gerar informações de depuração**

**Apache Sling JCR Installer** Estes parâmetros provavelmente não precisam de configuração, mas podem ser úteis para saber ao desenvolver ou depurar. Por exemplo, as pastas de instalação podem ser úteis para fazer check-in/check-out ou criar um pacote.

* **Pastas de instalação nomeiam regexp** e profundidade de hierarquia **máxima de pastas** de instalação - especifica onde e em que profundidade as pastas do repositório são pesquisadas para que os recursos sejam instalados. Quando um curinga é usado (como em .*/install) todas as correspondências apropriadas serão pesquisadas, por exemplo, `/libs/sling/install` e `/libs/cq/core/install`.

* **Caminho** de pesquisa, a lista de caminhos que o jcrinstall pesquisa os recursos a serem instalados, juntamente com um número que indica o fator de ponderação para esse caminho.

**Manipulador** de eventos de trabalho Apache Sling Configure parâmetros que gerenciam a programação de trabalhos:

* **Intervalo** de tentativas, **Máximo de tentativas**, **Máximo de trabalhos** paralelos, Tempo **de espera de** reconhecimento, entre outros.

* A alteração dessas configurações pode melhorar o desempenho em cenários com um alto número de trabalhos; por exemplo, uso intenso do AEM DAM e fluxos de trabalho.
* Valores específicos do seu cenário devem ser estabelecidos por meio de testes.
* Não altere essas configurações sem motivo, só altere após a devida consideração.

**Apache Sling JSP Script Handler** Define as configurações relevantes de desempenho para o manipulador de scripts JSP. Para melhorar o desempenho, você deve desativar o máximo possível.

Em especial, para as instâncias de produção:

* desativar **Gerar informações de depuração**
* desativar **Manter Java Gerado**
* desativar conteúdo **mapeado**
* desativar fragmentos **de origem de exibição**

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar o AEM no modo [](/help/sites-administering/production-ready.md)Production Ready.

**Configuração** de registro do Apache Sling Configurar:

* **Nível** de log e Arquivo **** de log, para definir o local e o nível de log da configuração central de log (error.log). O nível pode ser definido como um de `DEBUG`, `INFO`, `WARN`, `ERROR` e `FATAL`.

* **Número de Arquivos** de Log e Limite **de Arquivo de** Log para definir o tamanho e a rotação da versão do arquivo de log.

* **O padrão** de mensagem define o formato das mensagens de registro.

Para obter mais informações, consulte Registro [de AEM e Registro de](/help/sites-deploying/configure-logging.md#global-logging) Sling [](https://sling.apache.org/site/logging.html).

**Configuração do Apache Sling Logging Logger (Configuração de fábrica)** Configurar:

* **Nível** de log, Arquivo **de** log e Formato **de** mensagem para definir detalhes do arquivo de log e das mensagens.

* **Logger** para definir a categoria; por exemplo, registre apenas com.day.cq.

* Usando Configurações **de** fábrica, qualquer número de configurações adicionais pode ser adicionado para atender aos vários níveis e categorias de log necessários.
* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens TRACE de um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, para que mensagens sobre um serviço específico sejam registradas em um arquivo de log individual para facilitar o monitoramento.

Para obter mais informações, consulte Registro [de AEM e Registro de](/help/sites-deploying/configure-logging.md) Sling [](https://sling.apache.org/site/logging.html).

**Configuração do Apache Sling Logging Writer (Configuração de fábrica)** Configurar:

* **Arquivo** de log para definir a existência de um arquivo de log.
* **Número de Arquivos** de Log para definir a rotação da versão.

* O gravador pode ser usado por uma configuração **** do Apache Sling Logging Logger.

* Essas configurações são úteis durante o desenvolvimento; por exemplo, para registrar mensagens TRACE de um serviço específico em um arquivo de log específico.
* Essas configurações são úteis em um ambiente de produção; por exemplo, para que mensagens sobre um serviço específico sejam registradas em um arquivo de log individual para facilitar o monitoramento.

Para obter mais informações, consulte Registro [de AEM e Registro de](/help/sites-deploying/configure-logging.md) Sling [](https://sling.apache.org/site/logging.html).

**Configuração principal do servlet** Apache Sling:

* **Número de Chamadas por Solicitação** e Profundidade **de** Recorrência para proteger seu sistema contra chamadas de recursão infinitas e chamadas de script excessivas.

**Apache Sling MIME Type Service** Configure:

* **Tipos** MIME para adicionar os necessários ao seu projeto ao sistema. Isso permite que uma `GET` solicitação em um arquivo defina o cabeçalho correto do tipo de conteúdo para vincular o tipo de arquivo e o aplicativo.

**Filtro** de referenciador Apache Sling Para resolver problemas de segurança conhecidos com o CSRF (Cross-Site Request Forgery) no CRX WebDAV e Apache Sling, é necessário configurar o filtro Referenciador.

O serviço de filtro do referenciador é um serviço OSGi que permite configurar:

* quais métodos http devem ser filtrados
* se um cabeçalho de referenciador vazio é permitido
* e uma lista branca de servidores a serem permitidos além do host do servidor.

Consulte a Lista de verificação de [segurança - Problemas com falsificação](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) de solicitação entre sites para obter mais detalhes.

>[!NOTE]
>
>O Filtro de referência Apache Sling depende da instalação de um pacote de correção rápida.

**Configuração do Registrador** de Solicitações do Apache Sling:

* vários parâmetros para definir como as solicitações são registradas.
* **Ative o Log** de solicitações para ativar ou desativar.

* **Ative o Log** de acesso para ativar ou desativar.

Isso é emparelhado com o [Apache Sling Customizable Request Data Logger](#apacheslingcustomizablerequestdatalogger).

Para obter mais informações, consulte Registro [de AEM e Registro de](/help/sites-deploying/configure-logging.md) Sling [](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver Fatory** Configurar aspectos centrais da resolução de recursos Sling:

* **Caminhos** de pesquisa de recursos, adicione quaisquer caminhos específicos do projeto (mas não remova `/libs` ou `/apps`).

* **URLs** virtuais para definir seus mapeamentos de URL personalizados.

* **Mapeamentos** de URL para definir qualquer alias; por exemplo, de `/content` para `/`.

* **Localização** de mapeamento, a configuração do mapeador externalizada em `/etc/map`.

* Use a instalação local (por exemplo, use `https://localhost:4502/system/console/jcrresolver`) para determinar qual Resolvedor de recursos está ativo.

Para obter mais informações, consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Em particular, essas opções devem ser configuradas no repositório.
>
>Caso contrário, as alterações feitas nos Mapeamentos **de** URL usando o console do Felix podem ser substituídas pelo AEM na próxima inicialização.

**Apache Sling Servlet/Script Resolver e Error Handler** O Sling Servlet e o Script Resolver têm várias tarefas:

1. É usado como o `ServletResolver` para selecionar o Servlet ou Script para chamar para lidar com a solicitação.

1. Funciona como o `SlingScriptResolver`.

1. Ele gerencia a manipulação de erros ao implementar a `ErrorHandler` interface usando o mesmo algoritmo para selecionar servlets e scripts que manipulam erros, usados para resolver servlets e scripts de processamento de solicitações.

Vários parâmetros podem ser definidos, incluindo:

* **Os Caminhos** de execução listam os caminhos para procurar scripts executáveis; ao configurar caminhos específicos, você pode limitar quais scripts podem ser executados. Se nenhum caminho estiver configurado, o padrão será usado ( `/` = raiz), isso permitirá a execução de todos os scripts.
Se um valor de caminho configurado terminar com uma barra, a subárvore inteira será pesquisada. Sem essa barra, o script só será executado se for uma correspondência exata.

* **Usuário** de script - essa propriedade opcional pode especificar a conta de usuário do repositório usada para ler os scripts. Se nenhuma conta for especificada, o `admin` usuário será usado por padrão.

* **Extensões** padrão A lista de extensões para as quais o comportamento padrão será usado. Isso significa que o último segmento de caminho do tipo de recurso pode ser usado como o nome do script.

**Auxiliar** de fonte Day Commons GFX Ao renderizar gráficos, você pode usar DrawText para incorporar texto. Para isso, você também pode instalar suas próprias fontes:

* Defina o Caminho **da** fonte a ser pesquisado para fontes específicas do projeto.
Por exemplo, `/apps/myapp/fonts`.

**Configuração** Proxy de Configuração de Componentes HTTP Apache para todos os códigos usando o cliente HTTP Apache, usado quando um HTTP é feito; por exemplo, na replicação.

Ao criar uma nova configuração, não faça alterações na configuração de fábrica, mas crie uma nova configuração de fábrica para este componente usando o gerenciador de configuração disponível aqui: **https://localhost:4502/system/console/configMgr/**. A configuração do proxy está disponível em **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>No AEM 6.0 e versões anteriores, o proxy foi configurado no Cliente HTTP Day Commons. A partir do AEM 6.1 e versões posteriores, a configuração de proxy foi movida para a configuração de proxy &quot;Configuração de componentes HTTP do Apache&quot; em vez da configuração &quot;Cliente HTTP do Day Commons&quot;.

**Dia Antispam** CQ Configure o serviço antisspam (Akismet) usado. Isso requer que você registre o:

* **Provedor**
* **Chave da API**
* **URL registrado**

**Gerenciador** de biblioteca HTML do Adobe Granite Configure isso para controlar a manipulação de bibliotecas de clientes (css ou js); incluindo, por exemplo, a forma como a estrutura subjacente é vista.

* Para instâncias de produção:

   * habilitar **Minify** (para remover caracteres CRLF e espaços em branco).
   * habilite o **Gzip** (para permitir que os arquivos sejam compactados e acessados com uma solicitação).
   * desativar **Depuração**
   * desativar **tempo**

* Para o desenvolvimento de JS (especialmente quando firebugging/debugging):

   * desativar **Minify**
   * ative **Depuração** para separar os arquivos para depuração e uso com firebug.
   * ativar **Timing** no caso de interesse em timing.
   * habilite o console **de depuração** para ver as mensagens de log do console JS.

>[!CAUTION]
>
>Ao alterar a configuração para **Minify** ou **Gzip** , também será necessário excluir o conteúdo do `/var/clientlibs`. Esta é uma versão em cache das clientlibs e será recriada quando for solicitado.

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar o AEM no modo [](/help/sites-administering/production-ready.md)Production Ready.

**Manipulador** de Autenticação do Cabeçalho HTTP do Dia CQ Configurações gerais do sistema para o método de autenticação básico da solicitação HTTP.

Ao usar grupos [de usuários](/help/sites-administering/cug.md) fechados, você pode configurar (entre outros):

* **Realm HTTP**
* A página de logon **padrão**

**Verificação de serviço** do Verificador de links CQ de dia e, se necessário, configure:

* **Período** do Agendador para definir o intervalo no qual os links externos devem ser verificados automaticamente.

* Verifique o Intervalo **de tolerância de link** incorreto para o período após o qual um link externo malsucedido é considerado incorreto.
* **Padrões** de substituição de verificação de link para definir quaisquer caminhos a serem excluídos da verificação de link.

**Tarefa** do Verificador de links CQ de dia Defina as configurações de uma única tarefa do verificador de links (uma tarefa que verifica um link externo):

* Verifique os intervalos definidos em Intervalo **de teste de link** bom e Intervalo de teste de link **incorreto**

* Os vários parâmetros relacionados aos proxies para acesso à Internet e ao NTLM necessários para acesso externo ao verificar um link.

**Serviço** de e-mail do CQ de Dia Configure o nome do host e os detalhes de acesso do servidor de e-mail. Consulte a seção Configuração do serviço de e-mail.

**Newsletter Day CQ MCM** Configure as várias configurações usadas com o boletim informativo.

**Configuração do mapeamento** raiz do Day CQ:

* **Caminho** do Target para definir para onde uma solicitação para &quot; `/`&quot; será redirecionada.

Há duas interfaces de usuário disponíveis no AEM:

* a interface do usuário habilitada para toque é a interface padrão
* e a interface clássica obsoleta ainda está totalmente operacional

Usando o Mapeamento raiz do AEM, você pode configurar a interface que deseja ter como padrão para sua instância:

* Para que a interface do usuário habilitada para toque seja a interface padrão, o Caminho **do** Target deve apontar para:

   ```
      /projects.html
   ```

* Para ter a interface clássica como a interface padrão, o Caminho **do** Target deve apontar para:

   ```
      /welcome.html
   ```

>[!NOTE]
>
>Em uma instalação padrão, a interface otimizada ao toque é a interface padrão.

**Adobe Granite SSO Authentication Handler** Configurar detalhes do Single Sign On (SSO); essas configurações são frequentemente necessárias em configurações de autor corporativo, geralmente em conjunto com LDAP.

Várias propriedades de configuração estão disponíveis:

* **Caminho** Caminho para o qual o manipulador de autenticação está ativo. Se esse parâmetro for deixado em branco, o manipulador de autenticação será desativado. Por exemplo, o caminho / faz com que o manipulador de autenticação seja usado para todo o repositório.

* **O valor de classificação de serviço** OSGi Framework é usado para indicar a ordem usada para chamar esse serviço. Esse é um `int` valor em que valores mais altos designam precedência mais alta.
O valor padrão é `0`.

* **Nomes** do cabeçalhoOs nomes dos cabeçalhos que podem conter uma ID de usuário.

* **Nomes de cookies** Os nomes dos cookies que podem conter uma ID de usuário.

* **Nomes** de parâmetros O nome dos parâmetros de solicitação que podem fornecer a ID do usuário.

* **Mapa** de usuário Para usuários selecionados, o nome de usuário extraído da solicitação HTTP pode ser substituído por outro no objeto de credenciais. O mapeamento é definido aqui. Se o nome de usuário `admin` for exibido em ambos os lados do mapa, o mapeamento será ignorado. Lembre-se de que o caractere &quot;=&quot; deve ser escapado com um &quot;\&quot; à esquerda.

* **Formato** Indica o formato no qual a ID de usuário é fornecida. Uso:

   * `Basic` se a ID do usuário estiver codificada no formato HTTP Basic Authentication
   * `AsIs` se a ID do usuário for fornecida em texto sem formatação ou qualquer expressão regular aplicada, o valor deve ser usado como está ou como qualquer expressão regular

**Filtro** de Depuração do WCM CQ de Diaútil ao desenvolver, pois permite o uso de sufixos como ?debug=layout ao acessar uma página. Por exemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout fornecerá informações de layout que podem ser de interesse para o desenvolvedor.

* Desative isso nas instâncias de produção para garantir o desempenho e a segurança.

**Configuração do filtro** WCM CQ do dia:

* **Modo WCM **para definir o modo padrão.
* Em uma instância do autor, isso pode ser `edit`, `disable,preview` ou `analytics`.
Os outros modos podem ser acessados do sidekick, ou o sufixo `?wcmmode=disabled` pode ser usado para emular um ambiente de produção.

* Em uma instância de publicação, isso deve ser definido `disabled` para garantir que nenhum outro modo seja acessível.

>[!NOTE]
>
>Essa configuração é configurada automaticamente para instâncias de produção se você executar o AEM no modo [](/help/sites-administering/production-ready.md)Production Ready.

**Configuração do Verificador** de links do Day CQ WCM:

* **Lista de configurações** de regravação para especificar uma lista de locais para configurações do verificador de links baseadas em conteúdo. As configurações podem ser baseadas no modo de execução; isso é importante para distinguir entre ambientes de autor e publicação, pois as configurações do verificador de links podem ser diferentes.

**Dia CQ WCM Página Processador** Configuração:

* **Caminhos**, uma lista de locais onde o sistema escuta modificações de página antes de acionar uma `jcr:Event`.

**Adobe Page Impressions Tracker** Para uma instância do autor, configure:

* **sling.auth.requirements**: defina o valor dessa propriedade como `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Essa configuração permitirá solicitações anônimas ao serviço de rastreamento.

>[!NOTE]
>
>Consulte Impressões [da](/help/sites-deploying/configuring.md#enabling-page-impressions) página para obter mais informações.

**Estatísticas** de página WCM do Day CQ Para uma instância de publicação, configure:

* **URL para enviar dados** para configurar o URL usado para rastrear as estatísticas da página (é vital se uma solicitação do rastreador passar pelo dispatcher); por exemplo, o padrão é `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script de rastreamento habilitado** para ativar ( `true`) ou desativar ( `false`) a inclusão do script de rastreamento nas páginas. O valor padrão é `false`.

>[!NOTE]
>
>Consulte Impressões [da](/help/sites-deploying/configuring.md#enabling-page-impressions) página para obter mais informações.

**Controle do Day CQ WCM Version Manager** se, e como, as versões são gerenciadas no seu sistema:

* **Criar versão na ativação**, ativada em uma instalação padrão
* **Ativar Expurgação**

* **Expurgar caminhos**, os caminhos que uma ação de pesquisa procurará
* **Caminhos** de controle de versão implícitos, os caminhos nos quais o controle de versão implícito está ativo.

* **Idade** máxima da versão, a idade máxima (em dias) de uma versão

* **Número máximo de versões**, o número máximo de versões a serem mantidas

Consulte Expurgação [de](/help/sites-deploying/version-purging.md) versão para obter mais informações.

**Serviço** de notificação por e-mail do Fluxo de Trabalho do CQ de Dia Configure as configurações de e-mail para notificações enviadas por um fluxo de trabalho.

**Serviço** HTTP CQSE Controle o Mecanismo Servlet CQ:

* **NIO para HTTP, **Se usar ou não o NIO para HTTP. O padrão é true. Usado somente se HTTP estiver ativado.
* **Tempo limite da conexão, **Tempo limite da conexão em milissegundos. Essa propriedade se aplica às conexões HTTP e HTTPS. O padrão é 60 segundos.

* **Ative HTTPS,** independentemente de HTTPS estar ou não ativado. O padrão é false.
* **Tempo limite** da sessão, duração padrão de uma sessão HTTP especificada em minutos. Se o tempo limite for 0 ou menor, as sessões nunca atingirão o tempo limite. O padrão é 10 minutos.
* **Registro** de Depuração, se deve ou não gravar mensagens de nível DEBUG. O padrão é false.
* **Tamanho** do buffer de solicitação, Tamanho do buffer para solicitações em bytes. O padrão é 8 KB.
* **Número máximo de threads**, número máximo de threads a serem usados para lidar com solicitações. O padrão é 200.

As seguintes propriedades só se aplicam se HTTPS estiver ativado.

* **Porta** HTTPS, Porta para acompanhar a solicitação HTTPS. O padrão é 433.
* **NIO para HTTPS**, se deve ou não usar NIO para HTTP. O padrão é o valor da propriedade NIO para HTTP.
* **Keystore**, caminho absoluto para o Keystore a ser usado para HTTPS. Obrigatório se HTTPS estiver ativado.
* **Senha** do armazenamento de chaves, Senha para acessar o armazenamento de chaves.
* **Alias**-chave, Alias da chave secreta no Keystore.
* **Senha** da chave, Senha para desbloquear a chave secreta no Keystore.
* **Certificado** do cliente, requisito para que o cliente forneça um certificado válido. O padrão é nenhum.

Consulte também [Habilitando HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obter detalhes sobre as opções relacionadas ao SSL e uma descrição completa sobre como habilitar HTTPS para CQSE.

**Fábrica de Analisadores HTML do CQ Rewriter**

Controla o Analisador HTML para o gravador de CQ.

* **Tags adicionais a serem processadas** - você pode adicionar ou remover tags HTML a serem processadas pelo analisador. Por padrão, as seguintes tags são processadas: A,IMG,ÁREA,FORMULÁRIO,BASE,LINK,SCRIPT,CORPO,CABEÇALHO.
* **Preservar caso** de Camel - Por padrão, o analisador HTML converte atributos em caso de camelo (por exemplo, eBay) em minúsculas (por exemplo, ebay). Você pode desativar isso para preservar os atributos de maiúsculas e minúsculas do camelo. Isso é útil ao usar estruturas de front-end como Angular 2.

**Pool** de conexões JDBC por dia comum Configure o acesso a um banco de dados externo que está sendo usado como fonte de conteúdo.

Esta é uma configuração de fábrica, portanto várias instâncias podem ser configuradas.

**O Adobe CQ Media DPS Sessions Service** Gerencia Sessões da DPS para uso com Publicações.

Em particular, você pode definir o `dps.session.service.url.name`: o padrão está definido como [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**A comunicação de gravador** CDN entre o AEM e um CDN deve ser assegurada para que os ativos/binários sejam entregues ao usuário final de forma segura. Isso envolve duas tarefas:

* Acessar o recurso do AEM pela primeira vez (ou após expirar em cache) por meio do CDN.
* Acessar o recurso armazenado em cache no CDN com segurança, pois assim que o recurso for armazenado em cache no CDN, a solicitação não irá para o AEM e todos os usuários que tiverem acesso a esse recurso devem ser atendidos a partir do CDN.

O AEM fornece um regravador para regravar URLs de ativos internos em URLs CDN externos. Ele regrava links para serem transmitidos ao CDN, incluindo uma assinatura JWS e expira no tempo para permitir que o ativo seja acessado com segurança. Esse recurso deve ser usado em instâncias do autor.

O fluxo global é o seguinte:

1. O usuário é autenticado no AEM e solicita uma página com ativos.
1. A página solicitada contém um ativo semelhante a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. O Rewriter transforma o link em um URL CDN contendo uma Assinatura JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. O navegador do usuário encaminha a solicitação de ativo para o servidor CDN
1. O CDN deve ser configurado para encaminhar a solicitação para o AEM juntamente com o `cdn_sign` parâmetro.
1. Um Manipulador de autenticação valida o `cdn_sign` parâmetro e retorna o ativo ao CDN, que é então entregue ao usuário

O fluxo entre o navegador do usuário, o CDN e o AEM pode ser visualizado da seguinte maneira.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>No momento, esse recurso está habilitado apenas para instâncias de autor de AEM.

**CDNConfigServiceImpl** fornece configurações de CDN

O recurso de regravação de CDN pode ser ativado fornecendo o nome **de domínio de distribuição de** CDN na configuração para com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

O serviço também contém outras opções de configuração como ativar/desativar a regravação de CDN, prefixos de caminho para os quais a regravação de CDN é executada, valores TTL e protocolo (HTTP ou HTTPS).

**CDNRewriter** Um regravador para regravar URLs de imagem interna para URLs CDN

O valor Atributos **de** tag em com.adobe.cq.cdn.rewriter.impl.CDNRewriter pode ser definido para que somente os links de imagem seletivos sejam regravados.

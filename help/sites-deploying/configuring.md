---
title: Conceitos básicos de configuração
description: Saiba como configurar o Adobe Experience Manager para seus próprios requisitos específicos.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 0%

---

# Conceitos básicos de configuração{#basic-configuration-concepts}

O Adobe Experience Manager (AEM) é instalado com configurações padrão para todos os parâmetros que permitem sua execução imediata. No entanto, você pode configurar o AEM para seus próprios requisitos específicos.

Há muitos aspectos do AEM que podem ser configurados:

* Alguns são [normalmente configurados para cada instalação de projeto](#primary-configuration-considerations) e devem ser revisados para confirmar se são aplicáveis ao seu projeto.
* [Outras configurações](#further-configuration-considerations) podem ser comuns, mas não imperativas; estão relacionadas a recursos ou ao desempenho e estabilidade do sistema.
* Outros são necessários apenas para determinados recursos opcionais do AEM (eles são documentados junto com o recurso apropriado).

Dependendo da configuração específica, essas alterações podem ser feitas usando:

* **Console da Web do Adobe CQ**

  Este é um local padrão para configurar pacotes e serviços OSGi.

  Consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e práticas recomendadas.

* **Repositório**

  Um subconjunto de configurações OSGi está disponível no repositório. Isso garante que copiar ou replicar o conteúdo do repositório recrie configurações idênticas. Você também pode adicionar suas próprias configurações, dependendo do modo de execução, ao repositório.

  Consulte [Configuração OSGi no Repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) e, em particular, [Adicionando uma Nova Configuração ao Repositório](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) para obter mais detalhes.

* **Sistema de arquivos**

  Alguns arquivos de configuração residem no sistema de arquivos.

* **WCM do AEM**

  Vários aspectos podem ser configurados no próprio AEM WCM, muitos usando o console [Ferramentas](/help/sites-administering/tools-consoles.md); por exemplo, agentes de replicação.

>[!NOTE]
>
>Ao trabalhar com o Adobe Experience Manager, há vários métodos de gerenciamento das definições de configuração para serviços OSGi (nós do console ou do repositório).
>
>Consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

>[!NOTE]
>
>A configuração do AEM é simples. No entanto, determinadas alterações podem ter um grande impacto nos aplicativos. Por esse motivo, verifique se você tem a experiência e o conhecimento necessários antes de começar a configurar o AEM e faça apenas as alterações que você sabe que são necessárias. Quaisquer alterações feitas pelo console OSGi são **imediatamente** aplicadas ao sistema em execução (não é necessário reiniciar).

## Considerações sobre a configuração principal {#primary-configuration-considerations}

Esta lista detalha as áreas principais que são comumente configuradas para cada novo projeto. Nem todos são necessários, mas a lista deve ser lida e revisada para ver o que é aplicável ao seu projeto.

A lista fornece uma breve visão geral de cada aspecto de configuração, juntamente com links para as páginas que fornecem detalhes completos.

### Lista de verificação de segurança {#security-checklist}

Vários problemas de configuração principais estão listados na [Lista de Verificação de Segurança](/help/sites-administering/security-checklist.md). Certifique-se de ler este documento e executar qualquer ação necessária para sua instalação.

### Configuração da interface do usuário padrão — otimizada para toque ou clássica {#configuring-the-default-ui-touch-optimized-or-classic}

Há duas interfaces do usuário disponíveis para uso no AEM:

* A interface otimizada para toque
* A interface clássica

Você pode configurar a interface necessária usando o [Mapeamento de Raiz](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Mais informações sobre a seleção da interface estão disponíveis em [Seleção da interface](/help/sites-authoring/select-ui.md).

### IPv4 e IPv6 {#ipv-and-ipv}

Todos os elementos do AEM (por exemplo, o repositório e o Dispatcher) podem ser instalados em redes IPv4 e IPv6.

A operação é contínua, pois nenhuma configuração especial é necessária. Quando necessário, você pode simplesmente especificar um endereço IP usando o formato apropriado ao seu tipo de rede.

Isso significa que quando um endereço IP precisar ser especificado, você poderá selecionar (conforme necessário) de:

* um endereço IPv6

  por exemplo, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* um endereço IPv4

  por exemplo, `https://123.1.1.4:4502`

* um nome de servidor

  por exemplo, `https://www.yourserver.com:4502`

* o caso padrão de `localhost` será interpretado para instalações de rede IPv4 e IPv6

  por exemplo, `http://localhost:4502`

### Limpeza de versão {#version-purging}

Em uma instalação padrão, o AEM cria uma versão de uma página ou nó sempre que você ativa uma página (após atualizar o conteúdo). Você também pode criar versões adicionais mediante solicitação usando a guia **Versionamento** do sidekick. Todas essas versões são armazenadas no repositório e podem ser restauradas, se necessário.

Essas versões nunca são removidas, portanto, o tamanho do repositório cresce com o tempo e, portanto, deve ser gerenciado.

Consulte [Limpeza de versão](/help/sites-deploying/version-purging.md) para obter detalhes completos, em particular [Gerenciador de versão](/help/sites-deploying/version-purging.md#version-manager) para obter detalhes sobre como configurar o AEM para limpar versões mais antigas quando uma nova versão for criada.

### Logs {#logging}

O AEM oferece a possibilidade de configurar:

* parâmetros globais para o serviço de log central
* registro de dados de solicitação; uma configuração de registro especializada para informações de solicitação
* definições específicas para os serviços individuais; por exemplo, um arquivo de log individual e o formato para as mensagens de log

Consulte [Log](/help/sites-deploying/configure-logging.md) para obter detalhes completos.

### Modos de execução {#run-modes}

Os modos de execução permitem ajustar a instância do AEM para uma finalidade específica. Por exemplo, crie ou publique, teste, desenvolvimento ou intranet e assim por diante.

Isso é feito definindo coleções de parâmetros de configuração para cada modo de execução. Um conjunto básico de parâmetros de configuração é aplicado a todos os modos de execução, e você pode ajustar conjuntos adicionais para a finalidade de seu ambiente específico. Eles são aplicados conforme necessário.

Todas as definições de configuração são armazenadas em um repositório e ativadas definindo o **Modo de Execução**.

Consulte [Modos de Execução](/help/sites-deploying/configure-runmodes.md) para obter detalhes completos.

### Logon único {#single-sign-on}

O Logon único (SSO) permite que um usuário acesse vários sistemas após fornecer credenciais de autenticação (como um nome de usuário e senha) uma vez. Um sistema separado (conhecido como autenticador confiável) executa a autenticação e fornece ao Experience Manager as credenciais do usuário. O Experience Manager verifica e impõe as permissões de acesso ao usuário (ou seja, determina quais recursos o usuário tem permissão para acessar).

Consulte [Logon único](/help/sites-deploying/single-sign-on.md) para obter mais detalhes.

### Mapeamento de recursos {#resource-mapping}

O mapeamento de recursos é usado para definir redirecionamentos, URLs personalizados e hosts virtuais para o AEM.

Por exemplo, você pode usar esses mapeamentos para:

* Prefixe todas as solicitações com `/content` para que a estrutura interna fique oculta dos visitantes do seu site.
* Defina um redirecionamento para que todas as solicitações para a página `/content/en/gateway` do seu site sejam redirecionadas para `https://gbiv.com/`.

Consulte [Mapeamento de recursos](/help/sites-deploying/resource-mapping.md) para obter mais detalhes.

### Replicação, replicação reversa e agentes de replicação {#replication-reverse-replication-and-replication-agents}

Os agentes de replicação são fundamentais para a AEM como o mecanismo usado para:

* [Publicar (ativar)](/help/sites-authoring/publishing-pages.md) conteúdo de um autor para um ambiente de publicação.
* Limpar explicitamente o conteúdo do cache do Dispatcher.
* Retorne a entrada do usuário (por exemplo, entrada de formulário) do ambiente de publicação para o ambiente do autor (sob controle do ambiente do autor).

Para obter mais detalhes, consulte [Replicação](/help/sites-deploying/replication.md).

### Configurações do OSGi {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia do AEM. É usado para controlar os pacotes compostos do AEM e sua configuração.

Consulte [Configurações de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obter uma lista de vários pacotes relevantes para a implementação do projeto (listados de acordo com o pacote). Nem todas as configurações listadas precisam ser ajustadas, algumas são mencionadas para ajudar você a entender como o AEM opera.

Ao trabalhar com o AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

### Configuração do LDAP {#configuring-ldap}

A autenticação LDAP é necessária para autenticar usuários armazenados em um diretório LDAP (central), como o Ative Diretory. Isso ajuda a reduzir o esforço necessário para gerenciar contas de usuário.

A autenticação LDAP ocorre no nível do repositório, portanto, é manipulada diretamente pelo repositório. Para obter mais detalhes, consulte [Configurando LDAP com AEM](/help/sites-administering/ldap-config.md).

Para obter o gerenciamento de usuários no AEM (incluindo a atribuição de direitos de acesso), consulte [Administração e Segurança de Usuários](/help/sites-administering/security.md).

### Configuração do Dispatcher {#configuring-the-dispatcher}

O Dispatcher é a ferramenta de armazenamento em cache, balanceamento de carga ou ambos da Adobe Experience Manager. Ele pode ser usado com um servidor Web de classe empresarial.

Consulte [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) para obter os detalhes completos, em particular [Configurando o Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html) para obter mais detalhes sobre a configuração.

### Configuração do AEM LiveCycle Connector {#configuring-aem-livecycle-connector}

Com o lançamento dos serviços de documento da AEM e da Segurança de documentos da AEM, a AEM agora tem a capacidade de chamar os serviços de documento do LiveCycle para renderizar um formulário XFA, converter um documento para o PDF e proteger um documento por política.

### Descarregamento de Jobs e Administração de Topologia {#job-offloading-and-topology-administration}

[Offloading](/help/sites-deploying/offloading.md) distribui tarefas de processamento entre instâncias do Experience Manager em uma topologia. Com a descarga do, é possível usar instâncias específicas do Experience Manager para executar tipos específicos de processamento. O processamento especializado permite maximizar o uso dos recursos disponíveis do servidor.

As topologias são clusters do Experience Manager livremente acoplados que estão participando da descarga. Um cluster consiste em uma ou mais instâncias de servidor do Experience Manager (uma única instância é considerada um cluster).

Para obter mais informações sobre como exibir ou modificar a associação de topologia, consulte a seção [Administrando Topologias](/help/sites-deploying/offloading.md#administering-topologies).

### Configuração do console de boas-vindas {#configuring-the-welcome-console}

O console de Boas-vindas da interface clássica fornece uma lista de links para os vários consoles e funcionalidades no AEM.

É possível configurar os links que estão visíveis; consulte [Configurando o Console de Boas-vindas](/help/sites-developing/customizing-the-welcome-console.md) para obter mais detalhes.

### Configuração do para desempenho {#configuring-for-performance}

O [Desempenho](/help/sites-deploying/configuring-performance.md) é a chave do seu projeto. Determinados aspectos do AEM (e/ou do repositório subjacente) podem ser configurados para otimizar o desempenho.

Consulte [Configuração para Desempenho](/help/sites-deploying/configuring-performance.md#configuring-for-performance) para obter mais detalhes.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Armazenamento de dados compartilhado {#shared-data-store}

O armazenamento de dados do repositório é usado para descarregar o armazenamento de binários grandes do repositório em uma área separada, para que várias instâncias do mesmo binário (uma imagem, por exemplo) na árvore do repositório sejam armazenadas apenas uma vez.

Esse recurso &quot;armazenar uma vez, referência várias vezes&quot; pode ser estendido para atender não apenas a uma única árvore de repositório, mas repositórios totalmente separados, configurando o armazenamento de dados de cada um para fazer referência à mesma localização do sistema de arquivos compartilhados.

Esse armazenamento de dados pode ser compartilhado entre diferentes nós no mesmo cluster, diferentes instâncias de publicação e/ou criação na mesma instalação ou até mesmo instâncias totalmente separadas em instalações diferentes.

Para obter mais informações, consulte [Configurando Repositórios de Dados e Repositórios de Nós](/help/sites-deploying/data-store-config.md).

## Outras considerações de configuração {#further-configuration-considerations}

### Habilitar HTTP por SSL {#enabling-http-over-ssl}

Você pode habilitar HTTP sobre SSL para empregar conexões mais seguras aos seus servidores.

Consulte [Habilitando HTTP por SSL](/help/sites-administering/ssl-by-default.md) para obter mais detalhes.

### Portais e portlets do AEM {#aem-portals-and-portlets}

Um portal é um aplicativo da Web que fornece personalização, logon único, integração de conteúdo de diferentes fontes e hospeda a camada de apresentação dos sistemas de informações. O componente de portlet também permite incorporar um portlet na página. Para acessar o conteúdo fornecido pelo WCM CQ5, o servidor do portal pode ser equipado com o portlet do diretor do portal CQ5. Você pode fazer isso instalando, configurando e adicionando o portlet à página do portal.

Consulte o [Portal e Portlets](/help/sites-administering/aem-as-portal.md) para obter mais detalhes.

### Expiração de objetos estáticos {#expiration-of-static-objects}

Os objetos estáticos (por exemplo, ícones) não são alterados. Portanto, o sistema deve ser configurado de modo que não expire (por um período de tempo razoável) e, assim, reduza o tráfego desnecessário.

Consulte [Expiração de Objetos Estáticos](/help/sites-deploying/expiration-static-objects.md) para obter mais detalhes.

### Arquivos abertos no processo Java™ {#open-files-in-the-java-process}

Cada processo Java™ pode acessar arquivos - isso requer recursos do sistema. Por esse motivo, um limite superior é definido como o número de arquivos que cada processo tem permissão para acessar simultaneamente. Se isso for excedido, poderá ocorrer um erro de exceção.

Se o processo do AEM exceder esse máximo, a mensagem &quot;`too many open files`&quot; será exibida em `error.log`.

Para evitar essas exceções, faça o seguinte:

1. Verifique quantos arquivos abertos o processo do AEM está usando.

   Essa verificação depende da plataforma em que sua instância está sendo executada. Utilitários como lsof (UNIX®) ou Process Explorer (Windows) podem ser usados.

   Esse valor deve ser monitorado durante o desenvolvimento e o teste para:

   * confirme se os arquivos estão sendo fechados, conforme necessário
   * para determinar o valor máximo necessário (em várias circunstâncias)

1. Defina o máximo permitido.

   O novo valor deve atender às necessidades atuais e a quaisquer picos futuros, portanto, é aconselhável dobrar as necessidades atuais.

   Por padrão, o `serverctl` configura o `CQ_MAX_OPEN_FILES` para `8192`; isso deve ser suficiente para a maioria dos cenários.

### Configuração do editor de rich text {#configuring-the-rich-text-editor}

O **Editor de Rich Text** (**RTE**) fornece aos autores uma ampla variedade de [funcionalidades](/help/sites-authoring/rich-text-editor.md) para editar seu conteúdo textual; fornecendo a eles ícones, caixas de seleção e menus para uma experiência do WYSIWYG.

Consulte [Configurando o Editor de Rich Text](/help/sites-administering/rich-text-editor.md) para obter mais detalhes.

### Configuração de Desfazer para Edição de Página {#configuring-undo-for-page-editing}

Há várias propriedades que controlam o comportamento dos comandos desfazer e refazer para editar páginas. Eles podem ser configurados. Consulte [Configuração de Desfazer para Edição de Página](/help/sites-administering/config-undo.md) para obter mais detalhes.

### Configuração do componente de vídeo {#configuring-the-video-component}

O [componente de Vídeo](/help/sites-authoring/default-components-foundation.md#video) permite que você coloque um elemento de vídeo predefinido e pronto para uso na sua página.

Para que ocorra a transcodificação adequada, o administrador deve [instalar o FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) separadamente. Eles também podem [Configurar seus Perfis de vídeo](/help/sites-administering/config-video.md#configure-video-profiles) para uso com elementos html5.

### Configuração e personalização de relatórios {#configuring-and-customizing-reports}

Para ajudar você a monitorar e analisar o estado da sua instância, o CQ fornece uma seleção de relatórios padrão, que podem ser configurados para seus requisitos individuais:

Consulte as [Noções básicas sobre a personalização de relatórios](/help/sites-administering/reporting.md#the-basics-of-report-customization) para obter mais detalhes.

### Configuração da notificação por e-mail {#configuring-email-notification}

O CQ envia notificações por email para usuários que:

* Ter se inscrito em eventos de página, por exemplo, modificação ou replicação.
* Ter se inscrito nos eventos do fórum.
* É necessário executar uma etapa em um fluxo de trabalho.

Consulte [Configurando Notificação por Email](/help/sites-administering/notification.md) para obter mais detalhes.

### Ativar impressões de página {#enabling-page-impressions}

As impressões de página são exibidas na coluna **Impressões** do console siteadmin da interface clássica. Para habilitar a captura de impressões de página, configure o seguinte:

* Na instância de publicação:

   * [Estatísticas de página WCM CQ do dia](/help/sites-deploying/osgi-configuration-settings.md)

* Na instância do autor:

   * [Rastreador de impressões de página do Adobe](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>A configuração do Rastreador de impressões de página do Adobe no ambiente de criação permite solicitações anônimas ao serviço de rastreamento.

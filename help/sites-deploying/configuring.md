---
title: Conceitos básicos de configuração
seo-title: Basic Configuration Concepts
description: Saiba como configurar o AEM.
seo-description: Learn how to configure AEM.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 2%

---

# Conceitos básicos de configuração{#basic-configuration-concepts}

O Adobe Experience Manager (AEM) é instalado com as configurações padrão para todos os parâmetros, o que permite que ele seja executado &quot;imediatamente&quot;. No entanto, você pode configurar AEM para seus próprios requisitos específicos.

Há muitos aspectos do AEM que podem ser configurados:

* Alguns são [normalmente configurado para cada instalação de projeto](#primary-configuration-considerations) e devem ser revisadas para confirmar se são ou não aplicáveis ao seu projeto.
* [Outras configurações](#further-configuration-considerations) podem ser comuns, embora não sejam imperativas; relacionados a recursos ou desempenho e estabilidade do sistema.
* Outros são necessários apenas para determinados recursos opcionais do AEM (são documentados junto com o recurso apropriado).

Dependendo da configuração específica, essas alterações podem ser feitas usando o:

* **Adobe CQ Web Console**

   Este é um local padrão para configurar pacotes e serviços OSGi.

   Consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e práticas recomendadas.

* **Repositório**

   Um subconjunto de configurações OSGi está disponível no repositório. Isso garante que copiar ou replicar o conteúdo do repositório recrie configurações idênticas. Você também pode adicionar suas próprias configurações, dependendo do modo de execução, ao repositório.

   Consulte [Configuração do OSGi no Repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) , nomeadamente [Adicionar uma nova configuração ao repositório](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) para obter mais detalhes.

* **Sistema de arquivos**

   Alguns arquivos de configuração residem no sistema de arquivos.

* **WCM AEM**

   Vários aspectos podem ser configurados no próprio AEM WCM, muitos usando o [Ferramentas](/help/sites-administering/tools-consoles.md) console; por exemplo, agentes de replicação.

>[!NOTE]
>
>Ao trabalhar com o Adobe Experience Manager, há vários métodos de gerenciamento das configurações para serviços OSGi (console ou nós de repositório).
>
>Consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

>[!NOTE]
>
>Configurar AEM é simples, mas você deve estar ciente de que:
>
>Certas alterações podem ter um impacto importante nos aplicativos. Por esse motivo, verifique se você tem a experiência e o conhecimento necessários antes de começar a configurar o AEM e faça apenas as alterações necessárias. Todas as alterações feitas por meio do console OSGi são **imediatamente** aplicada ao sistema em execução (não é necessário reiniciar).

## Considerações de configuração primária {#primary-configuration-considerations}

Esta lista detalha as principais áreas configuradas com frequência para cada novo projeto. Nem todas são necessárias, mas a lista deve ser lida e revisada para ver o que se aplica ao seu projeto.

A lista fornece uma breve visão geral de cada aspecto de configuração, juntamente com links para as páginas que fornecem detalhes completos.

### Lista de verificação de segurança {#security-checklist}

Vários problemas chave de configuração são listados na variável [Lista de verificação de segurança](/help/sites-administering/security-checklist.md). Certifique-se de ler e tomar as medidas necessárias para a sua instalação.

### Configuração da interface de usuário padrão - Otimizada ao toque ou clássica {#configuring-the-default-ui-touch-optimized-or-classic}

Há duas interfaces de usuário disponíveis para uso no AEM:

* A interface otimizada para toque
* A interface clássica

É possível configurar a interface do usuário necessária usando [Mapeamento de raiz](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Mais informações sobre a seleção da interface do usuário estão disponíveis em [Selecionar sua interface do usuário](/help/sites-authoring/select-ui.md).

### IPv4 e IPv6 {#ipv-and-ipv}

Todos os elementos de AEM (por exemplo, o repositório, o Dispatcher etc.) podem ser instalados em redes IPv4 e IPv6.

A operação é perfeita, pois nenhuma configuração especial é necessária. Quando necessário, basta especificar um endereço IP usando o formato adequado ao seu tipo de rede.

Isso significa que, quando um endereço IP precisa ser especificado, você pode selecionar (conforme necessário) de:

* um endereço IPv6

   por exemplo `https://[ab12::34c5:6d7:8e90:1234]:4502`

* um endereço IPv4

   por exemplo `https://123.1.1.4:4502`

* um nome de servidor

   por exemplo, `https://www.yourserver.com:4502`

* o caso padrão de `localhost` será interpretado para instalações de rede IPv4 e IPv6

   por exemplo, `http://localhost:4502`

### Limpeza de versão {#version-purging}

Em uma instalação padrão, o AEM cria uma nova versão de uma página ou nó sempre que você ativa uma página (após atualizar o conteúdo). Você também pode criar versões adicionais mediante solicitação usando a variável **Controle de versão** guia do sidekick. Todas essas versões são armazenadas no repositório e podem ser restauradas, se necessário.

Essas versões nunca são removidas, portanto, o tamanho do repositório aumentará com o tempo e, portanto, precisará ser gerenciado.

Consulte [Limpeza de versão](/help/sites-deploying/version-purging.md) para mais pormenores, em especial [Gerenciador de versão](/help/sites-deploying/version-purging.md#version-manager) para obter detalhes sobre como configurar o AEM para limpar versões mais antigas quando uma nova versão for criada.

### Logs {#logging}

O AEM oferece a possibilidade de configurar:

* parâmetros globais para o serviço de registro central
* Solicitar registro de dados; uma configuração de registro especializada para obter informações de solicitação
* Configurações específicas para cada serviço; por exemplo, um arquivo de log individual e o formato para as mensagens de log

Consulte [Registro](/help/sites-deploying/configure-logging.md) para obter detalhes completos.

### Modos de execução {#run-modes}

Os modos de execução permitem ajustar a instância do AEM para uma finalidade específica; por exemplo, criar ou publicar, testar, desenvolver ou intranet, etc.

Isso é feito definindo coleções de parâmetros de configuração para cada modo de execução. Um conjunto básico de parâmetros de configuração é aplicado a todos os modos de execução. Em seguida, é possível ajustar conjuntos adicionais para a finalidade do ambiente específico. Elas são aplicadas conforme necessário.

Todas as configurações são armazenadas em um repositório e ativadas pela configuração do **Modo de execução**.

Consulte [Modos de Execução](/help/sites-deploying/configure-runmodes.md) para obter detalhes completos.

### Logon único {#single-sign-on}

O Logon único (SSO) permite que um usuário acesse vários sistemas após fornecer credenciais de autenticação (como nome de usuário e senha) uma vez. Um sistema separado (conhecido como autenticador confiável) executa a autenticação e fornece ao Experience Manager as credenciais do usuário. O Experience Manager verifica e aplica as permissões de acesso do usuário (ou seja, determina quais recursos o usuário tem permissão para acessar).

Consulte [Logon único](/help/sites-deploying/single-sign-on.md) para obter mais detalhes.

### Mapeamento de recursos {#resource-mapping}

O mapeamento de recursos é usado para definir redirecionamentos, URLs personalizadas e hosts virtuais para AEM.

Por exemplo, você pode usar esses mapeamentos para:

* Prefixar todas as solicitações com `/content` para que a estrutura interna fique oculta dos visitantes do seu site.
* Defina um redirecionamento para que todas as solicitações da variável `/content/en/gateway` página do seu site são redirecionadas para `https://gbiv.com/`.

Consulte [Mapeamento de recursos](/help/sites-deploying/resource-mapping.md) para obter mais detalhes.

### Replicação, replicação inversa e agentes de replicação {#replication-reverse-replication-and-replication-agents}

Os agentes de replicação são fundamentais para AEM como mecanismo utilizado para:

* [Publicar (ativar)](/help/sites-authoring/publishing-pages.md) conteúdo de um autor em um ambiente de publicação.
* Liberar explicitamente o conteúdo do cache do Dispatcher.
* Retorne a entrada do usuário (por exemplo, a entrada de formulário) do ambiente de publicação para o ambiente do autor (sob controle do ambiente do autor).

Para obter mais detalhes, consulte [Replicação](/help/sites-deploying/replication.md).

### Configurações do OSGi {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia de AEM. É usado para controlar os pacotes compostos de AEM e sua configuração.

Consulte [Configurações do OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obter uma lista dos vários pacotes relevantes para a implementação do projeto (listados de acordo com o pacote). Nem todas as configurações listadas precisam de ajuste, algumas são mencionadas para ajudar você a entender como o AEM opera.

Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

### Configuração do LDAP {#configuring-ldap}

A autenticação LDAP é necessária para autenticar usuários armazenados em um diretório LDAP (central), como o Ative Diretory. Isso ajuda a reduzir o esforço necessário para gerenciar contas de usuário.

A autenticação LDAP ocorre no nível do repositório, portanto, é manipulada diretamente pelo repositório. Para obter mais detalhes, consulte [Configuração do LDAP com AEM](/help/sites-administering/ldap-config.md).

Para o gerenciamento de usuários no AEM (incluindo a atribuição de direitos de acesso), consulte [Administração e segurança do usuário](/help/sites-administering/security.md).

### Configuração do Dispatcher {#configuring-the-dispatcher}

O Dispatcher é uma ferramenta de armazenamento em cache e/ou balanceamento de carga do Adobe Experience Manager, que pode ser usado em conjunto com um servidor Web de classe empresarial.

Consulte [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) para mais pormenores, em especial [Configuração do Dispatcher](https://helpx.adobe.com/pt/experience-manager/dispatcher/using/dispatcher-configuration.html) para obter mais detalhes sobre a configuração.

### Configuração AEM conector do LiveCycle {#configuring-aem-livecycle-connector}

Com o lançamento dos AEM Doc Services e AEM Doc Security, agora temos a capacidade de chamar os serviços de documento do LiveCycle para renderizar um formulário XFA, converter um documento em PDF e proteger um documento por políticas. Leia [Conector AEM LiveCycle](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) para obter mais detalhes.

### Descarregamento de Trabalho e Administração de Topologia {#job-offloading-and-topology-administration}

[Descarregamento](/help/sites-deploying/offloading.md) O distribui tarefas de processamento, somando instâncias Experience Manager em uma topologia. Com a descarga, você pode usar instâncias Experience Manager específicas para executar tipos específicos de processamento. O processamento especializado permite maximizar o uso dos recursos disponíveis do servidor.

As topologias são Experience Manager clusters vagamente acoplados que estão participando da descarga. Um cluster consiste em uma ou mais instâncias do servidor Experience Manager (uma única instância é considerada um cluster).

Para obter mais informações sobre como visualizar ou modificar a associação de topologia, consulte o [Administração de topologias](/help/sites-deploying/offloading.md#administering-topologies) seção.

### Configuração do console de boas-vindas {#configuring-the-welcome-console}

O console de boas-vindas da interface clássica fornece uma lista de links para os vários consoles e funcionalidades no AEM.

É possível configurar os links que estão visíveis. Consulte [Configuração do console de boas-vindas](/help/sites-developing/customizing-the-welcome-console.md) para obter mais detalhes.

### Configuração para desempenho {#configuring-for-performance}

[Desempenho](/help/sites-deploying/configuring-performance.md) é fundamental para o seu projeto. Determinados aspectos do AEM (e/ou do repositório subjacente) podem ser configurados para otimizar o desempenho.

Consulte [Configuração para desempenho](/help/sites-deploying/configuring-performance.md#configuring-for-performance) para obter mais detalhes.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Armazenamento de dados compartilhado {#shared-data-store}

O repositório de dados é usado para descarregar o armazenamento de binários grandes do repositório próprio de uma área separada, de modo que várias instâncias do mesmo binário (uma imagem, por exemplo) na árvore do repositório sejam armazenadas apenas uma vez.

Esse recurso &quot;store-once, reference-many-times&quot; pode ser estendido para servir não apenas uma única árvore de repositório, mas repositórios totalmente separados, configurando o armazenamento de dados de cada um para se referir ao mesmo local do sistema de arquivos compartilhado.

Esse armazenamento de dados pode ser compartilhado entre diferentes nós no mesmo cluster, em diferentes instâncias de publicação e/ou autor na mesma instalação ou ainda em instâncias totalmente separadas em diferentes instalações.

Para obter mais informações, consulte [Configuração dos armazenamentos de dados e de nós](/help/sites-deploying/data-store-config.md).

## Outras considerações de configuração {#further-configuration-considerations}

### Habilitar HTTP por SSL {#enabling-http-over-ssl}

Você pode habilitar HTTP sobre SSL para empregar conexões mais seguras com seus servidores.

Consulte [Habilitar HTTP por SSL](/help/sites-administering/ssl-by-default.md) para obter mais detalhes.

### Portais e portlets AEM {#aem-portals-and-portlets}

Um portal é uma aplicação Web que fornece personalização, logon único, integração de conteúdo de diferentes fontes e hospeda a camada de apresentação dos sistemas de informações. O componente de portlet também permite incorporar um portlet na página. Para acessar o conteúdo fornecido pelo WCM CQ5, o servidor de portal pode ser equipado com o portlet Director do portal CQ5. Você pode fazer isso instalando, configurando e adicionando o portlet à página do portal.

Consulte [Portal e portlets](/help/sites-administering/aem-as-portal.md) para obter mais detalhes.

### Expiração de objetos estáticos {#expiration-of-static-objects}

Os objetos estáticos (por exemplo, ícones) não são alterados. Por conseguinte, o sistema deve ser configurado de modo a não expirar (por um período de tempo razoável), reduzindo assim o tráfego desnecessário.

Consulte [Expiração de objetos estáticos](/help/sites-deploying/expiration-static-objects.md) para obter mais detalhes.

### Abrir arquivos no processo Java {#open-files-in-the-java-process}

Cada processo java pode acessar arquivos. Isso requer recursos do sistema. Por esse motivo, um limite máximo é definido como quantos arquivos cada processo tem permissão para acessar simultaneamente. Se isso for excedido, pode ocorrer um erro de exceção.

Se o processo de AEM exceder esse máximo, a mensagem &quot; `too many open files`&quot; será visto em `error.log`.

Para evitar essas exceções, é necessário:

1. Verifique quantos arquivos abertos seu processo de AEM está usando.

   A forma como você faz essa verificação dependerá da plataforma na qual sua instância está sendo executada. Utilitários como lsof (Unix) ou Process Explorer (Windows) podem ser usados.

   Esse valor deve ser monitorado durante o desenvolvimento e testes para:

   * confirme se os arquivos estão sendo fechados, conforme necessário
   * para determinar o valor máximo necessário (em várias circunstâncias)

1. Defina o máximo permitido.

   O novo valor deve atender tanto às necessidades atuais como a quaisquer picos futuros, pelo que é aconselhável duplicar as necessidades atuais.

   Por padrão, `serverctl` configurações `CQ_MAX_OPEN_FILES` para `8192`; isso deve ser suficiente para a maioria dos cenários.

### Configuração do editor de rich text {#configuring-the-rich-text-editor}

O **Editor de Rich Text** (**RTE**) fornece aos autores uma grande variedade de [funcionalidade](/help/sites-authoring/rich-text-editor.md) para editar seu conteúdo textual; fornecendo ícones, caixas de seleção e menus para uma experiência WYSIWYG.

Consulte [Configuração do editor de rich text](/help/sites-administering/rich-text-editor.md) para obter mais detalhes.

### Configuração de desfazer para edição de página {#configuring-undo-for-page-editing}

Há várias propriedades que controlam o comportamento dos comandos desfazer e refazer para editar páginas. Eles podem ser configurados, consulte [Configuração de desfazer para edição de página](/help/sites-administering/config-undo.md) para obter mais detalhes.

### Configuração do componente de vídeo {#configuring-the-video-component}

O [Componente de vídeo](/help/sites-authoring/default-components-foundation.md#video) O permite colocar um elemento de vídeo predefinido e pronto para uso na página.

Para que ocorra a decodificação adequada, você deve instalar o [FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) separadamente. Eles também podem [Configurar os perfis de vídeo](/help/sites-administering/config-video.md#configure-video-profiles) para uso com elementos html5.

### Configuração e personalização de relatórios {#configuring-and-customizing-reports}

Para ajudar você a monitorar e analisar o estado da sua instância, o CQ fornece uma seleção de relatórios padrão, que podem ser configurados para seus requisitos individuais:

Consulte a [Noções básicas da personalização de relatórios](/help/sites-administering/reporting.md#the-basics-of-report-customization) para obter mais detalhes.

### Configuração de notificação por email {#configuring-email-notification}

O CQ envia notificações por email para usuários que:

* Inscreveram-se em eventos de página, por exemplo, modificação ou replicação.
* Inscreveram-se nos eventos do fórum.
* É necessário executar uma etapa em um fluxo de trabalho.

Consulte [Configuração de notificação por email](/help/sites-administering/notification.md) para obter mais detalhes.

### Ativar impressões de página {#enabling-page-impressions}

As impressões de página são exibidas na **Impressões** coluna do console siteadmin da interface clássica. Para ativar a captura de impressões de página, você precisa configurar:

* Na instância de publicação:

   * [Estatísticas de página do WCM CQ do dia](/help/sites-deploying/osgi-configuration-settings.md)

* Na instância do autor:

   * [Rastreamento de impressões de página Adobe](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>A configuração do Rastreador de impressões de página do Adobe no ambiente do autor permitirá solicitações anônimas para o serviço de rastreamento.

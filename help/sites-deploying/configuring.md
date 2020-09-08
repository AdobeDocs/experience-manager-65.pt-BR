---
title: Conceitos básicos de configuração
seo-title: Conceitos básicos de configuração
description: Saiba como configurar o AEM.
seo-description: Saiba como configurar o AEM.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
translation-type: tm+mt
source-git-commit: 8f35717324cd2c1524fb2cf931b3ce21be05729a
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 1%

---


# Conceitos básicos de configuração{#basic-configuration-concepts}

O Adobe Experience Manager (AEM) é instalado com as configurações padrão para todos os parâmetros, o que permite que ele execute &quot;out of the box&quot;. No entanto, você pode configurar AEM para seus próprios requisitos específicos.

Há muitos aspectos de AEM que podem ser configurados:

* Alguns são configurados [comumente para cada instalação](#primary-configuration-considerations) do projeto e devem ser revisados para confirmar se são aplicáveis ao seu projeto.
* [Outras configurações](#further-configuration-considerations) podem ser comuns, embora não sejam imperativas; relacionado aos recursos, ou ao desempenho e estabilidade do sistema.
* Outros são necessários apenas para determinados recursos opcionais do AEM (são documentados juntamente com o recurso apropriado).

Dependendo da configuração específica, essas alterações podem ser feitas usando:

* **Adobe CQ Web Console**

   Este é um local padrão para configurar pacotes e serviços OSGi.

   Consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e práticas recomendadas.

* **Repositório**

   Um subconjunto de configurações OSGi está disponível no repositório. Isso garante que copiar ou replicar o conteúdo do repositório recrie configurações idênticas. Você também pode adicionar suas próprias configurações, dependendo do modo de execução, ao repositório.

   Consulte Configuração do [OSGi no repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) e, em particular, [Adicionar uma nova configuração ao repositório](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) para obter mais detalhes.

* **Sistema de arquivos**

   Alguns arquivos de configuração residem no sistema de arquivos.

* **WCM AEM**

   Vários aspectos podem ser configurados no próprio AEM WCM, muitos usando o console [Ferramentas](/help/sites-administering/tools-consoles.md) ; por exemplo, agentes de replicação.

>[!NOTE]
>
>Ao trabalhar com a Adobe Experience Manager, há vários métodos de gerenciar as configurações dos serviços OSGi (console ou nós de repositório).
>
>Consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

>[!NOTE]
>
>A configuração do AEM é simples, mas você deve estar ciente de que:
>
>Determinadas alterações podem ter um impacto importante nos aplicativos. Por esse motivo, certifique-se de ter a experiência e o conhecimento necessários antes da start de configurar o AEM e faça apenas as alterações necessárias. Todas as alterações feitas por meio do console OSGi são aplicadas **imediatamente** ao sistema em execução (nenhuma reinicialização é necessária).

## Considerações sobre a configuração principal {#primary-configuration-considerations}

Esta lista detalha as principais áreas configuradas comumente para cada novo projeto. Nem todos são necessários, mas a lista deve ser lida e revisada para ver o que se aplica ao seu projeto.

A lista fornece uma breve visão geral de cada aspecto de configuração, juntamente com links para as páginas que fornecem detalhes completos.

### Security Checklist {#security-checklist}

Vários problemas importantes de configuração estão listados na Lista de verificação de [segurança](/help/sites-administering/security-checklist.md). Certifique-se de ler isso e executar todas as ações necessárias para sua instalação.

### Configuração da interface padrão - otimizada ao toque ou clássica {#configuring-the-default-ui-touch-optimized-or-classic}

Há duas interfaces de usuário disponíveis para uso em AEM:

* A interface otimizada para toque
* A interface clássica

Você pode configurar a interface necessária usando o Mapeamento [](/help/sites-deploying/osgi-configuration-settings.md)raiz.

>[!NOTE]
>
>Outras informações sobre como selecionar a interface do usuário estão disponíveis em [Selecionar sua interface do usuário](/help/sites-authoring/select-ui.md).

### IPv4 e IPv6 {#ipv-and-ipv}

Todos os elementos de AEM (por exemplo, o repositório, o Dispatcher etc.) podem ser instalados em redes IPv4 e IPv6.

A operação é contínua, pois nenhuma configuração especial é necessária. Quando necessário, basta especificar um endereço IP usando o formato apropriado ao seu tipo de rede.

Isso significa que, quando um endereço IP precisa ser especificado, você pode selecionar (conforme necessário) de:

* um endereço IPv6

   for example `https://[ab12::34c5:6d7:8e90:1234]:4502`

* um endereço IPv4

   for example `https://123.1.1.4:4502`

* um nome de servidor

   for example, `https://www.yourserver.com:4502`

* o caso padrão de `localhost` será interpretado para instalações de rede IPv4 e IPv6

   for example, `http://localhost:4502`

### Expurgação de versão {#version-purging}

Em uma instalação padrão, AEM cria uma nova versão de uma página ou nó sempre que você ativa uma página (após atualizar o conteúdo). Você também pode criar versões adicionais mediante solicitação usando a guia **Controle de versão** do sidekick. Todas essas versões são armazenadas no repositório e podem ser restauradas, se necessário.

Essas versões nunca são expurgadas, portanto, o tamanho do repositório crescerá com o tempo e, portanto, precisará ser gerenciado.

Consulte Expurgação [de](/help/sites-deploying/version-purging.md) versão para obter detalhes completos, em particular o Gerenciador [de](/help/sites-deploying/version-purging.md#version-manager) versão para obter detalhes sobre como configurar AEM para expurgar versões anteriores quando uma nova versão for criada.

### Logs {#logging}

AEM oferta a possibilidade de configurar:

* parâmetros globais para o serviço central de registro
* solicitar o registro de dados; uma configuração de registro especializada para informações de solicitação
* definições específicas para cada serviço; por exemplo, um arquivo de log individual e um formato para as mensagens de log

Consulte [Registro](/help/sites-deploying/configure-logging.md) para obter detalhes completos.

### Modos de execução {#run-modes}

Os modos de execução permitem ajustar sua instância de AEM para uma finalidade específica; por exemplo, autor ou publicação, teste, desenvolvimento ou intranet, etc.

Isso é feito definindo coleções de parâmetros de configuração para cada modo de execução. Um conjunto básico de parâmetros de configuração é aplicado para todos os modos de execução, então você pode ajustar conjuntos adicionais para a finalidade do seu ambiente específico. Eles são aplicados conforme necessário.

Todas as configurações são armazenadas em um repositório e ativadas pela configuração do Modo **de execução**.

Consulte Modos de [execução](/help/sites-deploying/configure-runmodes.md) para obter detalhes completos.

### Logon único {#single-sign-on}

O logon único (SSO) permite que um usuário acesse vários sistemas após fornecer credenciais de autenticação (como nome de usuário e senha) uma vez. Um sistema separado (conhecido como autenticador confiável) executa a autenticação e fornece ao Experience Manager as credenciais do usuário. O Experience Manager verifica e impõe as permissões de acesso para o usuário (isto é, determina quais recursos o usuário tem permissão para acessar).

Consulte Logon [único](/help/sites-deploying/single-sign-on.md) para obter mais detalhes.

### Resource Mapping {#resource-mapping}

O mapeamento de recursos é usado para definir redirecionamentos, URLs personalizados e hosts virtuais para AEM.

Por exemplo, você pode usar esses mapeamentos para:

* Prefixe todas as solicitações com `/content` o prefixo para que a estrutura interna fique oculta dos visitantes para o site.
* Defina um redirecionamento para que todas as solicitações da `/content/en/gateway` página do site sejam redirecionadas para `https://gbiv.com/`.

Consulte Mapeamento [de](/help/sites-deploying/resource-mapping.md) recursos para obter mais detalhes.

### Replicação, Replicação Inversa e Agentes de Replicação {#replication-reverse-replication-and-replication-agents}

Os agentes de replicação são fundamentais para AEM como mecanismo usado para:

* [Publique (ative)](/help/sites-authoring/publishing-pages.md) conteúdo de um autor em um ambiente de publicação.
* Limpe explicitamente o conteúdo do cache do Dispatcher.
* Retorna a entrada do usuário (por exemplo, a entrada de formulário) do ambiente publish para o ambiente author (sob controle do ambiente author).

For further details see [Replication](/help/sites-deploying/replication.md).

### Configurações do OSGi {#osgi-configuration-settings}

[O OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia de AEM. É usado para controlar os pacotes compostos de AEM e sua configuração.

Consulte as configurações [do](/help/sites-deploying/osgi-configuration-settings.md) OSGi para obter uma lista dos vários pacotes que são relevantes para a implementação do projeto (listados de acordo com o pacote). Nem todas as configurações listadas precisam de ajuste, algumas são mencionadas para ajudá-lo a entender como AEM opera.

When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

### Configuração do LDAP {#configuring-ldap}

A autenticação LDAP é necessária para autenticar usuários armazenados em um diretório LDAP (central), como o Ative Diretory. Isso ajuda a reduzir o esforço necessário para gerenciar contas de usuário.

A autenticação LDAP ocorre no nível do repositório, portanto, é feita diretamente pelo repositório. Para obter mais detalhes, consulte [Configuração do LDAP com AEM](/help/sites-administering/ldap-config.md).

Para o gerenciamento de usuários no AEM (incluindo atribuição de direitos de acesso), consulte Administração e segurança [](/help/sites-administering/security.md)do usuário.

### Configuração do Dispatcher {#configuring-the-dispatcher}

O Dispatcher é uma ferramenta de cache e/ou balanceamento de carga da Adobe Experience Manager que pode ser usada em conjunto com um servidor Web de classe empresarial.

Consulte [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) para obter detalhes completos, em particular [Configuração do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para obter mais detalhes sobre a configuração.

### Configuração AEM conector do LiveCycle {#configuring-aem-livecycle-connector}

Com o lançamento dos Serviços AEM e AEM Segurança do Documento, agora temos a capacidade de chamar os serviços de documentação do LiveCycle para renderizar um formulário XFA, converter um documento em PDF e proteger um documento por política. Leia [AEM Conector](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) do LiveCycle para obter mais detalhes.

### Descarregamento de tarefa e administração de topologia {#job-offloading-and-topology-administration}

[A descarga](/help/sites-deploying/offloading.md) distribui tarefas de processamento que somam instâncias de Experience Manager em uma topologia. Com o descarregamento, você pode usar instâncias de Experience Manager específicas para executar tipos específicos de processamento. O processamento especializado permite maximizar o uso dos recursos disponíveis do servidor.

As topologias são clusters de Experience Manager que estão participando da descarga. Um cluster consiste em uma ou mais instâncias de servidor de Experience Manager (uma única instância é considerada um cluster).

Para obter mais informações sobre como visualização ou modificar a associação de topologia, consulte a seção Topologias [de](/help/sites-deploying/offloading.md#administering-topologies) administração.

### Configuração do console de boas-vindas {#configuring-the-welcome-console}

O console Bem-vindo da interface clássica fornece uma lista de links para os vários consoles e funcionalidades dentro do AEM.

É possível configurar os links que estão visíveis. Consulte [Configuração do console](/help/sites-developing/customizing-the-welcome-console.md) de boas-vindas para obter mais detalhes.

### Configuração para desempenho {#configuring-for-performance}

[O desempenho](/help/sites-deploying/configuring-performance.md) é a chave para o seu projeto. Determinados aspectos do AEM (e/ou do repositório subjacente) podem ser configurados para otimizar o desempenho.

Consulte [Configuração de desempenho](/help/sites-deploying/configuring-performance.md#configuring-for-performance) para obter mais detalhes.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Shared Data Store {#shared-data-store}

O repositório de dados é usado para descarregar o armazenamento de binários grandes do repositório próprio para uma área separada, de modo que várias instâncias do mesmo binário (uma imagem, por exemplo) na árvore do repositório sejam armazenadas apenas uma vez.

Esse recurso &quot;store-once, reference-many-times&quot; pode ser estendido para servir não apenas uma única árvore de repositório, mas repositórios totalmente separados, configurando o armazenamento de dados de cada um para se referir ao mesmo local do sistema de arquivos compartilhado.

Esse armazenamento de dados pode ser compartilhado entre diferentes nós no mesmo cluster, diferentes instâncias de publicação e/ou autor na mesma instalação, ou até mesmo instâncias totalmente separadas em instalações diferentes.

Para obter mais informações, consulte [Configuração de armazenamento de dados e armazenamento](/help/sites-deploying/data-store-config.md)de nós.

## Outras considerações sobre configuração {#further-configuration-considerations}

### Habilitando HTTP por SSL {#enabling-http-over-ssl}

Você pode habilitar HTTP sobre SSL para empregar conexões mais seguras para seus servidores.

Consulte [Habilitar HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obter mais detalhes.

### Portais e portlets AEM {#aem-portals-and-portlets}

Um portal é um aplicativo da Web que fornece personalização, logon único, integração de conteúdo de diferentes fontes e hospeda a camada de apresentação dos sistemas de informações. O componente portlet também permite que você incorpore um portlet na página. Para acessar o conteúdo fornecido pelo CQ5 WCM, o servidor de portal pode ser equipado com o Portlet Director do CQ5 Portal. Você pode fazer isso instalando, configurando e adicionando o portlet à página do portal.

Consulte [Portal e Portlets](/help/sites-administering/aem-as-portal.md) para obter mais detalhes.

### Expiração de objetos estáticos {#expiration-of-static-objects}

Objetos estáticos (por exemplo, ícones) não são alterados. Portanto, o sistema deve ser configurado para que não expire (por um período de tempo razoável) e, assim, reduza o tráfego desnecessário.

Consulte [Expiração de objetos](/help/sites-deploying/expiration-static-objects.md) estáticos para obter mais detalhes.

### Abrir arquivos no processo Java {#open-files-in-the-java-process}

Cada processo java pode acessar arquivos - isso requer recursos do sistema. Por isso, um limite máximo é definido como quantos arquivos cada processo tem permissão para acessar simultaneamente. Se isso for excedido, um erro de exceção poderá ocorrer.

Se o processo de AEM exceder esse máximo, a mensagem &quot; `too many open files`&quot; será exibida em `error.log`.

Para evitar essas exceções, é necessário:

1. Verifique quantos arquivos abertos seu processo de AEM está usando.

   A forma como você efetua essa verificação dependerá da plataforma na qual sua instância está sendo executada. Utilitários como lsof (Unix) ou Process Explorer (Windows) podem ser usados.

   Este valor deve ser monitorizado durante o desenvolvimento e testes para:

   * confirme se os arquivos estão sendo fechados, conforme necessário
   * para determinar o valor máximo necessário (em várias circunstâncias)

1. Defina o máximo permitido.

   O novo valor deverá atender tanto às necessidades atuais como a quaisquer picos futuros, pelo que é aconselhável duplo das necessidades atuais.

   Por padrão, `serverctl` configura `CQ_MAX_OPEN_FILES` para `8192`; isso deve ser suficiente para a maioria dos cenários.

### Configuração do Editor de Rich Text {#configuring-the-rich-text-editor}

O **Editor** de Rich Text (**RTE**) fornece aos autores uma ampla variedade de [funcionalidades](/help/sites-authoring/rich-text-editor.md) para editar seu conteúdo textual; fornecer ícones, caixas de seleção e menus para uma experiência WYSIWYG.

Consulte [Configuração do Editor](/help/sites-administering/rich-text-editor.md) de Rich Text para obter mais detalhes.

### Configuração do comando Desfazer para edição de página {#configuring-undo-for-page-editing}

Há várias propriedades que controlam o comportamento dos comandos desfazer e refazer para editar páginas. Eles podem ser configurados, consulte [Configuração de desfazer para edição](/help/sites-administering/config-undo.md) de página para obter mais detalhes.

### Configuração do componente de vídeo {#configuring-the-video-component}

The [Video component](/help/sites-authoring/default-components-foundation.md#video) allows you to place a predefined, out-of-the-box video element on your page.

Para que ocorra a decodificação adequada, você deve instalar o [FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) separadamente. They can also [Configure your Video Profiles](/help/sites-administering/config-video.md#configure-video-profiles) for use with html5 elements.

### Configuração e personalização de relatórios {#configuring-and-customizing-reports}

Para ajudá-lo a monitorar e analisar o estado de sua instância, o CQ fornece uma seleção de relatórios padrão, que podem ser configurados para seus requisitos individuais:

Consulte os [fundamentos da personalização](/help/sites-administering/reporting.md#the-basics-of-report-customization) de relatórios para obter mais detalhes.

### Configuração de notificação por email {#configuring-email-notification}

O CQ envia notificações por email para usuários que:

* Inscreveram-se em eventos de página, por exemplo, modificação ou replicação.
* Inscreveram-se nos eventos do fórum.
* É necessário executar uma etapa em um fluxo de trabalho.

Consulte [Configuração de notificação](/help/sites-administering/notification.md) por email para obter mais detalhes.

### Ativar impressões de página {#enabling-page-impressions}

As impressões de página são exibidas na coluna **Impressões** do console siteadmin da interface clássica. Para ativar a captura de impressões de página, é necessário configurar:

* Na instância de publicação:

   * [Estatísticas de Página do WCM do Day CQ](/help/sites-deploying/osgi-configuration-settings.md)

* Na instância do autor:

   * [Rastreamento de impressões de página de Adobe](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>A configuração do Controlador de impressões de página de Adobe no ambiente do autor permitirá solicitações anônimas ao serviço de rastreamento.


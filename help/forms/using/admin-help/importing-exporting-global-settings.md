---
title: Importação e exportação de configurações globais
description: Você pode importar e exportar definições de modelo de pesquisa e configurações globais para o Workspace.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---

# Importação e exportação de configurações globais {#importing-and-exporting-global-settings}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Você pode importar e exportar definições de modelo de pesquisa e configurações globais para o Workspace.

>[!NOTE]
>
>O espaço de trabalho do Flex está obsoleto para a versão do AEM forms.

Por exemplo, é possível mover de um ambiente de desenvolvimento para um ambiente de produção exportando as definições do modelo de pesquisa e as configurações globais de um ambiente e importando-as para o outro.

Após exportar o arquivo de configurações globais, você pode modificar as configurações em um editor de texto ou XML. No entanto, as únicas configurações que você pode editar são as configurações JChannelConnectionProperties, formViewOnly e specialRoutes. Para obter mais informações, consulte [configurações globais do Workspace](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>Se você alterar as propriedades do evento no arquivo de configurações globais, será necessário reiniciar o servidor.

## Importar uma definição de modelo de pesquisa {#import-a-search-template-definition}

1. No console de administração, clique em Serviços > Workspace > Administração global.
1. Na caixa Importar Definição de Modelo de Pesquisa, clique em Escolher Arquivo e selecione o modelo de pesquisa. Você só pode importar definições de modelo de pesquisa que foram originalmente exportadas de uma instância do Workspace.
1. Clique em Importar.

## Exportar uma definição de modelo de pesquisa {#export-a-search-template-definition}

1. Na página Administração global, em Exportar definição de modelo de pesquisa, clique em Listar tudo.
1. Na lista de modelos de pesquisa, selecione o modelo a ser exportado.

   >[!NOTE]
   >
   >Você pode selecionar mais de um modelo, mas somente o último modelo selecionado é exportado.

1. Clique em Exportar e salve o arquivo no computador.

## Importar configurações globais {#import-global-settings}

1. Na página Administração global, em Importar configurações globais, clique em Escolher arquivo e selecione o arquivo de configurações globais. O arquivo de configurações globais deve estar no formato XML.
1. Clique em Importar.

## Exportar configurações globais {#export-global-settings}

1. Na página Administração global, em Exportar configurações globais, clique em Exportar.
1. Salve o arquivo no computador.

## Configurações globais do Workspace {#workspace-global-settings}

Você pode modificar o arquivo de configurações globais; no entanto, as únicas configurações que você pode editar são as configurações JChannelConnectionProperties, formViewOnly e specialRoutes.

>[!NOTE]
>
>O espaço de trabalho do Flex está obsoleto para a versão do AEM forms.

O arquivo de configurações globais do Workspace inclui as seguintes configurações:

### configurações specialRoutes {#specialroutes-settings}

As configurações *specialRoutes* especificam as propriedades das rotas especiais, aprovar e negar, no Workspace. Em determinadas situações, os botões dessas rotas aparecem nos cartões de tarefa no Workspace e o usuário pode selecioná-los sem abrir o formulário. Você pode modificar as configurações specialRoutes no arquivo de configurações globais para adicionar nomes personalizados para aprovar e negar ou criar rotas adicionais.

**client_specialRoutes_route_approve_style:** O nome do estilo que está no tema do Workspace, que identifica os ícones do botão de aprovação. O estilo deve incluir valores para um ícone ativado e um ícone desativado. Para definir um estilo para um botão personalizado, você deve usar o seguinte modelo:
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` O arquivo CSS do Workspace está incorporado ao arquivo workspace-theme.swf, que está no arquivo adobe-workspace-client.ear > adobe-workspace-client.war. Para alterar a aparência do Workspace, é necessário recompilar o arquivo workspace-theme.swf.

**client_specialRoutes_route_deny_names:** A variedade de cadeias de caracteres que um usuário do Workbench pode usar para ser interpretada como &quot;negar&quot;. As cadeias de caracteres fazem distinção entre maiúsculas e minúsculas. Por exemplo, o valor padrão é negar. Se o usuário do Workbench usar a palavra Negar em um processo, a palavra não será reconhecida. A palavra Negar deve ser adicionada a essa configuração para que o botão de rota seja personalizado e tenha o estilo aplicado a ele.

**client_specialRoutes_route_deny_style:** O nome do estilo que está no arquivo de temas do Workspace, que identifica os ícones do botão negar. O estilo deve incluir valores para um ícone ativado e um ícone desativado. Para definir um estilo para um botão personalizado, você deve usar o seguinte modelo:
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_route_approve_names:** A variedade de cadeias de caracteres que um usuário do Workbench pode usar para ser interpretada como &quot;aprovar&quot;. As cadeias de caracteres fazem distinção entre maiúsculas e minúsculas. Por exemplo, o valor padrão é aprovar. Se o usuário do Workbench usar a palavra Aprovar em um processo, a palavra não será reconhecida. A palavra Aprovar deve ser adicionada a essa configuração para que o botão de rota seja personalizado e tenha o estilo aplicado a ele.

**client_specialRoutes_names:** as chaves usadas para localizar o valor da cadeia de caracteres personalizada dos arquivos de recurso. Cada entrada nessa configuração precisa incluir os valores para os nomes e o estilo.

### Configurações do JGroup {#jgroup-settings}

Estas configurações só aparecerão se você tiver atualizado do Adobe LiveCycle ES 2.5 ou anterior.

**server_remoteevents_ClientTimeoutMilliseconds:** O tempo máximo que o JGroup aguarda pelas mensagens de evento. Essa configuração não deve ser alterada.

**server_remoteevents_ServerTimeoutMilliseconds:** O tempo limite para receber mensagens JGroup no servidor. Essa opção define o atraso para enviar mensagens do servidor para o cliente.

**server_remoteevents_JChannelConnectionProperties:** as propriedades de conexão para o JGroup usadas para se comunicar entre o servidor (no qual um evento de serviço é processado pelo serviço RemoteEvent) e todas as instâncias do Workspace.

Talvez seja necessário alterar os valores de UDP do endereço IP de multicast (mcast_addr), da porta IP de multicast (mcast_port) e do TTL dos pacotes de multicast (ip_ttl). Por padrão, os valores de porta e endereço IP de multicast são gerados aleatoriamente e, geralmente, os valores não precisam ser alterados. No entanto, se sua empresa tiver quaisquer políticas de rede relacionadas a intervalos de multicast específicos para endereços IP de multicast, talvez seja necessário alterar os valores.

>[!NOTE]
>
>O TTL deve ser maior que o número de switches de rede entre os servidores no cluster; no entanto, se o valor for definido como muito alto, poderá fazer com que pacotes multicast viajem para sub-redes, onde serão descartados.

As propriedades restantes nessa configuração não devem ser alteradas.

**server_remoteevents_JGroupName:** O nome do JGroup usado para comunicação de evento remoto. Esse valor é gerado aleatoriamente para evitar conflitos em clusters. Esse valor não deve ser alterado.

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### configurações de formView {#formview-settings}

**client_formView_openFormInFullScreen:** Para exibir todos os formulários no Workspace no modo de tela cheia, defina esta opção como true. Por padrão, essa opção está definida como falsa e os formulários não são exibidos no modo de tela cheia. O serviço do Usuário contém uma opção para abrir o documento associado a uma tarefa no modo de tela cheia. Isso permite controlar a exibição com base no processo.

**client_rows_formViewOnly:** Quando definido como True, as rotas não são exibidas na exibição de cartão ou na exibição de lista no Workspace. O valor padrão é Falso, o que significa que as rotas são exibidas na exibição de cartão e na exibição de lista.

### Outras configurações {#other-settings}

**client_mimeTypes_openOutsideBrowser:** o tipo MIME de documentos que são abertos fora da instância do navegador Workspace. Se os processos da sua organização exigirem um tipo MIME adicional, especifique-o aqui. Os valores padrão são:

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** armazena em cache uma interface de usuário de tarefa personalizada.

**server_debugLevel:** Não altere esta configuração.

**client_pollingInterval:** define o intervalo de sondagem (em segundos) usado no Flex Workspace (obsoleto para formulários AEM no JEE) para detectar tarefas novas e modificadas. O padrão é 3 segundos. Isso não funciona no AEM Forms Workspace.

**client_systemContext_name:** especifique um nome personalizado (por exemplo, Cidadão) a ser exibido no campo Adicionado por (na guia Anexos) para os anexos de uma tarefa no AEM Forms Workspace.

Para definir o nome personalizado:

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Para o aplicativo de demonstração, o nome para exibição padrão é **Cidadão**. Para um aplicativo personalizado que você cria, o nome para exibição padrão é **Conta de Contexto do Sistema**.
>
>**client_idleTimeout:** quando um usuário permanece inativo por um período específico, a sessão do AEM Forms Workspace expira. Para habilitar o recurso, adicione uma entrada às Configurações Globais &lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>. Você pode especificar o valor 0 para desativar o tempo limite ocioso. O tempo é especificado em segundos.

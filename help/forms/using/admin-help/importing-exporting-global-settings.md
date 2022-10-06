---
title: Importação e exportação de configurações globais
seo-title: Importing and exporting global settings
description: Você pode importar e exportar definições de modelo de pesquisa e configurações globais para o Workspace.
seo-description: You can import and export search template definitions and global settings for Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---

# Importação e exportação de configurações globais {#importing-and-exporting-global-settings}

Você pode importar e exportar definições de modelo de pesquisa e configurações globais para o Workspace.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão AEM formulários.

Por exemplo, é possível mover de um ambiente de desenvolvimento para um ambiente de produção exportando as definições do modelo de pesquisa e as configurações globais de um ambiente e importando-as para outro.

Após exportar o arquivo de configurações globais, você pode modificar as configurações em um editor de XML ou texto. No entanto, as únicas configurações que você deseja editar são as configurações JChannelConnectionProperties, formViewOnly e SpecialRoutes. Para obter mais informações, consulte [Configurações globais do Workspace](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>Se você alterar as propriedades do evento no arquivo de configurações globais, deverá reiniciar o servidor.

## Importar uma definição de modelo de pesquisa {#import-a-search-template-definition}

1. No console de administração, clique em Serviços > Workspace > Administração global.
1. Na caixa Importar definição do modelo de pesquisa, clique em Escolher arquivo e selecione o modelo de pesquisa. Você só pode importar definições de modelo de pesquisa que foram originalmente exportadas de uma instância do Workspace.
1. Clique em Importar.

## Exportar uma definição de modelo de pesquisa {#export-a-search-template-definition}

1. Na página Administração global , em Exportar definição de modelo de pesquisa, clique em Listar tudo.
1. Na lista de modelos de pesquisa, selecione o modelo a ser exportado.

   >[!NOTE]
   >
   >Você pode selecionar mais de um modelo, mas somente o último modelo selecionado é exportado.

1. Clique em Exportar e salve o arquivo em seu computador.

## Importar configurações globais {#import-global-settings}

1. Na página Administração global , em Importar configurações globais, clique em Escolher arquivo e selecione o arquivo de configurações globais. O arquivo de configurações globais deve estar no formato XML.
1. Clique em Importar.

## Exportar configurações globais {#export-global-settings}

1. Na página Administração global , em Exportar configurações globais, clique em Exportar.
1. Salve o arquivo em seu computador.

## Configurações globais do Workspace {#workspace-global-settings}

Você pode modificar o arquivo de configurações globais; no entanto, as únicas configurações que você deseja editar são as configurações JChannelConnectionProperties, formViewOnly e specialRoutes.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão AEM formulários.

O arquivo de configurações globais do Workspace inclui as seguintes configurações:

### configurações especiaisRoutes {#specialroutes-settings}

O *specialRoutes* As configurações especificam as propriedades das rotas especiais, aprovam e negam, no Workspace. Em determinadas situações, os botões dessas rotas são exibidos nos cartões de tarefa no Workspace e o usuário pode selecioná-los sem abrir o formulário. Você pode modificar as configurações especiaisRoutes no arquivo de configurações globais para adicionar nomes personalizados para aprovar e negar ou para criar rotas adicionais.

**client_SpecialRoutes_route_approve_style:** O nome do estilo localizado no tema do Workspace, que identifica os ícones do botão aprovar. O estilo deve incluir valores para um ícone ativado e desativado. Para definir um estilo para um botão personalizado, você deve usar o seguinte template:
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` O arquivo CSS do Workspace é incorporado ao arquivo workspace-theme.swf, que está localizado no arquivo adobe-workspace-client.ear > adobe-workspace-client.war. Para alterar a aparência do Workspace, você deve recompilar o arquivo workspace-theme.swf .

**client_SpecialRoutes_route_deny_names:** A variedade de strings que um usuário do Workbench pode usar para ser interpretado como &quot;negar&quot;. As cadeias de caracteres fazem distinção entre maiúsculas e minúsculas. Por exemplo, o valor padrão é negar. Se o usuário do Workbench usar a palavra Negar em um processo, a palavra não será reconhecida. A palavra Negar deve ser adicionada a essa configuração para que o botão de rota seja personalizado e tenha o estilo aplicado a ele.

**client_SpecialRoutes_route_deny_style:** O nome do estilo localizado no arquivo de tema do Workspace, que identifica os ícones do botão negar. O estilo deve incluir valores para um ícone ativado e desativado. Para definir um estilo para um botão personalizado, você deve usar o seguinte template:
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_SpecialRoutes_route_approve_names:** A variedade de strings que um usuário do Workbench pode usar para ser interpretado como &quot;aprovar&quot;. As cadeias de caracteres fazem distinção entre maiúsculas e minúsculas. Por exemplo, o valor padrão é aprovar. Se o usuário do Workbench usar a palavra Aprovar em um processo, a palavra não será reconhecida. A palavra Aprovar deve ser adicionada a essa configuração para que o botão de rota seja personalizado e tenha o estilo aplicado a ele.

**client_SpecialRoutes_names:** As chaves usadas para localizar o valor da string personalizada dos arquivos de recurso. Cada entrada nessa configuração precisa incluir os valores para os nomes e o estilo.

### Configurações do JGroup {#jgroup-settings}

Essas configurações aparecem somente se você tiver atualizado do Adobe LiveCycle ES 2.5 ou anterior.

**server_remoteevents_ClientTimeoutMilliseconds:** O tempo máximo que o JGroup aguarda para mensagens de evento. Esta configuração não deve ser alterada.

**server_remoteevents_ServerTimeoutMilliseconds:** O tempo limite para receber mensagens JGroup no servidor. Essa opção define o atraso para enviar mensagens do servidor para o cliente.

**server_remoteevents_JChannelConnectionProperties:** As propriedades de conexão do JGroup que são usadas para se comunicar entre o servidor (no qual um evento de serviço é processado pelo serviço RemoteEvent) e todas as instâncias do Workspace.

Talvez seja necessário alterar os valores do UDP para o endereço IP de multicast (mcast_addr), a porta IP de multicast (mcast_port) e o TTL para os pacotes de multicast (ip_ttl). Por padrão, o endereço IP multicast e os valores de porta são gerados aleatoriamente e, em geral, os valores não precisam ser alterados. No entanto, se sua empresa tiver políticas de rede relacionadas a intervalos de multicast específicos para endereços IP de multicast, talvez seja necessário alterar os valores.

>[!NOTE]
>
>O TTL deve ser superior ao número de switches de rede entre os servidores do cluster; no entanto, se o valor for definido como muito alto, poderá fazer com que pacotes multicast viajem para sub-redes, onde serão descartados.

As propriedades restantes nessa configuração não devem ser alteradas.

**server_remoteevents_JGroupName:** O nome do JGroup usado para comunicação de evento remoto. Esse valor é gerado aleatoriamente para evitar conflitos em clusters. Este valor não deve ser alterado.

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### configurações do formView {#formview-settings}

**client_formView_openFormInFullScreen:** Para exibir todos os formulários no Workspace no modo de tela cheia, defina essa opção como true. Por padrão, essa opção é definida como false e os formulários não são exibidos no modo de tela cheia. Observe que o serviço Usuário contém uma opção para abrir o documento associado a uma tarefa no modo de tela cheia. Isso permite controlar a exibição de acordo com o processo.

**client_route_formViewOnly:** Quando definido como Verdadeiro, as rotas não são exibidas na exibição de cartão ou na exibição de lista no Workspace. O valor padrão é Falso, o que significa que as rotas são exibidas na exibição de cartão e na exibição de lista.

### Outras configurações {#other-settings}

**client_mimeTypes_openOutsideBrowser:** O tipo MIME de documentos que serão abertos fora da instância do navegador do Workspace. Se os processos de sua organização exigirem um tipo MIME adicional, especifique-o aqui. Os valores padrão são:

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** Armazena em cache uma interface de usuário de tarefa personalizada.

**server_debugLevel:** Não altere esta configuração.

**client_pollingInterval:** Define o intervalo de sondagem (em segundos) usado no (Obsoleto para formulários AEM no JEE) Flex Workspace para detectar tarefas novas e modificadas. O padrão é 3 segundos. Isso não funciona no AEM Forms Workspace.

**client_systemContext_name:** Especifique um nome personalizado (por exemplo, Cidadão) para exibir no campo Adicionado por (na guia Anexos ) para os anexos de uma tarefa no AEM Forms Workspace.

Para definir o nome personalizado:

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Para o aplicativo Demo, o nome de exibição padrão é **Cidadão**. Para um aplicativo personalizado criado, o nome de exibição padrão é **Conta de Contexto do Sistema**.
>
>**client_idleTimeout:** Quando um usuário permanece inativo por um período específico, a sessão do AEM Forms Workspace expira. Para ativar o recurso, adicione uma entrada às Configurações globais &lt;client_idletimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idletimeout>. Você pode especificar o valor 0 para desativar o tempo limite de ociosidade. A quantidade de tempo é especificada em segundos.

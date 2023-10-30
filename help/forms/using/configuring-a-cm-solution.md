---
title: Configurar uma solução de gerenciamento de correspondência
description: Configure uma solução de Gerenciamento de correspondência no ambiente do AEM Forms.
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# Configurar uma solução de gerenciamento de correspondência {#configuring-a-correspondence-management-solution}

## Definindo o URL da instância do autor para VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Use as etapas a seguir para definir um URL da instância do autor para a restauração da versão da instância do autor:

1. Ir para *https://:&lt;publishhost>:&lt;publishport>/lc/system/console/configMgr*. Faça logon com as credenciais de usuário do Console de gerenciamento OSGi. As credenciais padrão são admin/admin.
1. Localize e clique no link **[!UICONTROL Editar]** ícone ao lado do **[!UICONTROL com.adobe.livecycle.content.ativate.impl.VersionRestoreManagerImpl.name]** configuração.
1. No **[!UICONTROL URL do autor do VersionRestoreManager]** especifique a URL da instância do Autor de VersionRestoreManager.

   **String de URL**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Se houver várias instâncias de autor (Clusterizadas) com um Balanceador de carga, especifique o URL para o balanceador de carga no **[!UICONTROL URL do autor do VersionRestoreManager]** campo.

1. Clique em **[!UICONTROL Salvar]**.

## Definição do URL da instância de publicação para AtivationManagerImpl (gerenciador de ativação da instância pública) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Siga estas etapas para definir o URL da instância de publicação para o gerenciador de ativação da instância pública:

1. Ir para *https://:&lt;authorhost>:&lt;authorport>/lc/system/console/configMgr*. Faça logon com as credenciais de usuário do Console de gerenciamento OSGi. As credenciais padrão são admin/admin.
1. Localize e clique no link **[!UICONTROL Editar]** ícone ao lado do **[!UICONTROL com.adobe.livecycle.content.ativate.impl.AtivationManagerImpl.name]** configuração.
1. No **[!UICONTROL URL de publicação do AtivationManager]** especifique o URL para acessar o AtivationManager da instância de publicação. Você pode fornecer os seguintes URLs.

   * **URL do Balanceador de Carga (Recomendado)**: forneça o URL do balanceador de carga, se você tiver um servidor da Web que atue como balanceador de carga na frente do farm de publicação (várias instâncias de publicação não clusterizadas).
   * **URL da instância de publicação**: forneça qualquer URL de instância de publicação, se você tiver uma única instância de publicação ou se o servidor da Web que lidera o farm de publicação não estiver acessível no ambiente de criação devido a quaisquer restrições. Caso a instância de publicação especificada esteja inativa, há um mecanismo de fallback que deve ser tratado no lado do autor.
   * **String de URL**:

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Clique em **[!UICONTROL Salvar]**.

Para obter mais informações sobre como configurar o Gerenciamento de correspondência, consulte [Propriedades de configuração do gerenciamento de correspondência](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).

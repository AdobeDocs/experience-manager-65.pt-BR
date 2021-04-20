---
title: Configuração de uma solução de gerenciamento de correspondência
seo-title: Configuração de uma solução de gerenciamento de correspondência
description: Configuração de uma solução de gerenciamento de correspondência
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---


# Configurar uma solução de gerenciamento de correspondência {#configuring-a-correspondence-management-solution}

## Definindo o URL da instância do autor para VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Use as seguintes etapas para definir um URL de instância do autor para a restauração da versão da instância do autor:

1. Vá para *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Faça logon com as credenciais do usuário do Console de Gerenciamento OSGi. As credenciais padrão são admin/admin.
1. Encontre e clique no ícone **[!UICONTROL Edit]** ao lado da configuração **[!UICONTROL com.adobe.livecycle.content.ativate.impl.VersionRestoreManagerImpl.name]**.
1. No campo **[!UICONTROL VersionRestoreManager Author URL]**, especifique o URL da instância do autor de VersionRestoreManager.

   **Sequência** de URL:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Se houver várias instâncias de autor (em cluster) diante de um Balanceador de carga, especifique o URL para o balanceador de carga no campo **[!UICONTROL VersionRestoreManager Author URL]**.

1. Clique em **[!UICONTROL Salvar]**.

## Definição do URL da instância de publicação para AtivationManagerImpl (gerenciador de ativação da instância pública) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Siga estas etapas para definir o URL da instância de publicação para o gerenciador de ativação da instância pública:

1. Vá para *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Faça logon com as credenciais do usuário do Console de Gerenciamento OSGi. As credenciais padrão são admin/admin.
1. Localize e clique no ícone **[!UICONTROL Edit]** ao lado da configuração **[!UICONTROL com.adobe.livecycle.content.ativate.impl.AtivationManagerImpl.name]**.
1. No campo **[!UICONTROL URL de publicação do AtivationManager]**, especifique o URL para acessar a instância de publicação do AtivationManager. Você pode fornecer os seguintes URLs.

   * **URL do Balanceador de Carga (Recomendado)**: Forneça o URL do balanceador de carga. Caso tenha um servidor da Web atuando como balanceador de carga na frente do farm de publicação (várias instâncias de publicação sem cluster).
   * **URL** da instância de publicação: Forneça qualquer URL de instância de publicação. Se você tiver uma única instância de publicação ou o servidor da Web que encaminha o farm de publicação não estiver acessível a partir do ambiente do autor devido a quaisquer restrições. Caso a instância de publicação especificada esteja inativa, há um mecanismo de fallback com o qual lidar no lado do autor.
   * **Sequência** de URL:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Clique em **[!UICONTROL Salvar]**.

Para obter mais informações sobre como configurar o Gerenciamento de correspondência, consulte [Propriedades de configuração do Gerenciamento de correspondência](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).

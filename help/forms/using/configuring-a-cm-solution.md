---
title: Configuração de uma solução de Gerenciamento de correspondência
seo-title: Configuração de uma solução de Gerenciamento de correspondência
description: Configuração de uma solução de Gerenciamento de correspondência
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 1%

---


# Configuração de uma solução de Gerenciamento de correspondência {#configuring-a-correspondence-management-solution}

## Definindo o URL da instância do autor para VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Use as seguintes etapas para definir um URL de instância do autor para a restauração da versão da instância do autor:

1. Vá para *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Faça logon com as credenciais de usuário do Console de gerenciamento OSGi. As credenciais padrão são admin/admin.
1. Localize e clique no ícone **[!UICONTROL Editar]** ao lado da configuração **[!UICONTROL com.adobe.livecycle.content.ativate.impl.VersionRestoreManagerImpl.name]** .
1. No campo URL **[!UICONTROL do autor do]** VersionRestoreManager, especifique o URL da instância do autor do VersionRestoreManager.

   **Sequência** de caracteres do URL:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Se houver várias instâncias do autor (em cluster) encaminhadas por um Balanceador de Carga, especifique o URL para o balanceador de carga no campo URL **[!UICONTROL do autor]** VersionRestoreManager.

1. Clique em **[!UICONTROL Salvar]**.

## Definindo o URL da instância de publicação para AtivationManagerImpl (gerenciador de ativação de instância pública) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Siga estas etapas para definir o URL da instância de publicação para o gerenciador de ativações de instância pública:

1. Vá para *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Faça logon com as credenciais de usuário do Console de gerenciamento OSGi. As credenciais padrão são admin/admin.
1. Localize e clique no ícone **[!UICONTROL Editar]** ao lado da configuração **[!UICONTROL com.adobe.livecycle.content.ativation.impl.AtivationManagerImpl.name]** .
1. No campo URL **[!UICONTROL de publicação do]** ActivationManager, especifique o URL para acessar a instância de publicação do ActivationManager. Você pode fornecer os seguintes URLs.

   * **URL do Balanceador de Carga (Recomendado)**: Forneça o URL do balanceador de carga. Se você tiver um servidor Web agindo como balanceador de carga na frente do farm de publicação (várias instâncias de publicação não clusterizadas).
   * **URL** da instância de publicação: Forneça qualquer URL de instância de publicação. Se você tiver uma única instância de publicação ou o servidor Web que encaminha o farm de publicação não estiver acessível do ambiente do autor devido a quaisquer restrições. Caso a instância de publicação especificada esteja inativa, há um mecanismo de fallback a ser tratado no lado do autor.
   * **Sequência** de caracteres do URL:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Clique em **[!UICONTROL Salvar]**.

Para obter mais informações sobre como configurar o Gerenciamento de correspondência, consulte Propriedades [de configuração do Gerenciamento de](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)correspondência.

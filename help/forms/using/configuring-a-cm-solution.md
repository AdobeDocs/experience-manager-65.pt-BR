---
title: Configurar uma solução de gerenciamento de correspondência
description: Saiba como configurar uma solução de Gerenciamento de correspondência em um ambiente do AEM Forms.
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 1%
---
# Configurar uma solução de gerenciamento de correspondência {#configuring-a-correspondence-management-solution}

## Definindo o URL da instância do autor para VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Use as etapas a seguir para definir um URL da instância do autor para a restauração da versão da instância do autor:

1. Acesse *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Faça logon com as credenciais de usuário do Console de gerenciamento OSGi. As credenciais padrão são admin/admin.
1. Localize e clique no ícone **[!UICONTROL Editar]** ao lado da configuração **[!UICONTROL com.adobe.livecycle.content.ativate.impl.VersionRestoreManagerImpl.name]**.
1. No campo **[!UICONTROL URL do Autor de VersionRestoreManager]**, especifique a URL da instância do Autor de VersionRestoreManager.

   **cadeia de caracteres de URL**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Se houver várias instâncias de autor (Clusterizadas) com base em um Balanceador de Carga, especifique a URL para o balanceador de carga no campo **[!UICONTROL URL do Autor de VersionRestoreManager]**.

1. Clique em **[!UICONTROL Salvar]**.

## Definição do URL da instância de publicação para AtivationManagerImpl (gerenciador de ativação da instância pública) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Siga estas etapas para poder definir o URL da instância de publicação para o gerenciador de ativação da instância pública:

1. Vá para *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Faça logon com as credenciais de usuário do Console de gerenciamento OSGi. As credenciais padrão são admin/admin.
1. Localize e clique no ícone **[!UICONTROL Editar]** ao lado da configuração **[!UICONTROL com.adobe.livecycle.content.ativate.impl.AtivationManagerImpl.name]**.
1. No campo **[!UICONTROL Publicar URL]** do AtivationManager, especifique a URL para acessar o AtivationManager da instância de publicação. Você pode fornecer os seguintes URLs.

   * **URL do Balanceador de Carga (Recomendado)**: Forneça a URL do balanceador de carga, caso você tenha um servidor Web que atue como balanceador de carga na frente do farm de publicação (várias instâncias de publicação não clusterizadas).
   * **URL da instância de publicação**: forneça qualquer URL da instância de publicação, se você tiver uma única instância de publicação ou se o servidor Web que está à frente do farm de publicação não estiver acessível do ambiente de criação devido a restrições. Caso a instância de publicação especificada esteja inativa, há um mecanismo de fallback que deve ser tratado no lado do autor.
   * **cadeia de caracteres de URL**:

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Clique em **[!UICONTROL Salvar]**.

Para obter mais informações sobre como configurar o Gerenciamento de Correspondências, consulte [Propriedades de Configuração do Gerenciamento de Correspondências](https://helpx.adobe.com/br/aem-forms/6-2/cm-configuration-properties.html).

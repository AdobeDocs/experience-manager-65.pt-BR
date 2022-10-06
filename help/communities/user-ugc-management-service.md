---
title: Serviço de gerenciamento de usuários e UGC no AEM Communities
seo-title: User and UGC Management Service in AEM Communities
description: Use APIs para excluir e exportar em massa conteúdo gerado pelo usuário e desative a conta do usuário.
seo-description: Use APIs to bulk delete and bulk export user generated content, and disable user account.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Serviço de gerenciamento de usuários e UGC no AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>O GDPR é usado como exemplo nas seções abaixo, mas os detalhes cobertos são aplicáveis a todas as regulamentações de proteção e privacidade de dados; como GDPR, CCPA etc.

O AEM Communities expõe as APIs prontas para uso para gerenciar perfis de usuários e conteúdo gerado por usuários (UGC) em massa. Depois de habilitado, a variável **UserUgcManagement** permite que usuários privilegiados (administradores de comunidade e moderadores) desabilitem perfis de usuário e excluam em massa ou exportem em massa o UGC para usuários específicos. Essas APIs também permitem que controladores e processadores de dados do cliente cumpram os Regulamentos Gerais de Proteção de Dados (GDPR) da União Europeia e outras regras de privacidade inspiradas no GDPR.

Para obter mais informações, consulte o [Página do GDPR no Centro de privacidade do Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Se você tiver configurado [Adobe Analytics no AEM Communities](/help/communities/analytics.md) no site, os dados do usuário capturados são enviados para o servidor do Adobe Analytics. O Adobe Analytics fornece APIs que permitem acessar, exportar e excluir dados do usuário, além de estar em conformidade com o GDPR. Para obter mais informações, consulte [Enviar solicitações de acesso e de exclusão](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html).

Para usar essas APIs, é necessário ativar a variável `/services/social/ugcmanagement` endpoint ativando o serviço UserUgcManagement. Para ativar esse serviço, instale o [servlet de amostra](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) disponível em [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). Em seguida, pressione o endpoint na instância de publicação do site das comunidades com parâmetros apropriados usando uma solicitação http, semelhante a:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. No entanto, também é possível criar uma interface do usuário (interface do usuário) para gerenciar perfis de usuário e conteúdo gerado pelo usuário no sistema.

Essas APIs ativadas executam as seguintes funções.

## Recuperar o UGC de um usuário {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** ajuda a exportar todo o UGC de um usuário do sistema.

* **usuário**: ID autorizável de um usuário.
* **outputStream**: O resultado é retornado como fluxo de saída, que é um arquivo zip, incluindo o conteúdo gerado pelo usuário (como arquivo json) e anexos (que incluem imagens ou vídeos carregados pelo usuário).

Por exemplo, para exportar o UGC de um usuário chamado Weston McCall, que usa weston.mccall@dodgit.com como ID autorizável para fazer logon no site de comunidades, você pode enviar uma solicitação de http GET semelhante ao seguinte:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Excluir o UGC de um usuário {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** ajuda a excluir todo o UGC de um usuário do sistema.

* **usuário**: ID autorizável do usuário.

Por exemplo, para excluir o UGC de um usuário que tenha uma ID autorizável weston.mccall@dodgit.com por meio de uma solicitação http-POST, use os seguintes parâmetros:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Excluir UGC do Adobe Analytics {#delete-ugc-from-adobe-analytics}

Para excluir dados do usuário da Adobe Analytics, siga as [Fluxo de trabalho do GDPR Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html); já que a API não exclui dados do usuário do Adobe Analytics.

Para mapeamentos de variáveis Adobe Analytics usados pelo AEM Communities, consulte a seguinte imagem:

![Mapeamento de variável de comunidades AEM para o Adobe Analytics](assets/analytics-communities-mapping.png)

## Desativar uma conta de usuário {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, usuário String)** ajuda a desativar uma conta de usuário.

* **usuário**: ID autorizável do usuário.

>[!NOTE]
>
>Desativar um usuário exclui todo o conteúdo gerado pelo usuário que ele tem no servidor.

Por exemplo, para excluir o perfil de um usuário com ID autorizável `weston.mccall@dodgit.com` por meio da solicitação http-POST, use os seguintes parâmetros:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>A API deleteUserAccount() desativa somente um perfil de usuário no sistema e remove o UGC. No entanto, para excluir um perfil de usuário do sistema, navegue até **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), localize o nó do usuário e exclua-o.

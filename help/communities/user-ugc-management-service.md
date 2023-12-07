---
title: Serviço de gerenciamento de usuários e UGC no AEM Communities
description: Use APIs para excluir e exportar em massa o conteúdo gerado pelo usuário e desabilitar a conta do usuário.
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# Serviço de gerenciamento de usuários e UGC no AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>O GDPR é usado como exemplo nas seções abaixo, mas os detalhes abordados se aplicam a todas as regulamentações de proteção e privacidade de dados; como o GDPR, CCPA e assim por diante.

O AEM Communities expõe APIs prontas para uso para gerenciar perfis de usuários e gerenciar conteúdo gerado pelo usuário (UGC) em massa. Uma vez habilitado, o **UserUgcManagement** o serviço permite que os usuários privilegiados (administradores e moderadores da comunidade) desativem perfis de usuários e excluam ou exportem em massa o UGC para usuários específicos. Essas APIs também permitem que controladores e processadores de dados do cliente estejam em conformidade com os Regulamentos Gerais de Proteção de Dados (GDPR) da União Europeia e outras determinações de privacidade inspiradas no GDPR.

Para obter mais informações, consulte a [Página do GDPR no Centro de privacidade do Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Se você configurou o [Adobe Analytics no AEM Communities](/help/communities/analytics.md) site, os dados capturados do usuário são enviados ao servidor do Adobe Analytics. O Adobe Analytics fornece APIs que permitem acessar, exportar e excluir dados do usuário e estar em conformidade com o GDPR. Para obter mais informações, consulte [Enviar solicitações de acesso e de exclusão](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

Para colocar essas APIs em uso, é necessário ativar o `/services/social/ugcmanagement` ativando o serviço UserUgcManagement. Para ativar esse serviço, instale o [servlet de amostra](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) disponível em [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). Em seguida, acesse o endpoint na instância de publicação do site de comunidades com parâmetros apropriados usando uma solicitação http, semelhante a:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. No entanto, também é possível criar uma interface do usuário (interface do usuário) para gerenciar perfis de usuário e conteúdo gerado pelo usuário no sistema.

Essas APIs permitem executar as seguintes funções.

## Recuperar o UGC de um usuário {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, usuário de cadeia de caracteres, OutputStream outputStream)** O ajuda a exportar todo o UGC de um usuário do sistema.

* **usuário**: ID autorizável de um usuário.
* **outputStream**: o resultado é retornado como um fluxo de saída, que é um arquivo zip que inclui o conteúdo gerado pelo usuário (como arquivo json) e anexos (que incluem imagens ou vídeos carregados pelo usuário).

Por exemplo, para exportar o UGC de um usuário chamado Weston McCall, que usa weston.mccall@dodgit.com como ID autorizável para fazer logon no site de comunidades, você pode enviar uma solicitação http GET semelhante à seguinte:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Excluir o UGC de um usuário {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, Usuário de cadeia de caracteres)** ajuda a excluir do sistema todo o UGC de um usuário.

* **usuário**: ID autorizável do usuário.

Por exemplo, para excluir o UGC de um usuário com ID autorizável weston.mccall@dodgit.com por meio da solicitação http-POST, use os seguintes parâmetros:

* usuário = `weston.mccall@dodgit.com`
* operação = `deleteUgc`

### Excluir UGC do Adobe Analytics {#delete-ugc-from-adobe-analytics}

Para excluir dados do usuário da Adobe Analytics, siga as [Fluxo de trabalho do GDPR Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=pt-BR); já que a API não exclui dados do usuário do Adobe Analytics.

Para ver os mapeamentos de variáveis do Adobe Analytics usados pelo AEM Communities, consulte a seguinte imagem:

![Mapeamento de variáveis de comunidades AEM para o Adobe Analytics](assets/analytics-communities-mapping.png)

## Desativar uma conta de usuário {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, Usuário de cadeia de caracteres)** ajuda a desativar uma conta de usuário.

* **usuário**: ID autorizável do usuário.

>[!NOTE]
>
>A desativação de um usuário exclui todo o conteúdo gerado pelo usuário que ele tem no servidor.

Por exemplo, para excluir o perfil de um usuário com ID autorizável `weston.mccall@dodgit.com` por meio da solicitação http-POST, use os seguintes parâmetros:

* usuário = `weston.mccall@dodgit.com`
* operação = `deleteUser`

>[!NOTE]
>
>A API deleteUserAccount() desativa apenas um perfil de usuário no sistema e remove o UGC. No entanto, para excluir um perfil de usuário do sistema, navegue até **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), localize o nó do usuário e exclua-o.

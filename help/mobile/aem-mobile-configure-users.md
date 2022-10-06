---
title: Configurar usuários e grupos de usuários
seo-title: Configure Your Users and User Groups
description: Siga esta página para entender as funções do usuário e como configurar usuários e grupos para dar suporte à criação e ao gerenciamento de seu aplicativo móvel On-Demand Services.
seo-description: Follow this page to understand the user roles and how to configure your users and groups to support the authoring and mangement of your mobile On-Demand services app.
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Configurar usuários e grupos de usuários {#configure-your-users-and-user-groups}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Este capítulo descreve as funções do usuário e como configurar usuários e grupos para dar suporte à criação e ao gerenciamento de seus aplicativos móveis.

## Usuários e administração de grupo do aplicativo AEM Mobile {#aem-mobile-application-users-and-group-administration}

### Autores de conteúdo do aplicativo AEM Mobile (grupo de autores do aplicativo) {#aem-mobile-application-content-authors-app-author-group}

Os membros do grupo de autores do aplicativo são responsáveis pela criação AEM conteúdo do aplicativo móvel, incluindo páginas, texto, imagens e vídeos.

#### Configuração de grupo - autores de aplicativos {#group-configuration-app-authors}

1. Crie um novo grupo de usuários chamado &quot;autores de aplicativos&quot;:

   Navegue até o Admin Console do usuário: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   No console do grupo de usuários, selecione o botão &quot;+&quot; para criar um grupo.

   Defina a ID desse grupo como &quot;autores de aplicativos&quot; para indicar que é um tipo específico de grupo de usuários de criação específico para a criação de aplicativos móveis no AEM.

1. Adicionar membro ao grupo: Autores

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Agora que você criou o Grupo de usuários autores de aplicativos, é possível adicionar membros individuais da equipe a esse novo grupo por meio do [Console de administração do usuário](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. O seguinte permite adicionar AEM Grupo de autores de conteúdo:

   (Leia) em

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### Grupo de administradores de aplicativos do AEM Mobile (grupo de administradores de aplicativos) {#aem-mobile-application-administrators-group-app-admins-group}

Membros do grupo app-admins podem criar conteúdo do aplicativo com as mesmas permissões incluídas com autores de aplicativos **E** além disso, são também responsáveis por:

* Preparando, publicando e limpando atualizações do aplicativo ContentSync OTA

>[!NOTE]
>
>As permissões determinam a disponibilidade de algumas ações do usuário no AEM App Command Center.
>
>Você observará que algumas opções não estão disponíveis para autores de aplicativos que estão disponíveis para administradores de aplicativos.

### Configuração de grupo - app-admins {#group-configuration-app-admins}

1. Crie um novo grupo chamado app-admins.
1. Adicione os seguintes grupos ao seu novo grupo de administradores de aplicativos:

   * autores de conteúdo
   * usuários de fluxo de trabalho

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >os usuários do workflow são necessários para criar remotamente com o serviço de PhoneGap Build

1. Navegue até o [Console de permissões](http://localhost:4502/useradmin) e adicionar permissões para administrar cloudservices

   * (Ler, Modificar, Criar, Excluir, Replicar) em /etc/cloudservices/mobileservices

1. No mesmo console Permissões, adicione permissões para preparar, publicar e limpar atualizações de conteúdo do aplicativo;

   * (Ler, Modificar, Criar, Excluir, Replicar) em /etc/packages/mobileapp
   * (Leia) em /var/contentsync

   >[!NOTE]
   >
   >A replicação de pacotes é usada para publicar atualizações de aplicativos da instância de autor na instância de publicação

   >[!CAUTION]
   >
   >O acesso a /var/contentsync é negado ao OOTB.
   >
   >A omissão da permissão READ pode resultar na criação e replicação de pacotes de atualização vazios.

1. Adicionar membros a este grupo, conforme necessário
1. Para exportar conteúdo ou fazer upload

   * (Leia) em /etc/contentsync para acessar modelos de exportação
   * (Leitura) em /var para para trajeto de caminho em leituras
   * (Ler, Gravar, Modificar, Excluir) em /var/contentsync para gravar, ler e limpar conteúdo de exportação em cache do ContentSync

### Recursos adicionais {#additional-resources}

Para entender mais sobre as outras duas funções e responsabilidades para criar um aplicativo AEM Mobile On-demand Services, consulte os seguintes recursos:

* [Desenvolvimento de conteúdo AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Criação de conteúdo AEM para aplicativo AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

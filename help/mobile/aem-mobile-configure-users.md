---
title: Configurar usuários e grupos de usuários
seo-title: Configurar usuários e grupos de usuários
description: Siga esta página para entender as funções do usuário e como configurar seus usuários e grupos para suportar a criação e o gerenciamento do aplicativo móvel On-Demand Services.
seo-description: Siga esta página para entender as funções do usuário e como configurar seus usuários e grupos para suportar a criação e o gerenciamento do aplicativo móvel On-Demand Services.
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurar usuários e grupos de usuários {#configure-your-users-and-user-groups}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Este capítulo descreve as funções do usuário e como configurar seus usuários e grupos para suportar a criação e o gerenciamento de seus aplicativos móveis.

## Usuários e administração de grupos do aplicativo AEM Mobile {#aem-mobile-application-users-and-group-administration}

### Autores de conteúdo do aplicativo AEM Mobile (grupo de autores do aplicativo) {#aem-mobile-application-content-authors-app-author-group}

Os membros do grupo de autores do aplicativo são responsáveis pela criação de conteúdo do aplicativo AEM móvel, incluindo páginas, texto, imagens e vídeos.

#### Configuração de grupo - app-autores {#group-configuration-app-authors}

1. Crie um novo grupo de usuários chamado &quot;app-autores&quot;:

   Navegue até o Console de administração do usuário: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   No console do grupo de usuários, selecione o botão &#39;+&#39; para criar um grupo.

   Defina a ID desse grupo como &quot;app-autores&quot; para indicar que é um tipo específico de grupo de usuários do autor específico para a criação de aplicativos móveis no AEM.

1. Adicionar membro ao grupo: Autores

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Agora que você criou o Grupo de usuários de autores de aplicativos, é possível adicionar membros individuais da equipe a esse novo grupo por meio do console [Administrador de](http://localhost:4502/libs/granite/security/content/useradmin.md)usuários.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. O seguinte permite que você adicione ao grupo de autores de conteúdo do AEM:

   (Lido) em

   * /app
   *  /etc/clientlibs
   *  /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile Application Administrators Group (grupo de administradores de aplicativos) {#aem-mobile-application-administrators-group-app-admins-group}

Os membros do grupo app-admins podem criar conteúdo do aplicativo com as mesmas permissões incluídas com os autores do aplicativo **E** , além disso, são responsáveis por:

* Preparação, publicação e limpeza de atualizações do ContentSync OTA do aplicativo

>[!NOTE]
>
>As permissões determinam a disponibilidade de algumas ações do usuário no AEM App Command Center.
>
>Você notará que algumas opções não estão disponíveis para autores de aplicativos que estão disponíveis para administradores de aplicativos.

### Configuração de grupo - app-admins {#group-configuration-app-admins}

1. Crie um novo grupo chamado app-admins.
1. Adicione os seguintes grupos ao seu novo grupo de administradores de aplicativos:

   * autores de conteúdo
   * usuários do fluxo de trabalho
   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >os usuários do fluxo de trabalho precisam criar remotamente com o serviço PhoneGap Build

1. Navegue até o console [](http://localhost:4502/useradmin) Permissões e adicione permissões para administrar serviços em nuvem

   * (Ler, Modificar, Criar, Excluir, Replicar) em /etc/cloudservices/mobileservices

1. No mesmo console Permissões, adicione permissões para preparar, publicar e limpar atualizações de conteúdo do aplicativo;

   * (Ler, Modificar, Criar, Excluir, Replicar) em /etc/packages/mobileapp
   * (Lido) em /var/contentsync
   >[!NOTE]
   >
   >A replicação de pacotes é usada para publicar atualizações de aplicativos da instância do autor para publicar a instância

   >[!CAUTION]
   >
   >O acesso a /var/contentsync foi negado como OOTB.
   >
   >A omissão da permissão READ pode resultar na criação e replicação de pacotes de atualização vazios.

1. Adicionar membros a este grupo, conforme necessário
1. Para exportar conteúdo ou fazer upload

   * (Leia) em /etc/contentsync para acessar modelos de exportação
   * (Leitura) em /var para caminho transversal em leituras
   * (Leia, grave, modifique, exclua) em /var/contentsync para gravar, ler e limpar conteúdo de exportação em cache do ContentSync

### Additional Resources {#additional-resources}

Para saber mais sobre as outras duas funções e responsabilidades para criar um aplicativo de serviços sob demanda do AEM Mobile, consulte os seguintes recursos:

* [Desenvolver conteúdo do AEM para serviços sob demanda do AEM Mobile](/help/mobile/aem-mobile-on-demand.md)
* [Criação de conteúdo do AEM para o aplicativo de serviços sob demanda do AEM Mobile](/help/mobile/mobile-apps-ondemand.md)

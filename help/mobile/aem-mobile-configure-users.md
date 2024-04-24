---
title: Configurar usuários e grupos de usuários
description: Siga esta página para entender as funções de usuário e como configurar seus usuários e grupos para oferecer suporte à criação e ao gerenciamento do seu aplicativo de serviços por demanda para dispositivos móveis.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Configurar usuários e grupos de usuários {#configure-your-users-and-user-groups}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Este capítulo descreve as funções de usuário e como configurar usuários e grupos para oferecer suporte à criação e ao gerenciamento de aplicativos móveis.

## Administração de usuários e grupos do aplicativo AEM Mobile {#aem-mobile-application-users-and-group-administration}

### Autores de conteúdo do aplicativo AEM Mobile (grupo de autores do aplicativo) {#aem-mobile-application-content-authors-app-author-group}

Os membros do grupo de autores do aplicativo são responsáveis pela criação de conteúdo de aplicativo móvel AEM, incluindo páginas, texto, imagens e vídeos.

#### Configuração de grupo - autores do aplicativo {#group-configuration-app-authors}

1. Crie um grupo de usuários chamado &quot;autores-aplicativos&quot;:

   Navegue até o Admin Console do usuário: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   No console do grupo de usuários, selecione o botão &quot;+&quot; para criar um grupo.

   Defina a ID desse grupo como &quot;autores-do-aplicativo&quot; para indicar que ele é um tipo específico de grupo de usuários do autor específico para a criação de aplicativos móveis dentro do AEM.

1. Adicionar membro ao grupo: Autores

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Agora que você criou o Grupo de usuários de autores de aplicativos, é possível adicionar membros de equipe individuais a esse novo grupo por meio da [Admin Console do usuário](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. O seguinte permite que você adicione ao grupo de autores de conteúdo AEM:

   (Leitura) em

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### Grupo de administradores de aplicativos AEM Mobile (grupo de administradores de aplicativos) {#aem-mobile-application-administrators-group-app-admins-group}

Os membros do grupo de administradores de aplicativos podem criar conteúdo de aplicativos com as mesmas permissões incluídas nos autores de aplicativos **E** além disso, são também responsáveis por:

* Preparando, publicando e limpando atualizações de OTA do ContentSync do aplicativo

>[!NOTE]
>
>As permissões determinam a disponibilidade de algumas ações do usuário no Centro de comando do aplicativo AEM.
>
>Observe que algumas opções não estão disponíveis para autores de aplicativos que estão disponíveis para administradores de aplicativos.

### Configuração de grupo - app-admins {#group-configuration-app-admins}

1. Crie um grupo chamado administradores de aplicativos.
1. Adicione os seguintes grupos ao novo grupo de administradores de aplicativos:

   * autores de conteúdo
   * workflow-users

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >os usuários do workflow precisam criar remotamente com o serviço de PhoneGap Build

1. Navegue até a [Console de permissões](http://localhost:4502/useradmin) e adicionar permissões para administrar o cloudservices

   * (Ler, modificar, criar, excluir, replicar) em /etc/cloudservices/mobileservices

1. No mesmo console de Permissões, adicione permissões para preparar, publicar e limpar atualizações de conteúdo do aplicativo;

   * (Ler, Modificar, Criar, Excluir, Replicar) em /etc/packages/mobileapp
   * (Leitura) em /var/contentsync

   >[!NOTE]
   >
   >A replicação de pacotes é usada para publicar atualizações de aplicativos da instância de autor para a instância de publicação

   >[!CAUTION]
   >
   >/var/contentsync acesso negado pronto para uso.
   >
   >A omissão da permissão LER pode resultar na criação e replicação de pacotes de atualização vazios.

1. Adicione membros a este grupo conforme necessário
1. Para exportar ou fazer upload de conteúdo

   * (Leitura) em /etc/contentsync para acessar modelos de exportação
   * (Leitura) em /var para passagem de caminho em leituras
   * (Ler, Gravar, Modificar, Excluir) em /var/contentsync para gravar, ler e limpar o conteúdo de exportação em cache do ContentSync

### Recursos adicionais {#additional-resources}

Para entender mais sobre as outras duas funções e responsabilidades para criar um aplicativo AEM Mobile On-demand Services, consulte os seguintes recursos:

* [Desenvolvimento de conteúdo AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Criação de conteúdo AEM para aplicativo AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

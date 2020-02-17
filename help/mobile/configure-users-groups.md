---
title: Configurar usuários e grupos de usuários
seo-title: Configurar usuários e grupos de usuários
description: Siga esta página para entender as funções do usuário e como configurar seus usuários e grupos para suportar a criação e o gerenciamento de seus aplicativos móveis.
seo-description: Siga esta página para entender as funções do usuário e como configurar seus usuários e grupos para suportar a criação e o gerenciamento de seus aplicativos móveis.
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurar usuários e grupos de usuários {#configure-your-users-and-user-groups}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Este capítulo descreve as funções do usuário e como configurar seus usuários e grupos para suportar a criação e o gerenciamento de seus aplicativos móveis.

## Usuários e administração de grupos do aplicativo AEM Mobile {#aem-mobile-application-users-and-group-administration}

Para ajudar a organizar e gerenciar o modelo de permissão para aplicativos AEM, os dois grupos a seguir estão disponíveis:

* app-admins para administradores de aplicativos
* autores de aplicativos para autores de aplicativos

### Autores de conteúdo do aplicativo AEM Mobile (grupo de autores do aplicativo) {#aem-mobile-application-content-authors-app-author-group}

Os membros do grupo de autores do aplicativo são responsáveis pela criação de conteúdo do aplicativo AEM móvel, incluindo páginas, texto, imagens e vídeos.

#### Configuração de grupo - app-autores {#group-configuration-app-authors}

1. Crie um novo grupo de usuários chamado &quot;app-autores&quot;:

   Navegue até o Console de administração do usuário: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   No console do grupo de usuários, selecione o botão &#39;+&#39; para criar um grupo.

   Defina a ID desse grupo como &quot;app-autores&quot; para indicar que é um tipo específico de grupo de usuários do autor específico para a criação de aplicativos móveis no AEM.

1. Adicionar membro ao grupo: Autores

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Adicionar autores de aplicativos ao grupo Autores

1. Agora que você criou o Grupo de usuários de autores de aplicativos, é possível adicionar membros individuais da equipe a esse novo grupo por meio do console [Administrador de](http://localhost:4502/libs/granite/security/content/useradmin.md)usuários.

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Editar grupos de usuários

1. Navegue até o console [](http://localhost:4502/useradmin) Permissões e adicione permissões para administrar serviços em nuvem

   * (Leitura) em /etc/cloudservices
   >[!NOTE]
   >
   >Autores do aplicativo estende o grupo de autores de conteúdo padrão (autores) do AEM, herdando assim a capacidade de criar conteúdo em /content/phonegap

### AEM Mobile Application Administrators Group (grupo de administradores de aplicativos) {#aem-mobile-application-administrators-group-app-admins-group}

Os membros do grupo app-admins podem criar conteúdo do aplicativo com as mesmas permissões incluídas com os autores do aplicativo **E** , além disso, são responsáveis por:

* Configuração dos serviços em nuvem do PhoneGap Build e Adobe Mobile Services no AEM
* Preparar, publicar e apagar atualizações do aplicativo Content Sync OTA

>[!NOTE]
>
>As permissões determinam a disponibilidade de algumas ações do usuário no AEM App Command Center.
>
>Você notará que algumas opções não estão disponíveis para autores de aplicativos que estão disponíveis para administradores de aplicativos.

#### Configuração de grupo - app-admins {#group-configuration-app-admins}

1. Crie um novo grupo chamado app-admins.
1. Adicione os seguintes grupos ao seu novo grupo de administradores de aplicativos:

   * autores de conteúdo
   * usuários do fluxo de trabalho
   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Navegue até o console [](http://localhost:4502/useradmin) Permissões e adicione permissões para administrar serviços em nuvem

   * (Ler, Modificar, Criar, Excluir, Replicar) em /etc/cloudservices/mobileservices
   * (Ler, Modificar, Criar, Excluir, Replicar) em /etc/cloudservices/phonegap-build

1. No mesmo console Permissões, adicione permissões para preparar, publicar e limpar atualizações de conteúdo do aplicativo

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

## Permissões do bloco do painel {#dashboard-tile-permissions}

Os blocos do painel podem expor ações diferentes com base nas permissões que o usuário possui. A seguir, é apresentada uma descrição das ações disponíveis para cada bloco.

Além dessas permissões, uma ação também pode ser exibida/ocultada com base em como o aplicativo atual está configurado. Por exemplo, não há razão para expor a ação &quot;Compilação remota&quot;, se uma configuração de nuvem PhoneGap não tiver sido atribuída ao aplicativo. Eles serão listados abaixo nas seções &quot;Condição **de** configuração&quot;.

### Gerenciar bloco de aplicativos {#manage-app-tile}

No momento, o bloco não tem ações que exijam permissões, no entanto, a página de detalhes do aplicativo tem as seguintes ações:

* *Editar* para app-author e app-admin (Acionador da interface do usuário - jcr:write - em /content/phonegap/{suffix})
* *Baixar* para app-author e app-admin (Acionador da interface do usuário - em /content/phonegap/{suffix})

A imagem abaixo mostra as opções de Download e Edição para um aplicativo:

![chlimage_1-21](assets/chlimage_1-21.png)


---
title: Configurar usuários e grupos de usuários
description: Siga esta página para entender as funções de usuário e como configurar seus usuários e grupos para oferecer suporte à criação e ao gerenciamento de seus aplicativos móveis.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Configurar usuários e grupos de usuários {#configure-your-users-and-user-groups}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Este capítulo descreve as funções de usuário e como configurar usuários e grupos para oferecer suporte à criação e ao gerenciamento de aplicativos móveis.

## Administração de usuários e grupos do aplicativo AEM Mobile {#aem-mobile-application-users-and-group-administration}

Para ajudar a organizar e gerenciar o modelo de permissão para aplicativos AEM, os dois grupos a seguir estão disponíveis:

* app-admins para administradores do aplicativo
* autores de aplicativos para autores de aplicativos

### Autores de conteúdo do aplicativo AEM Mobile (grupo de autores do aplicativo) {#aem-mobile-application-content-authors-app-author-group}

Os membros do grupo de autores do aplicativo são responsáveis pela criação de conteúdo de aplicativo móvel AEM, incluindo páginas, texto, imagens e vídeos.

#### Configuração de grupo - autores do aplicativo {#group-configuration-app-authors}

1. Crie um grupo de usuários chamado &quot;autores-aplicativos&quot;:

   Navegue até o Admin Console do usuário: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   No console do grupo de usuários, selecione o botão &quot;+&quot; para criar um grupo.

   Defina a ID desse grupo como &quot;autores-do-aplicativo&quot; para indicar que ele é um tipo específico de grupo de usuários do autor específico para a criação de aplicativos móveis dentro do AEM.

1. Adicionar membro ao grupo: Autores

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Adicionar autores do aplicativo ao grupo Autores

1. Agora que você criou o Grupo de usuários de autores de aplicativos, é possível adicionar membros de equipe individuais a esse novo grupo por meio da [Admin Console do usuário](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Editar grupos de usuários

1. Navegue até a [Console de permissões](http://localhost:4502/useradmin) e adicionar permissões para administrar o cloudservices

   * (Leitura) em /etc/cloudservices

   >[!NOTE]
   >
   >Os autores do aplicativo estendem o grupo padrão de autores de conteúdo (autores) do AEM, para que eles herdem a capacidade de criar conteúdo em /content/phonegap

### Grupo de administradores de aplicativos AEM Mobile (grupo de administradores de aplicativos) {#aem-mobile-application-administrators-group-app-admins-group}

Os membros do grupo de administradores de aplicativos podem criar conteúdo de aplicativos com as mesmas permissões incluídas nos autores de aplicativos **E** além disso, são também responsáveis por:

* Configuração dos serviços em nuvem do PhoneGap Build e do Adobe Mobile Services no AEM
* Preparando, publicando e limpando atualizações de OTA da sincronização de conteúdo do aplicativo

>[!NOTE]
>
>As permissões determinam a disponibilidade de algumas ações do usuário no Centro de comando do aplicativo AEM.
>
>Observe que algumas opções não estão disponíveis para autores de aplicativos que estão disponíveis para administradores de aplicativos.

#### Configuração de grupo - app-admins {#group-configuration-app-admins}

1. Crie um grupo chamado administradores de aplicativos.
1. Adicione os seguintes grupos ao novo grupo de administradores de aplicativos:

   * autores de conteúdo
   * workflow-users

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Navegue até a [Console de permissões](http://localhost:4502/useradmin) e adicionar permissões para administrar o cloudservices

   * (Ler, modificar, criar, excluir, replicar) em /etc/cloudservices/mobileservices
   * (Ler, Modificar, Criar, Excluir, Replicar) em /etc/cloudservices/phonegap-build

1. No mesmo console de Permissões, adicione permissões para preparar, publicar e limpar atualizações de conteúdo do aplicativo

   * (Ler, Modificar, Criar, Excluir, Replicar) em /etc/packages/mobileapp
   * (Leitura) em /var/contentsync

   >[!NOTE]
   >
   >A replicação de pacotes é usada para publicar atualizações de aplicativos da instância de autor para a instância de publicação

   >[!CAUTION]
   >
   >/var/contentsync acesso negado OOTB.
   >
   >A omissão da permissão LER pode resultar na criação e replicação de pacotes de atualização vazios.

1. Adicione membros a este grupo conforme necessário

## Permissões de bloco do painel {#dashboard-tile-permissions}

Os blocos de painéis podem expor ações diferentes com base nas permissões que o usuário tem. As informações a seguir descrevem quais ações estão disponíveis para cada bloco.

Além dessas permissões, uma ação também pode ser exibida/ocultada com base em como o aplicativo atual é configurado. Por exemplo, não há razão para expor a ação &quot;Compilação remota&quot;, se uma configuração de nuvem do PhoneGap não tiver sido atribuída ao aplicativo. Eles estão listados abaixo em &#39;**Condição de configuração**&#39; seções.

### Gerenciar mosaico do aplicativo {#manage-app-tile}

No momento, o bloco não tem ações que exigem permissões. No entanto, a página de detalhes do aplicativo tem as seguintes ações:

* *Editar* para autor e administrador de aplicativos (Acionador da interface do usuário - jcr:write - on /content/phonegap/{suffix})
* *Baixar* para autor e administrador do aplicativo (Acionador da interface do usuário - ativado /content/phonegap/{suffix})

A imagem abaixo mostra as opções Baixar e Editar de um aplicativo:

![chlimage_1-21](assets/chlimage_1-21.png)

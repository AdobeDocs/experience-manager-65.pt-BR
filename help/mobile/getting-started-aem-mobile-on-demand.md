---
title: AEM Mobile sob demanda
seo-title: AEM Mobile sob demanda
description: Iniciar uma nova experiência de aplicativo AEM Mobile requer uma coesão de funções antes de estar pronto para a edição de conteúdo. Siga esta página para começar a usar AEM serviços sob demanda para dispositivos móveis.
seo-description: Iniciar uma nova experiência de aplicativo AEM Mobile requer uma coesão de funções antes de estar pronto para a edição de conteúdo. Siga esta página para começar a usar AEM serviços sob demanda para dispositivos móveis.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---


# AEM Mobile sob demanda{#aem-mobile-on-demand}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Se você não estiver usando AEM como sua fonte de gerenciamento de conteúdo, consulte [Ajuda da AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM oferece várias ferramentas que permitem a integração do conteúdo em aplicativos móveis.

O diagrama a seguir ilustra como os vários componentes do AEM Mobile e dos serviços sob demanda se encaixam para fornecer conteúdo para aplicativos móveis.

AEM aplicativo Preflight pode ser considerado um ambiente de teste para pré-visualização do aplicativo e do conteúdo antes da publicação; enquanto o aplicativo AEM Mobile é o aplicativo final criado para distribuição.

>[!NOTE]
>
>Para saber mais sobre o aplicativo Preflight, consulte [Usar o aplicativo AEM Preflight](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) na Ajuda do AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>No diagrama acima, a instância de publicação de AEM não é necessária para um cenário de implantação típico da AEM Mobile On-demand Services.

## Iniciar um novo aplicativo móvel {#starting-a-new-mobile-app}

A AEM Mobile é apenas um pilar que constitui a plataforma AEM completa.

Iniciar uma nova experiência de aplicativo AEM Mobile requer uma coesão de funções antes de estar pronto para a edição de conteúdo. As seguintes funções fornecem um ponto de partida para a criação de um novo aplicativo AEM Mobile:

* **Administrador**
* **Desenvolvedor**
* **Autor**

>[!NOTE]
>
>Antes de trabalhar com a AEM Mobile e seguir as etapas neste guia de introdução, os usuários devem estar familiarizados com a AEM. Saiba mais sobre as noções básicas de AEM [here](/help/sites-deploying/deploy.md).

### Noções básicas sobre o Painel de aplicativos AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Antes de entender as funções e responsabilidades, o usuário deve ter conhecimento profundo do **Centro de controle da AEM Mobile** ou do **Painel de aplicativos**. Clique [aqui](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obter uma compreensão aprofundada.

### Administrador do AEM {#aem-administrator}

Um ***AEM administrador*** é responsável por adicionar um novo aplicativo ao catálogo da AEM Mobile, criando um novo aplicativo usando o assistente de criação ou importando um aplicativo existente. AEM administradores que criam um novo aplicativo usando o *assistente de criação* da AEM Mobile, geralmente selecionam um dos modelos de aplicativo desejados em nossos exemplos de referência predefinidos ou (na maioria dos casos) em um modelo de aplicativo personalizado criado por *AEM desenvolvedores.*

Um administrador de AEM é responsável pelas seguintes tarefas ao criar um aplicativo usando o AEM Mobile On-demand Services:

* [Configuração do AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuração dos grupos de usuários e usuários](/help/mobile/aem-mobile-configure-users.md)
* [Visualização com o Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administração de serviços de conteúdo](/help/mobile/developing-content-services.md)

Para começar a usar as funções e responsabilidades de um Administrador, consulte [Administração de conteúdo para usar o AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## Desenvolvedor AEM {#aem-developer}

Um **desenvolvedor AEM** estende e cria modelos e componentes da Web personalizados para permitir que o *Autor do AEM *crie experiências móveis bonitas e envolventes. Esses modelos e componentes não são otimizados apenas para o mundo do aplicativo móvel; mas comunique-se com o dispositivo e com o servidor AEM (qualquer servidor remoto) aos pontos finais de serviço do canal onni. AEM editor de conteúdo integrado é usado por *Autores do AEM* para criar experiências avançadas e relevantes no aplicativo, incluindo integração com o restante do Adobe Marketing Cloud.

Um desenvolvedor AEM é responsável pelas seguintes tarefas ao criar um aplicativo usando o AEM Mobile On-demand Services:

* [Modelos e componentes do aplicativo](/help/mobile/app-templates-and-components1.md)
* [Mobile com sincronização de conteúdo](/help/mobile/mobile-ondemand-contentsync.md)
* [Propriedades de conteúdo e exportação de conteúdo](/help/mobile/on-demand-content-properties-exporting.md)
* [Desenvolvimento dos serviços de conteúdo da AEM Mobile](//help/mobile/developing-content-services.md)

Para começar a usar as funções e responsabilidades do desenvolvedor, consulte [Desenvolvimento de conteúdo AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Uma função *AEM desenvolvedor* não start e termina com o desenvolvimento de modelos e componentes. Um *desenvolvedor AEM* pode criar um aplicativo totalmente novo em vez de simplesmente estender a amostra de implementação de referência pronta para uso.

## AEM Author {#aem-author}

Um ***Autor do AEM* (ou *Marketer*)**usa os modelos e componentes personalizados desenvolvidos ou prontos para uso para adicionar e editar páginas, arrastar e soltar componentes e adicionar mídia de todos os tipos do DAM, incluindo imagens, vídeos e fragmentos de texto (fragmentos de conteúdo). AEM editor de conteúdo incorporado é usado por *Autores do AEM* para criar experiências avançadas e relevantes no aplicativo, incluindo integração com o restante do Adobe Marketing Cloud.

Um autor de AEM deve entender os seguintes tópicos ao criar um aplicativo usando o AEM Mobile On-demand Services:

* [painel de aplicativos AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Ações de criação e configuração do aplicativo](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuração na nuvem](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gerenciamento de conteúdo](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Visão geral dos serviços de conteúdo](/help/mobile/develop-content-as-a-service.md)

Para começar a usar as funções e responsabilidades de um Autor, consulte [Criação AEM conteúdo para o aplicativo AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Um autor de AEM também é responsável por configurar direitos, criar cartões e layouts e enviar notificações por push. Além disso, para obter mais informações sobre métodos de criação de conteúdo; Gestão de artigos e coleções; criar banners, cartões e layouts no AEM Mobile, consulte [Portal sob demanda do AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).


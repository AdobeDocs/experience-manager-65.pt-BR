---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: Iniciar uma nova experiência de aplicativo do AEM Mobile requer uma coesão de funções antes de estar pronto para a edição de conteúdo. Siga esta página para começar a usar os serviços sob demanda do AEM Mobile.
seo-description: Iniciar uma nova experiência de aplicativo do AEM Mobile requer uma coesão de funções antes de estar pronto para a edição de conteúdo. Siga esta página para começar a usar os serviços sob demanda do AEM Mobile.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Se você não estiver usando o AEM como sua fonte de gerenciamento de conteúdo, consulte a Ajuda [do](https://helpx.adobe.com/digital-publishing-solution/topics.html)AEM Mobile On-Demand Services.

O AEM fornece várias ferramentas que permitem a integração do conteúdo em aplicativos móveis.

O diagrama a seguir ilustra como os vários componentes do AEM Mobile e dos serviços sob demanda se encaixam para fornecer conteúdo para aplicativos móveis.

O aplicativo AEM Preflight pode ser considerado um ambiente de teste para visualizar o aplicativo e o conteúdo antes da publicação; Considerando que o aplicativo AEM Mobile é o aplicativo final criado para distribuição.

>[!NOTE]
>
>Para saber mais sobre o aplicativo Preflight, consulte [Usar o aplicativo](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) AEM Preflight na Ajuda dos serviços sob demanda do AEM Mobile.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>No diagrama acima, a instância de publicação de AEM não é necessária para um cenário de implantação típico dos serviços sob demanda do AEM Mobile.

## Iniciar um novo aplicativo móvel {#starting-a-new-mobile-app}

O AEM Mobile é apenas um pilar que constitui a plataforma completa do AEM.

Iniciar uma nova experiência de aplicativo do AEM Mobile requer uma coesão de funções antes de estar pronto para a edição de conteúdo. As seguintes funções fornecem um ponto de partida para a criação de um novo aplicativo AEM Mobile:

* **Administrador**
* **Desenvolvedor**
* **Autor**

>[!NOTE]
>
>Antes de trabalhar com o AEM Mobile e seguir as etapas neste guia de introdução, os usuários devem se familiarizar com o AEM. Learn the basics of AEM [here](/help/sites-deploying/deploy.md).

### Como entender o painel de aplicativos do AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Antes de entender as funções e responsabilidades, o usuário deve ter um conhecimento profundo do Centro **de controle do** AEM Mobile ou do Painel **de** aplicativos. Clique [aqui](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obter uma compreensão profunda.

### Administrador do AEM {#aem-administrator}

Um administrador ***do*** AEM é responsável por adicionar um novo aplicativo ao catálogo do AEM Mobile, criando um novo aplicativo usando o assistente de criação ou importando um aplicativo existente. Os administradores de AEM que criam um novo aplicativo usando o assistente *de* criação do AEM Mobile geralmente selecionam um dos modelos de aplicativo desejados em nossos exemplos de referência prontos ou (na maioria dos casos) em um modelo de aplicativo personalizado criado pelos desenvolvedores do *AEM.*

Um administrador do AEM é responsável pelas seguintes tarefas ao criar um aplicativo usando os serviços sob demanda do AEM Mobile:

* [Configuração do AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuração dos grupos de usuários e usuários](/help/mobile/aem-mobile-configure-users.md)
* [Visualização com o Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administração de serviços de conteúdo](/help/mobile/developing-content-services.md)

Para começar a usar as funções e responsabilidades de um administrador, consulte [Administração de conteúdo para usar os serviços](/help/mobile/aem-mobile.md)sob demanda do AEM Mobile.

## Desenvolvedor do AEM {#aem-developer}

Um desenvolvedor **do** AEM estende e cria modelos e componentes personalizados da Web para permitir que o *Autor do AEM *crie experiências móveis bonitas e envolventes. Esses modelos e componentes não são otimizados apenas para o mundo do aplicativo móvel; mas comunique-se com o dispositivo e com o servidor AEM (qualquer servidor remoto) aos pontos finais de serviço de canal oniano. O editor de conteúdo integrado do AEM é usado pelos autores *do* AEM para criar experiências avançadas e relevantes no aplicativo, incluindo a integração com o restante da Adobe Marketing Cloud.

Um desenvolvedor do AEM é responsável pelas seguintes tarefas ao criar um aplicativo usando os serviços sob demanda do AEM Mobile:

* [Modelos e componentes do aplicativo](/help/mobile/app-templates-and-components1.md)
* [Mobile com sincronização de conteúdo](/help/mobile/mobile-ondemand-contentsync.md)
* [Propriedades de conteúdo e exportação de conteúdo](/help/mobile/on-demand-content-properties-exporting.md)
* [Desenvolvimento de serviços de conteúdo do AEM Mobile](//help/mobile/developing-content-services.md)

Para começar a usar as funções e responsabilidades do desenvolvedor, consulte [Desenvolvimento de conteúdo do AEM para serviços](/help/mobile/aem-mobile-on-demand.md)sob demanda do AEM Mobile.

>[!NOTE]
>
>A função de desenvolvedor do *AEM* não começa nem termina com o desenvolvimento de modelos e componentes. Um desenvolvedor *do* AEM pode criar um aplicativo totalmente novo em vez de simplesmente estender a amostra de implementação de referência pronta para uso.

## AEM Author {#aem-author}

Um autor ***do *AEM (ou*profissional de marketing *)**usa os modelos e componentes personalizados desenvolvidos ou prontos para uso para adicionar e editar páginas, arrastar e soltar componentes e adicionar mídia de todos os tipos do DAM, incluindo imagens, vídeos e fragmentos de texto (fragmentos de conteúdo). O editor de conteúdo integrado do AEM é usado pelos autores*do *AEM para criar experiências avançadas e relevantes no aplicativo, incluindo a integração com o restante da Adobe Marketing Cloud.

Um autor do AEM deve entender os seguintes tópicos, ao criar um aplicativo usando os serviços sob demanda do AEM Mobile:

* [Painel do aplicativo AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Ações de criação e configuração do aplicativo](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuração na nuvem](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gerenciamento de conteúdo](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Visão geral dos serviços de conteúdo](/help/mobile/develop-content-as-a-service.md)

Para começar a usar as funções e responsabilidades de um autor, consulte [Criação de conteúdo AEM para o aplicativo](/help/mobile/mobile-apps-ondemand.md)AEM Mobile On-Demand Services.

>[!NOTE]
>
>Um autor de AEM também é responsável por configurar direitos, criar cartões e layouts e enviar notificações por push. Além disso, para obter mais informações sobre métodos de criação de conteúdo; Gestão de artigos e coleções; criar banners, cartões e layouts no AEM Mobile, consulte Portal [sob demanda do](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2)AEM Mobile.


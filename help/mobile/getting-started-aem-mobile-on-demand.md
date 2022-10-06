---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: Iniciar uma nova experiência com o aplicativo AEM Mobile requer uma coesão de funções antes de estar pronto para a edição de conteúdo. Siga esta página para começar a usar AEM serviços sob demanda para dispositivos móveis.
seo-description: Starting a new AEM Mobile app experience requires a cohesion of roles before it is ready for content editing. Follow this page to get started with AEM mobile On-Demand services.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Se você não estiver usando o AEM como fonte de gerenciamento de conteúdo, consulte [Ajuda do AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

O AEM fornece várias ferramentas que permitem integrar seu conteúdo a aplicativos móveis.

O diagrama a seguir ilustra como os vários componentes do AEM Mobile e dos serviços sob demanda se encaixam para fornecer conteúdo aos aplicativos móveis.

AEM o aplicativo Preflight pode ser considerado um ambiente de teste para visualizar o aplicativo e o conteúdo antes da publicação; enquanto o aplicativo AEM Mobile é o aplicativo final criado para distribuição.

>[!NOTE]
>
>Para saber mais sobre o aplicativo Preflight, consulte [Usar o aplicativo AEM Preflight](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) na Ajuda do AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>No diagrama acima, a instância de publicação do AEM não é necessária para um cenário de implantação típico do AEM Mobile On-demand Services.

## Iniciar um novo aplicativo móvel {#starting-a-new-mobile-app}

O AEM Mobile é apenas um pilar que constitui a plataforma AEM completa.

Iniciar uma nova experiência com o aplicativo AEM Mobile requer uma coesão de funções antes de estar pronto para a edição de conteúdo. As seguintes funções fornecem um ponto de partida para a criação de um novo aplicativo do AEM Mobile:

* **Administrador**
* **Desenvolvedor**
* **Autor**

>[!NOTE]
>
>Antes de trabalhar com o AEM Mobile e seguir as etapas deste guia de introdução, os usuários devem se familiarizar com o AEM. Saiba mais sobre as noções básicas do AEM [here](/help/sites-deploying/deploy.md).

### Como entender o painel de aplicativos do AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Antes de entender as funções e responsabilidades, o usuário deve ter conhecimento profundo de **AEM Mobile Control Center** ou **Painel de aplicativos**. Clique em [here](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obter uma compreensão profunda.

### Administrador do AEM {#aem-administrator}

Um ***Administrador de AEM*** O é responsável por adicionar um novo aplicativo ao catálogo do AEM Mobile, criando um novo aplicativo usando o assistente de criação ou importando um aplicativo existente. Administradores de AEM que criam um novo aplicativo usando o AEM Mobile *assistente de criação* normalmente, selecione um dos modelos de aplicativo desejados a partir de nossos exemplos de referência prontos para uso ou (na maioria dos casos) um modelo de aplicativo personalizado criado por *AEM desenvolvedores.*

Um administrador de AEM é responsável pelas seguintes tarefas ao criar um aplicativo usando o AEM Mobile On-demand Services:

* [Configuração do AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configurar seus usuários e grupos de usuários](/help/mobile/aem-mobile-configure-users.md)
* [Visualização com comprovação](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administração dos serviços de conteúdo](/help/mobile/developing-content-services.md)

Para começar a usar funções e responsabilidades de um Administrador, consulte [Administração de conteúdo para usar o AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## Desenvolvedor de AEM {#aem-developer}

Um **Desenvolvedor de AEM** O estende e cria modelos e componentes da Web personalizados para permitir que o *Autor do AEM *crie experiências móveis bonitas e envolventes. Esses modelos e componentes não são otimizados apenas para o mundo do aplicativo móvel; mas comunique-se com o dispositivo e com o servidor AEM (qualquer servidor remoto) aos pontos finais do serviço omnicanal. AEM editor de conteúdo integrado é usado por *Autores do AEM* para criar experiências avançadas e relevantes no aplicativo, incluindo integração com o resto da Adobe Marketing Cloud.

Um desenvolvedor de AEM é responsável pelas seguintes tarefas ao criar um aplicativo usando o AEM Mobile On-demand Services:

* [Modelos e componentes do aplicativo](/help/mobile/app-templates-and-components1.md)
* [Móvel com sincronização de conteúdo](/help/mobile/mobile-ondemand-contentsync.md)
* [Propriedades de conteúdo e exportação de conteúdo](/help/mobile/on-demand-content-properties-exporting.md)
* [Desenvolvimento dos serviços de conteúdo da AEM Mobile](/help/mobile/developing-content-services.md)

Para começar a usar as funções e responsabilidades do desenvolvedor, consulte [Desenvolvimento de conteúdo AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Um *do desenvolvedor de AEM* não inicia e termina com o desenvolvimento de modelos e componentes. Um *Desenvolvedor de AEM* O pode criar um aplicativo totalmente novo em vez de simplesmente estender a amostra de implementação de referência predefinida.

## Autor do AEM {#aem-author}

Um ***Autor do AEM* ou *Profissional de marketing*)**O usa os modelos e componentes desenvolvidos ou prontos para uso personalizados para adicionar e editar páginas, arrastar e soltar componentes e adicionar mídia de todos os tipos do DAM, incluindo imagens, vídeos e fragmentos de texto (fragmentos de conteúdo). AEM editor de conteúdo integrado é usado por *Autores do AEM* para criar experiências avançadas e relevantes no aplicativo, incluindo integração com o resto da Adobe Marketing Cloud.

Um autor de AEM deve entender os seguintes tópicos, ao criar um aplicativo usando o AEM Mobile On-demand Services:

* [Painel de aplicativos do AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Ações de criação e configuração do aplicativo](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuração na nuvem](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gerenciamento de conteúdo](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Visão geral dos serviços de conteúdo](/help/mobile/develop-content-as-a-service.md)

Para começar a usar as funções e responsabilidades de um autor, consulte [Criação de conteúdo AEM para aplicativo AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Um autor do AEM também é responsável por configurar o direito, criar cartões e layouts e enviar notificações por push. Além disso, para obter mais informações sobre métodos de criação de conteúdo; Gestão de artigos e coleções; criar banners, cartões e layouts no AEM Mobile, consulte [Portal sob demanda do AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).

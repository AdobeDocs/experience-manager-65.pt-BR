---
title: Ações de criação e configuração do aplicativo
seo-title: Application Create and Configuration Actions
description: A criação de um aplicativo é frequentemente o primeiro passo para a criação e o gerenciamento de conteúdo sob demanda do AEM Mobile. Siga esta página para saber mais.
seo-description: Creating an app is often the first step towards creating and managing AEM Mobile On-Demand content. Follow this page to learn more.
uuid: f6b41d9a-d896-479e-9f6c-e91a88f3e74d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: ccafd49a-5c8a-44eb-9b0c-37070560bb52
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# Ações de criação e configuração do aplicativo{#application-create-and-configuration-actions}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

## Criação de um aplicativo sob demanda {#creating-an-on-demand-application}

A criação de um aplicativo é frequentemente a primeira etapa para criar e gerenciar conteúdo sob demanda da AEM Mobile, além de ser executada no nível de Administrador do AEM. Ele representa um shell de conteúdo, visualizável em dispositivos móveis, pronto para exibir o conteúdo criado do autor, como artigos, imagens, coleções, etc.

Os detalhes do seu aplicativo podem ser visualizados no Painel ou no Centro de controle do AEM Mobile.

>[!NOTE]
>
>O Painel é uma série de blocos úteis que fornecem uma visão geral do conteúdo do aplicativo, dos metadados e do status da conexão AEM Mobile On-Demand.
>
>Consulte [Painel de aplicativos do AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obter detalhes.

**Para criar um aplicativo sob demanda:**

1. Selecionar **Celular** no painel lateral.
1. Selecionar **Aplicativos** da Navegação.
1. Clique em **Criar** e selecione **Aplicativo** no menu suspenso .
1. Escolha o modelo de aplicativo móvel e clique em **Próximo**.
1. Insira as propriedades do aplicativo, como **Título**, **Nome**, **Descrição**.
1. Clique em **Avançar**.
1. Se for conhecido, insira os detalhes de configuração da nuvem; caso contrário, clique em **Criar**.
1. Clique em **Concluído** para exibir seu novo aplicativo AEM Mobile no catálogo.

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>Esse processo permite criar uma instância do aplicativo no AEM.

## Usar modelos de aplicativo {#using-app-templates}

Os modelos de aplicativos fornecem uma maneira fácil de aproveitar os designs existentes criados pelos desenvolvedores, usados para criar novos aplicativos no AEM.

O que é um modelo de aplicativo? Pense nisso como uma coleção de modelos de página e componentes que representam uma linha de base ou uma base de um aplicativo.
Ao criar um novo aplicativo com base no modelo de outro aplicativo, você obtém um aplicativo que tem um representante de ponto de partida do aplicativo no qual ele foi criado.

Você deve ter um modelo de aplicativo móvel existente (ou um aplicativo instalado que tenha um modelo de aplicativo) para usar esse recurso.

### A próxima etapa {#the-next-step}

Depois de criar um aplicativo sob demanda no painel do aplicativo, a próxima etapa é associar seu aplicativo à configuração da nuvem.

Consulte [Associar seu aplicativo à configuração da nuvem](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) para obter mais detalhes.

### Avançar {#getting-ahead}

Depois de se familiarizar com a criação de um aplicativo sob demanda e, portanto, associar esse aplicativo a uma configuração de nuvem, consulte [Ações de gerenciamento de conteúdo](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

**Ações de gerenciamento de conteúdo** envolve a criação e o gerenciamento do seguinte conteúdo:

* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gerenciamento de banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gerenciando Coleções](/help/mobile/mobile-on-demand-managing-collections.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar Cancelar publicação de conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento de conteúdo AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Administração de conteúdo para usar o AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)

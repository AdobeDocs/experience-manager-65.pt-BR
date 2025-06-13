---
title: Extensão [!DNL Adobe Experience Manager] 6.5 usando o Adobe Developer App Builder.
description: Extensão [!DNL Adobe Experience Manager] 6.5 usando o Adobe Developer App Builder.
exl-id: 8221c2db-82d4-43df-ad38-e8e7831541ac
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Extensão do [!DNL Adobe Experience Manager] usando o Adobe Developer App Builder {#extend-using-app-builder}

## O que é o App Builder para AEM {#project-appbuilder}

O novo Adobe Developer App Builder fornece uma estrutura de extensibilidade para que um desenvolvedor estenda facilmente as funcionalidades do AEM.

O App Builder fornece uma estrutura unificada de extensibilidade de terceiros para integrar e criar experiências personalizadas que estendem o Adobe Experience Manager. Com essa estrutura completa de extensibilidade, criada na infraestrutura da Adobe, os desenvolvedores podem criar microsserviços personalizados, estender e integrar o Adobe Experience Manager às soluções da Adobe e ao restante da pilha de TI.

O App Builder fornece uma maneira de os clientes estenderem facilmente o Adobe Experience Manager em vários casos de uso:

* Extensibilidade de middleware - Conecte sistemas externos com aplicativos Adobe criando conectores personalizados ou use um conjunto de integrações pré-construídas.
* Extensibilidade dos principais serviços - Amplie os principais recursos do aplicativo estendendo o comportamento padrão com recursos personalizados e lógica de negócios.
* Extensibilidade de experiência do usuário - Amplie a experiência principal para atender aos requisitos comerciais ou criar propriedades digitais específicas do cliente, vitrines e aplicativos de back-office.

>[!NOTE]
>
>Para clientes do AEM as a Cloud Service que desejam usar o App Builder, consulte [Extensão do Adobe Experience Manager as a Cloud Service usando o Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html?lang=pt-BR).

## Arquitetura {#architecture}

Em vez de uma solução pronta para uso, a Adobe Developer App Builder fornece uma plataforma de desenvolvimento comum, consistente e padronizada para estender as soluções da Adobe Cloud, como o AEM, incluindo:

* Adobe Developer Console — Para microsserviços personalizados e desenvolvimento de extensões, permite que os desenvolvedores criem e gerenciem projetos enquanto acessam todas as ferramentas e APIs necessárias para criar plug-ins e integrações.
* Ferramentas do desenvolvedor — Ferramentas de código aberto, SDKs e bibliotecas para permitir que os desenvolvedores criem facilmente extensões e integrações personalizadas. Use o React Spectrum (kit de ferramentas da interface do Adobe) para ter uma interface comum para todos os aplicativos da Adobe.
* Serviços — I/O Runtime para hospedar a infraestrutura na plataforma sem servidor da Adobe e I/O Events para integrações baseadas em eventos. A Adobe também oferece suporte pronto para armazenar dados e arquivos.
* Adobe Experience Cloud — os desenvolvedores podem enviar extensões e integrações para publicação em sua organização da Experience Cloud. Em seguida, os administradores do sistema podem revisar, gerenciar e aprovar essas extensões. Depois de publicadas, suas ferramentas e extensões personalizadas do App Builder podem ser encontradas junto com outros aplicativos da Adobe Experience Cloud.

O diagrama a seguir ilustra como um aplicativo padrão criado no App Builder usa essas funcionalidades:

![Arquitetura](assets/appbuilder-architecture.jpg)

Para obter mais detalhes sobre a arquitetura do App Builder, consulte [Visão geral da arquitetura](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/architecture_overview/architecture-overview).

## Introdução ao App Builder {#additional-resources}

Para ajudar você a começar a usar o App Builder, uma série de documentações foi criada para ajudar você a começar:

* [Introdução ao App Builder](https://developer.adobe.com/app-builder/docs/get_started/)

## Continue aprendendo com a documentação {#appbuilder-documentation}

O App Builder fornece vídeos e documentação para desenvolvedores, incluindo guias e documentação de referência para ajudar você a começar a desenvolver seus próprios aplicativos personalizados:

* [Documentação do App Builder](https://developer.adobe.com/app-builder/docs/overview/)
* [Vídeos do App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Experimente um dos aplicativos de amostra {#appbuilder-codesamples}

Pronto para começar a desenvolver? Há vários aplicativos de exemplo para ajudá-lo a começar rapidamente:

* [App Builder Code Labs no site da Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/)


---
title: Extensão do  [!DNL Adobe Experience Manager] 6.5 usando o Adobe Developer App Builder.
description: Extensão do  [!DNL Adobe Experience Manager] 6.5 usando o Adobe Developer App Builder.
source-git-commit: aab7d4aaf11b6aef3b729f906259a76c152fd6f0
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Extensão [!DNL Adobe Experience Manager] usando o Adobe Developer App Builder {#extend-using-app-builder}

## O que é o App Builder para AEM {#project-firefly}

O novo Adobe Developer App Builder oferece uma estrutura de extensibilidade para um desenvolvedor estender facilmente AEM funcionalidades.

O App Builder fornece uma estrutura unificada de extensibilidade de terceiros para integrar e criar experiências personalizadas que estendem o Adobe Experience Manager. Com essa estrutura completa de extensibilidade, integrada à infraestrutura Adobe, os desenvolvedores podem criar microsserviços personalizados, estender e integrar a Adobe Experience Manager em soluções de Adobe e no restante da pilha de TI.

O App Builder fornece aos clientes uma maneira de estender facilmente o Adobe Experience Manager em vários casos de uso:

* Extensibilidade Middleware - Conecte sistemas externos com aplicativos Adobe criando conectores personalizados ou aproveite um conjunto de integrações pré-criadas.
* Extensibilidade de serviços principais - Estenda os principais recursos do aplicativo ao estender o comportamento padrão com recursos personalizados e lógica comercial.
* Extensibilidade da experiência do usuário - Estenda a experiência principal para atender aos requisitos dos negócios ou crie propriedades digitais, vitrines e aplicativos de back-office específicos do cliente.

O App Builder (anteriormente conhecido como Project Firefly) está disponível para clientes corporativos e parceiros por meio da nossa Visualização do desenvolvedor desde o verão de 2020. A disponibilidade geral (GA) do App Builder está agendada para dezembro de 2021. Saudamos os desenvolvedores a experimentar o App Builder por meio do [Trial Program](http://adobe.ly/appbuilder-trial).

>[!NOTE]
>
> Para AEM como clientes do Cloud Service que desejam aproveitar o App Builder, acesse [Extensão do Adobe Experience Manager as a Cloud Service usando o Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/configuring-and-extending/app-builder.html).

## Arquitetura {#architecture}

Em vez de uma solução pronta para uso, o Adobe Developer App Builder oferece uma plataforma de desenvolvimento comum, consistente e padronizada para estender as soluções da Adobe Cloud, como AEM, incluindo:

* Console do desenvolvedor do Adobe — para microsserviços e desenvolvimento de extensões personalizados, permitindo que os desenvolvedores criem e gerenciem projetos ao acessar todas as ferramentas e APIs necessárias para criar plug-ins e integrações.
* Ferramentas do desenvolvedor — Ferramentas de código aberto, SDKs e bibliotecas para permitir que os desenvolvedores criem facilmente extensões e integrações personalizadas. Use o React Spectrum (kit de ferramentas da interface do usuário do Adobe) para ter uma interface comum para todos os aplicativos do Adobe.
* Serviços — I/O Runtime para hospedar a infraestrutura em nossa plataforma sem servidor e Eventos de E/S para integrações baseadas em eventos. Também fornecemos suporte pronto para uso para armazenar dados e arquivos.
* Adobe Experience Cloud — Os desenvolvedores podem enviar extensões e integrações para serem publicadas em sua Experience Cloud Org. Os administradores do sistema podem então revisar, gerenciar e aprovar essas extensões. Depois de publicadas, suas ferramentas e extensões personalizadas do App Builder podem ser encontradas junto com outros aplicativos do Adobe Experience Cloud.

O diagrama a seguir ilustra como um aplicativo padrão criado no App Builder aproveita essas funcionalidades:

![Arquitetura](assets/firefly-architecture.jpg)

Para obter mais detalhes sobre a arquitetura do App Builder, consulte [Visão geral da arquitetura](https://www.adobe.io/project-firefly/docs/guides/).

## Introdução ao App Builder {#additional-resources}

Para ajudar você a começar a usar o App Builder, criamos uma série de documentação para ajudá-lo a começar:

* [Introdução ao App Builder](https://www.adobe.io/project-firefly/docs/getting_started/)

## Continuar o aprendizado com a documentação {#appbuilder-documentation}

O App Builder fornece vídeos e documentação para desenvolvedores, incluindo guias e documentação de referência para ajudar você a começar a desenvolver seus próprios aplicativos personalizados:

* [Documentação do App Builder](https://www.adobe.io/project-firefly/docs/overview/)
* [Vídeos do App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Experimente um dos aplicativos de exemplo {#appbuilder-codesamples}

Pronto para começar a desenvolver? Temos muitos aplicativos de exemplo para ajudá-lo a entrar em contato rapidamente:

* [Laboratórios de código do App Builder no site do desenvolvedor do Adobe](https://www.adobe.io/project-firefly/docs/resources/)

## Suporte {#support}

Para o tipo de suporte ao desenvolvedor, incentivamos os desenvolvedores a usar nosso [Experience League forum](https://experienceleaguecommunities.adobe.com/t5/project-firefly/ct-p/project-firefly).

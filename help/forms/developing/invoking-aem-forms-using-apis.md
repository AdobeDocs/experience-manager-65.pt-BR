---
title: Invocar o AEM Forms usando APIs
seo-title: Invocar o AEM Forms usando APIs
description: Invocar o AEM Forms usando APIs
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Invocar o AEM Forms usando APIs {#invoking-aem-forms-using-apis}

A Adobe Experience Manager Forms é um software corporativo baseado no J2EE que consiste em serviços que operam dentro de uma infraestrutura compartilhada. Geralmente, as operações de serviço consomem ou produzem documentos. Usando o AEM Forms, é possível combinar o fluxo de trabalho de formulários com formulários eletrônicos, segurança do documento e geração de documentos em um conjunto integrado e coeso de serviços. Esses serviços podem ser acessados dentro e fora do firewall.

Os aplicativos clientes podem chamar programaticamente os serviços da AEM Forms usando uma API Java, serviços da Web, Remoting e REST. Usando o console de administração, você pode configurar um serviço para expor um terminal que permite que os serviços da AEM Forms sejam chamados de forma programática. Por padrão, a maioria dos serviços é pré-configurada para expor pontos de extremidade Remoting, Java e serviços da Web.

Seus requisitos de negócios determinam qual método de invocação usar. Por exemplo, usando a API Java, é possível integrar a funcionalidade AEM Forms aos aplicativos corporativos Java, como Java Entity e Message beans. Da mesma forma, você pode integrar a funcionalidade do AEM Forms em projetos do .NET (ou outros projetos desenvolvidos com ambientes de desenvolvimento que suportam padrões de serviço da Web) usando serviços da Web.

Os serviços exigem a execução de um container de serviço, de modo semelhante ao modo como os EJBs (Enterprise JavaBeans™) exigem um container J2EE. A AEM Forms inclui apenas uma implementação de um container de serviço. O container de serviço é responsável por gerenciar a duração de um serviço, incluindo sua implantação e garantindo que todas as solicitações sejam enviadas ao serviço correto. Ele também gerencia documentos que um serviço consome ou produz.

>[!NOTE]
>
>A programação com formulários AEM não inclui informações sobre como chamar o AEM Forms usando pastas monitoradas ou email.


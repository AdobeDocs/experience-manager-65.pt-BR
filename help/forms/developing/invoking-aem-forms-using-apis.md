---
title: Invocar formulários AEM usando APIs
seo-title: Invocar formulários AEM usando APIs
description: 'null'
seo-description: 'null'
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Invocar formulários AEM usando APIs {#invoking-aem-forms-using-apis}

O Adobe Experience Manager Forms é um software corporativo baseado em J2EE que consiste em serviços que operam em uma infraestrutura compartilhada. As operações de serviço normalmente consomem ou produzem documentos. Usando o AEM Forms, é possível combinar o fluxo de trabalho de formulários com formulários eletrônicos, segurança de documentos e geração de documentos em um conjunto integrado e coeso de serviços. Esses serviços podem ser acessados dentro e fora do firewall.

Aplicativos cliente podem chamar programaticamente os serviços do AEM Forms usando uma API Java, serviços da Web, Remoting e REST. Usando o console de administração, você pode configurar um serviço para expor um terminal que permite que os serviços do AEM Forms sejam chamados de forma programática. Por padrão, a maioria dos serviços é pré-configurada para expor pontos de extremidade Remoting, Java e serviços da Web.

Seus requisitos de negócios determinam qual método de invocação usar. Por exemplo, usando a API Java, é possível integrar a funcionalidade do AEM Forms aos aplicativos corporativos Java, como Java Entity e Message beans. Da mesma forma, é possível integrar a funcionalidade do AEM Forms em projetos .NET (ou outros projetos desenvolvidos com ambientes de desenvolvimento que suportam padrões de serviço da Web) usando serviços da Web.

Os serviços exigem a execução de um contêiner de serviço, de modo semelhante ao modo como os EJBs (Enterprise JavaBeans™) exigem um contêiner J2EE. O AEM Forms inclui apenas uma implementação de um contêiner de serviço. O contêiner de serviço é responsável por gerenciar a duração de um serviço, incluindo a implantação e a garantia de que todas as solicitações sejam enviadas ao serviço correto. Ele também gerencia documentos que um serviço consome ou produz.

>[!NOTE]
>
>A programação com formulários do AEM não inclui informações sobre como chamar formulários do AEM usando pastas monitoradas ou email.


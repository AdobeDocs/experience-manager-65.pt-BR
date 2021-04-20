---
title: Chamar o AEM Forms usando APIs
seo-title: Chamar o AEM Forms usando APIs
description: Chamar o AEM Forms usando APIs
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# Chamar o AEM Forms usando APIs {#invoking-aem-forms-using-apis}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O Adobe Experience Manager Forms é um software corporativo baseado em J2EE que consiste em serviços que operam dentro de uma infraestrutura compartilhada. As operações de serviço normalmente consomem ou produzem documentos. Ao usar o AEM Forms, é possível combinar o fluxo de trabalho de formulários com formulários eletrônicos, segurança de documentos e geração de documentos em um conjunto de serviços integrado e coeso. Esses serviços podem ser acessados dentro e fora do firewall.

Aplicativos clientes podem invocar programaticamente os serviços da AEM Forms usando uma API Java, serviços da Web, Remota e REST. Usando o console de administração, é possível configurar um serviço para expor um terminal que permite aos serviços da AEM Forms por chamada programática. Por padrão, a maioria dos serviços é pré-configurada para expor pontos de extremidade de Remota, Java e serviço da Web.

Seus requisitos comerciais determinam qual método de invocação usar. Por exemplo, usando a API Java, é possível integrar a funcionalidade AEM Forms em seus aplicativos empresariais Java, como Java Entity e Message beans. Da mesma forma, é possível integrar a funcionalidade do AEM Forms em projetos do .NET (ou outros projetos desenvolvidos com ambientes de desenvolvimento que suportam padrões de serviço da Web) usando serviços da Web.

Os serviços exigem que um contêiner de serviço seja executado, de modo semelhante a como o Enterprise JavaBeans™ (EJBs) requer um contêiner J2EE. O AEM Forms inclui apenas uma implementação de um contêiner de serviço. O contêiner de serviço é responsável pelo gerenciamento da duração de um serviço, incluindo sua implantação e garantia de que todas as solicitações sejam enviadas para o serviço correto. Ele também gerencia documentos que um serviço consome ou produz.

>[!NOTE]
>
>A programação com formulários AEM não inclui informações sobre como invocar o AEM Forms usando pastas vigiadas ou email.


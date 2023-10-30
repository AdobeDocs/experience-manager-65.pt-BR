---
title: Como chamar o AEM Forms usando APIs?
description: Chame serviços da AEM Forms usando uma API Java, serviços da Web, comunicação remota e REST.
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
role: Developer
exl-id: 0e92d1ad-12bd-4bfd-81cc-9be8e376c5ca
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Chamada do AEM Forms usando APIs {#invoking-aem-forms-using-apis}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

O Adobe Experience Manager Forms é um software corporativo baseado em J2EE que consiste em serviços que operam em uma infraestrutura compartilhada. As operações de serviço normalmente consomem ou produzem documentos. Ao usar o AEM Forms, você pode combinar o fluxo de trabalho de formulários com formulários eletrônicos, segurança de documentos e geração de documentos em um conjunto integrado e coeso de serviços. Esses serviços podem ser acessados de dentro e de fora do firewall.

Os aplicativos clientes podem chamar serviços da AEM Forms programaticamente usando uma API Java, serviços da Web, comunicação remota e REST. Usando o console de administração, você pode configurar um serviço para expor um endpoint que permite que os serviços do AEM Forms sejam chamados programaticamente. Por padrão, a maioria dos serviços é pré-configurada para expor pontos de extremidade de serviços da Web, Java e Comunicação remota.

Seus requisitos comerciais determinam qual método de invocação usar. Por exemplo, usando a API Java, você pode integrar a funcionalidade AEM Forms em seus aplicativos corporativos Java, como Entidade Java e Beans de mensagem. Da mesma forma, você pode integrar a funcionalidade do AEM Forms em projetos .NET (ou outros projetos desenvolvidos com ambientes de desenvolvimento que oferecem suporte aos padrões de serviço da Web) usando serviços da Web.

Os serviços exigem um contêiner de serviço para ser executado, de modo semelhante a como o Enterprise JavaBeans™ (EJBs) requer um contêiner J2EE. O AEM Forms inclui apenas uma implementação de um contêiner de serviço. O container de serviço é responsável por gerenciar a duração de um serviço, incluindo a implantação e a garantia de que todas as solicitações sejam enviadas ao serviço correto. Ele também gerencia documentos que um serviço consome ou produz.

>[!NOTE]
>
>A programação com formulários AEM não inclui informações sobre como chamar o AEM Forms usando Pastas monitoradas ou email.

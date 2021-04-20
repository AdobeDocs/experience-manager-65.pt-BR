---
title: Tradução de conteúdo para sites multilíngues
seo-title: Tradução de conteúdo para sites multilíngues
description: Saiba como traduzir conteúdo para sites multilíngues.
seo-description: Saiba como traduzir conteúdo para sites multilíngues.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: Language Copy
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---


# Tradução do conteúdo para sites multilíngues {#translating-content-for-multilingual-sites}

Automatize a tradução de conteúdo da página, ativos e conteúdo gerado pelo usuário para criar e manter sites multilíngues. Para automatizar os fluxos de trabalho de tradução, você integra provedores de serviços de tradução ao AEM e cria projetos para traduzir o conteúdo em vários idiomas. AEM suporta fluxos de trabalho de tradução humana e de máquina.

* Tradução humana: O conteúdo é enviado para seu provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo traduzido é retornado e importado para o AEM. Quando seu provedor de tradução é integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.
* Tradução da máquina: O serviço de tradução automática traduz imediatamente seu conteúdo.

A tradução de conteúdo envolve as seguintes etapas:

1. [Conecte AEM com seu ](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) provedor de serviços de tradução e  [crie configurações](/help/sites-administering/tc-tic.md) de estrutura de integração de tradução.
1. [Associe as páginas do ](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) domínio de idioma com o serviço de tradução e as configurações de estrutura.
1. [Identifique o tipo de ](/help/sites-administering/tc-rules.md) conteúdo a ser traduzido.
1. [Prepare o conteúdo para ](/help/sites-administering/tc-prep.md) tradução criando o idioma principal e criando as páginas raiz das cópias de idioma.
1. [Crie ](/help/sites-administering/tc-manage.md) projetos de tradução para coletar o conteúdo para traduzir e preparar o processo de tradução.
1. Use os projetos de tradução para [gerenciar o processo de tradução de conteúdo](/help/sites-administering/tc-manage.md).

Se o seu provedor de serviços de tradução não fornecer um conector para integração com o AEM, o AEM oferecerá suporte à extração manual e à reinserção do conteúdo de tradução no formato XML.

>[!NOTE]
>
>Seu usuário precisa ser membro do grupo de administradores do projeto para usar os recursos de Cópia de idioma .

## Práticas recomendadas     {#best-practices}

A página [Práticas recomendadas de tradução](/help/sites-administering/tc-bp.md) contém informações importantes sobre sua implementação.

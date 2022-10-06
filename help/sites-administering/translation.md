---
title: Tradução de conteúdo para sites multilíngues
seo-title: Translating Content for Multilingual Sites
description: Saiba como traduzir conteúdo para sites multilíngues.
seo-description: Learn how to translate content for multilingual sites.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: Language Copy
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 83%

---

# Tradução de conteúdo para sites multilíngues {#translating-content-for-multilingual-sites}

Automatize a tradução de conteúdo da página, ativos e conteúdo gerado pelo usuário para criar e manter sites multilíngues. Para automatizar workflows de tradução, você integra provedores de serviços de tradução ao AEM e cria projetos para traduzir o conteúdo em vários idiomas. O AEM permite workflows de tradução humana e de máquina.

* Tradução humana: o conteúdo é enviado para seu provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo traduzido é retornado e importado para o AEM. Quando seu provedor de tradução é integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.
* Tradução automática: o serviço de tradução automática traduz imediatamente seu conteúdo.

A tradução de conteúdo envolve as seguintes etapas:

1. [Conecte o AEM com seu provedor de serviços de tradução](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) e [crie configurações da estrutura de integração de tradução](/help/sites-administering/tc-tic.md).
1. [Associe as páginas do seu idioma principal](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) com o serviço de tradução e as configurações da estrutura.
1. [Identifique o tipo de conteúdo](/help/sites-administering/tc-rules.md) para traduzir.
1. [Prepare o conteúdo para tradução](/help/sites-administering/tc-prep.md) criando o idioma principal e as páginas raiz das cópias de idioma.
1. [Crie projetos de tradução](/help/sites-administering/tc-manage.md) para coletar o conteúdo para traduzir e para preparar o processo de tradução.
1. Use os projetos de tradução para [gerenciar o processo de tradução de conteúdo](/help/sites-administering/tc-manage.md).

Se o seu provedor de serviços de tradução não fornecer um conector para integração com o AEM, o AEM oferecerá suporte à extração manual e à reinserção do conteúdo de tradução no formato XML.

>[!NOTE]
>
>Seu usuário precisa ser membro do grupo de administradores do projeto para usar os recursos de Cópia de idioma .

## Práticas recomendadas     {#best-practices}

A página [Práticas recomendadas de tradução](/help/sites-administering/tc-bp.md) contém informações importantes sobre a implementação.

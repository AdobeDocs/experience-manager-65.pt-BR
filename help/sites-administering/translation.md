---
title: Traduzindo conteúdo para sites multilíngues
seo-title: Traduzindo conteúdo para sites multilíngues
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
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09

---


# Traduzindo conteúdo para sites multilíngues {#translating-content-for-multilingual-sites}

Automatize a tradução de conteúdo da página, ativos e conteúdo gerado pelo usuário para criar e manter sites multilíngues. Para automatizar os fluxos de trabalho de tradução, você integra os provedores de serviços de tradução ao AEM e cria projetos para traduzir o conteúdo em vários idiomas. O AEM suporta fluxos de trabalho de tradução automática e humana.

* Tradução humana: O conteúdo é enviado ao seu provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo convertido é retornado e importado para o AEM. Quando seu provedor de tradução está integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.
* Tradução automática: O serviço de tradução automática traduz imediatamente seu conteúdo.

A tradução de conteúdo envolve as seguintes etapas:

1. [Conecte o AEM ao seu provedor](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) de serviços de tradução e [crie configurações](/help/sites-administering/tc-tic.md)de estrutura de integração de tradução.
1. [Associe as páginas do seu idioma mestre](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) ao serviço de tradução e às configurações de estrutura.
1. [Identifique o tipo de conteúdo](/help/sites-administering/tc-rules.md) a ser traduzido.
1. [Prepare o conteúdo para tradução](/help/sites-administering/tc-prep.md) criando o idioma mestre e as páginas raiz das cópias de idioma.
1. [Crie projetos](/help/sites-administering/tc-manage.md) de tradução para coletar o conteúdo para traduzir e preparar o processo de tradução.
1. Use os projetos de tradução para [gerenciar o processo](/help/sites-administering/tc-manage.md)de tradução de conteúdo.

Se seu provedor de serviços de tradução não fornecer um conector para integração com o AEM, o AEM oferece suporte à extração e reinserção manuais do conteúdo de tradução no formato XML.

>[!NOTE]
>
>Seu usuário precisa ser membro do grupo de administradores do projeto para usar os recursos de Cópia de idioma.

## Práticas recomendadas {#best-practices}

A página Práticas recomendadas [de](/help/sites-administering/tc-bp.md) tradução contém informações importantes sobre sua implementação.

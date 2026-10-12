---
title: Tradução de conteúdo para sites multilíngues
description: Saiba como traduzir conteúdo para sites multilíngues.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: d9d38edd-df1b-480c-8f5e-72b62576f390
    internal-label: Site and page features
subfeature_v2:
  - id: e15a4109-ae5d-497d-b301-31149e35aed4
    internal-label: Language Copy Wizard
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 73%
---
# Tradução de conteúdo para sites multilíngues {#translating-content-for-multilingual-sites}

Automatize a tradução de conteúdo da página, ativos e conteúdo gerado pelo usuário para criar e manter sites multilíngues. Para automatizar fluxos de trabalho de tradução, você integra provedores de serviços de tradução ao AEM e cria projetos para traduzir o conteúdo em vários idiomas. O AEM permite fluxos de trabalho de tradução humana e de máquina.

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
>Seu usuário precisa ser membro do grupo projetos-administradores para usar os recursos de Cópia de idioma.

## Práticas recomendadas {#best-practices}

A página [Práticas recomendadas de tradução](/help/sites-administering/tc-bp.md) contém informações importantes sobre a implementação.

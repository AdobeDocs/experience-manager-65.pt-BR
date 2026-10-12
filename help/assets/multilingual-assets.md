---
title: Ativo multilíngue
description: Saiba como automatizar fluxos de trabalho para traduzir ativos, incluindo binários, metadados e tags em vários idiomas.
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
hide: true
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%
---
# Ativos multilíngues {#multilingual-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | Este artigo |

O [!DNL Adobe Experience Manager Assets] permite automatizar fluxos de trabalho de tradução em ativos (incluindo binários, metadados e tags) para gerar ativos em outros idiomas para uso em projetos multilíngues.

Para automatizar fluxos de trabalho de tradução, você integra provedores de serviços de tradução ao [!DNL Experience Manager] e cria projetos para traduzir ativos em vários idiomas. [!DNL Experience Manager] dá suporte a fluxos de trabalho de tradução humana e de máquina.

Tradução humana: os ativos traduzidos são retornados e importados para [!DNL Experience Manager]. Quando seu provedor de tradução é integrado ao [!DNL Experience Manager], os ativos são automaticamente enviados entre o [!DNL Experience Manager] e o provedor de tradução.

Tradução automática: o serviço de tradução automática traduz imediatamente os metadados e as tags dos ativos.

A tradução de ativos inclui o seguinte:

1. [Conectar o Experience Manager com o provedor de serviços de tradução](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Criar configurações da estrutura de integração de tradução](/help/sites-administering/tc-tic.md)
1. [Preparar ativos para tradução](preparing-assets-for-translation.md)
1. [Aplicar serviços de tradução em nuvem a pastas](transition-cloud-services.md)
1. [Criar projetos de tradução](translation-projects.md)

Se o seu provedor de serviços de tradução não fornecer um conector para integração com o [!DNL Experience Manager], use um [processo alternativo](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Consulte também [Criar projetos de tradução para fragmentos de conteúdo](creating-translation-projects-for-content-fragments.md).

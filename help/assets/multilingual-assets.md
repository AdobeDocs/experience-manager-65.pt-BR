---
title: Ativos multilíngues e tradução de ativos
description: Saiba como automatizar fluxos de trabalho para traduzir ativos, incluindo binários, metadados e tags em vários idiomas.
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 8%

---

# Ativos multilíngues {#multilingual-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/multilingual-assets.html?lang=en) |

[!DNL Adobe Experience Manager Assets] permite automatizar fluxos de trabalho de tradução em ativos (incluindo binários, metadados e tags) para gerar ativos em outros idiomas para usar em projetos multilíngues.

Para automatizar workflows de tradução, você integra provedores de serviços de tradução a [!DNL Experience Manager] e criar projetos para traduzir ativos em vários idiomas. [!DNL Experience Manager] suporta fluxos de trabalho de tradução humana e automática.

Tradução humana: Os ativos traduzidos são retornados e importados para o [!DNL Experience Manager]. Quando seu provedor de tradução está integrado ao [!DNL Experience Manager], os ativos são enviados automaticamente entre [!DNL Experience Manager] e o provedor de tradução.

Tradução da máquina: O serviço de tradução automática traduz imediatamente os metadados e as tags para os ativos.

A tradução de ativos inclui o seguinte:

1. [Conectar o Experience Manager com o provedor de serviços de tradução](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Criar configurações da estrutura de integração de tradução](/help/sites-administering/tc-tic.md)
1. [Preparar ativos para tradução](preparing-assets-for-translation.md)
1. [Aplicar serviços de nuvem de tradução a pastas](transition-cloud-services.md)
1. [Criar projetos de tradução](translation-projects.md)

Se seu provedor de serviços de tradução não fornecer um conector para integrar com [!DNL Experience Manager]use um [processo alternativo](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Consulte também [Criar projetos de tradução para fragmentos de conteúdo](creating-translation-projects-for-content-fragments.md).

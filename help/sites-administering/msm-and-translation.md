---
title: Administração do site
seo-title: Website Administration
description: Saiba como gerenciar sites multilíngues no AEM.
seo-description: Learn how to manage multilingual websites in AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 43%

---

# Administração do site{#website-administration}

As seguintes ferramentas de administração estão disponíveis para gerenciar sites e páginas:

* O Multi Site Manager (MSM) permite que você use o mesmo conteúdo de site em vários locais, permitindo variações:

   * [Reutilizar conteúdo: gerenciador de vários sites e Live Copy](/help/sites-administering/msm.md)

* A tradução permite automatizar a tradução do conteúdo da página, ativos e conteúdo gerado pelo usuário para criar e manter sites multilíngues:

   * [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md)

* Esses dois recursos podem ser combinados para atender a sites que são ambos [Multinacional e multilíngue](#multinational-and-multilingual-sites).

## Sites multinacionais e multilíngues {#multinational-and-multilingual-sites}

É possível criar conteúdo para sites multinacionais e multilíngues com eficiência usando o gerenciador de vários sites e o fluxo de trabalho de tradução. Crie um site principal em um idioma, para um país específico, e use esse conteúdo como base para outros sites, usando tradução quando necessário:

* [Traduzir](/help/sites-administering/translation.md) o site principal em diferentes idiomas.

* Use o [Gerenciador de vários sites](/help/sites-administering/msm.md) para:

   * Reutilize o conteúdo do site principal e as traduções para criar sites para outros países e culturas.
   * Limite o uso do Multi Site Manager para conteúdo em um idioma, por exemplo, inglês principal -> ramificações de idioma inglês em sites do país, francês principal -> ramificações de idioma francês em sites do país.
   * Quando necessário, desanexe elementos das cópias ativas para adicionar detalhes de localização.

O diagrama a seguir ilustra como os principais conceitos se cruzam (mas não mostra todos os níveis/elementos envolvidos):

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Neste cenário, e em situações comparáveis, o MSM não gerencia as diferentes versões de idioma dessa maneira.
>
>* [MSM](/help/sites-administering/msm.md) gerencia a implantação do conteúdo traduzido de um blueprint (por exemplo, um principal global) para as cópias ao vivo (por exemplo, os sites locais), dentro dos limites de um idioma.
>* Os recursos de integração de [tradução](/help/sites-administering/translation.md) do AEM, juntamente com serviços de gerenciamento de tradução de terceiros, gerenciam os idiomas e a tradução de conteúdo para esses diferentes idiomas.
>
>Para casos de uso mais avançados, o MSM também pode ser usado com conteúdo principal de vários idiomas.

>[!NOTE]
>
>Em todos os casos de uso, é recomendável ler as seguintes práticas recomendadas:
>
>* [Práticas recomendadas para MSM](/help/sites-administering/msm-best-practices.md); em particular:
   >
   >   * [Criar site](/help/sites-administering/msm-best-practices.md#create-site)
   >   * [MSM e sites multilíngues](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [Práticas recomendadas para tradução](/help/sites-administering/tc-bp.md)


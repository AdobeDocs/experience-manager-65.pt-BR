---
title: Administração do site
seo-title: Administração do site
description: Saiba como gerenciar sites multilíngues no AEM.
seo-description: Saiba como gerenciar sites multilíngues no AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
translation-type: tm+mt
source-git-commit: 0885fb6eb6b6a6b8fefd522b2656c8f64e0a537e

---


# Administração do site{#website-administration}

As seguintes ferramentas de administração estão disponíveis para gerenciar sites e páginas:

* O Multi Site Manager (MSM) permite que você use o mesmo conteúdo do site em vários locais, permitindo variações:

   * [Reutilizando conteúdo: Multi Site Manager e Live Copy](/help/sites-administering/msm.md)

* A tradução permite que você automatize a tradução de conteúdo da página, ativos e conteúdo gerado pelo usuário para criar e manter sites multilíngues:

   * [Traduzindo conteúdo para sites multilíngues](/help/sites-administering/translation.md)

* Esses dois recursos podem ser combinados para atender a sites [multinacionais e multilíngues](#multinational-and-multilingual-sites).

## Sites multinacionais e multilíngues {#multinational-and-multilingual-sites}

Você pode criar conteúdo para sites multinacionais e multilíngues com eficiência usando o Multi Site Manager e o fluxo de trabalho de tradução. Crie um site mestre em um idioma, para um país específico, em seguida, use esse conteúdo como base para outros sites, usando a tradução quando necessário:

* [Traduza](/help/sites-administering/translation.md) o site mestre em diferentes idiomas.

* Usar o [Multi Site Manager](/help/sites-administering/msm.md) para:

   * Reutilize o conteúdo do site mestre e as traduções para criar sites para outros países e culturas.
   * Certifique-se de limitar o uso do Multi Site Manager ao conteúdo em um idioma, por exemplo, mestre em inglês -> ramificações de idioma inglês em sites de países, mestre em francês -> ramificações de idioma francês em sites de países.
   * Quando necessário, desanexe elementos das cópias online para adicionar detalhes de localização.

O diagrama a seguir ilustra como os conceitos principais se cruzam (mas não mostra todos os níveis/elementos envolvidos):

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Nesse cenário, e em situações comparáveis, o MSM não gerencia as diferentes versões de idioma como tal.
>
>* [O MSM](/help/sites-administering/msm.md) gerencia a implantação de conteúdo traduzido de um blueprint (por exemplo, um mestre global) para as cópias online (por exemplo, os sites locais), dentro dos limites de um idioma.
>* Os recursos de integração de [tradução](/help/sites-administering/translation.md) do AEM, juntamente com serviços de gerenciamento de tradução de terceiros, gerenciam os idiomas e traduzem o conteúdo para esses diferentes idiomas.
>
>
Para casos de uso mais avançados, o MSM também pode ser usado em mestres de idioma.

>[!NOTE]
>
>Para todos os casos de uso, é recomendável ler as seguintes práticas recomendadas:
>
>* [Práticas recomendadas para a MSM](/help/sites-administering/msm-best-practices.md); em particular:
>
>   * [Criar site](/help/sites-administering/msm-best-practices.md#create-site)
>   * [Sites MSM e multilíngues](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [Práticas recomendadas para tradução](/help/sites-administering/tc-bp.md)

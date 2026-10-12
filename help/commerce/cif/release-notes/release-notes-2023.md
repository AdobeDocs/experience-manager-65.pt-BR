---
title: Notas de versão de 2023 do AEM Content and Commerce
description: Notas de versão de 2023 do Adobe Experience Manager Content and Commerce.
exl-id: 00349400-6860-4e3c-ba56-fa12afc5db1d
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 20%
---
# Visão geral da versão do Commerce integration framework GitHub

## Visão geral dos requisitos de sistema

Revise os requisitos mínimos do sistema na tabela abaixo para a versão do CIF que você está usando atualmente ou planeja usar no futuro.

| Componente | Requisitos do sistema |
|:-------|:-----------------------------------------------------------------------------------------------:|
| Complemento do CIF | Mínimo: esquemas do AEM 6.5.8, Adobe Commerce 2.3.5 GraphQL |
| Componentes principais da CIF | [Requisitos do sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Arquétipo de projeto do AEM | [Requisitos do sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data de lançamento: dezembro de 2023

| Componente | Versão | Detalhes |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Componentes principais da CIF | 2.12.4 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.4) |

### Correções de erros {#bug-fixes-december}

* Servlets de redirecionamento de produto e categoria registrados para o tipo de recurso da Página v3
* Corrigir eventos de pesquisa ao vivo da extensão do CIF AEP

## Data de lançamento: novembro de 2023

| Componente | Versão | Detalhes |
|:-------|:-------------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Complemento do CIF | 2023.11.23.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2023.11.23.00.zip) |
| Site de referência CIF Venia | 2023.11.08 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2023.11.08) |

### Correções de erros {#bug-fixes-november}

* Exibição de mais de 40 configurações no console de Configurações do CIF

## Data de lançamento: julho de 2023

| Componente | Versão | Detalhes |
|:-------|:-------:|--------------------------------------------------------------------------------------------------------------:|
| Componentes principais da CIF | 2.12.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.2) |

### Novidades {#what-is-new-july}

* Ganchos de filtro de produto no componente `ProductList`

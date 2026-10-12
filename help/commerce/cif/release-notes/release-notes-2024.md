---
title: Notas de versão de 2024 do AEM Content and Commerce
description: Conteúdo do Adobe Experience Manager e Notas de versão do Commerce 2024.
exl-id: 372e6a46-72bb-4db4-ad01-534ca723ae58
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
source-wordcount: '274'
ht-degree: 17%
---
# Visão geral da versão do Commerce integration framework GitHub

## Visão geral dos requisitos de sistema

Revise os requisitos mínimos do sistema na tabela abaixo para a versão do CIF que você está usando atualmente ou planeja usar no futuro.

| Componente | Requisitos do sistema |
|:-------|:-----------------------------------------------------------------------------------------------:|
| Complemento do CIF | Mínimo: esquemas do GraphQL do AEM 6.5.18, Adobe Commerce 2.3.5 |
| Componentes principais da CIF | [Requisitos do sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Arquétipo de projeto do AEM | [Requisitos do sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data de lançamento: outubro de 2024

| Componente | Versão | Detalhes |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Componentes principais da CIF | 2.15.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.15.0) |

### Correções de erros {#bug-fixes-October}

* Correção dos testes de interface do usuário para funcionarem corretamente com componentes principais do CIF.
* Solução de um problema em que o formato de URL da categoria não funcionava como esperado na instância da nuvem.

## Data de lançamento: setembro de 2024

| Componente | Versão | Detalhes |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Componentes principais da CIF | 2.14.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.14.2) |

### Melhorias {#improvements-September}

* Tornar o limite de categoria personalizável.

### Correções de erros {#bug-fixes-September}

* Os campos do Commerce não estão integrados corretamente ao editor de esquema de metadados do Assets.
* Problema com o multicampo de produtos do carrossel para arrastar e soltar.
* Problema com o multicampo de categoria do carrossel para arrastar e soltar
* O clique não funciona para os menus nas Informações da página na página do editor de categoria e produto.
* O número do pedido não está visível na página Confirmação do pedido.

## Data de lançamento: janeiro de 2024

| Componente | Versão | Detalhes |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Componentes principais da CIF | 2.12.6 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.6) |

### Correções de erros {#bug-fixes-january}

* Foi corrigido o botão Adicionar ao carrinho e o botão Adicionar à lista de desejos no componente de coleção de produtos

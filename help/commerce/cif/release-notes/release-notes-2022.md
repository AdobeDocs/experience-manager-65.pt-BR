---
title: Notas de versão do AEM Content and Commerce 2022
description: Notas de versão do AEM Content and Commerce 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 1a82930d9f0aa84cea590782aba2e70ec23b41c3
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 27%

---

# Visão geral da versão da Commerce Integration Framework do GitHub

## Visão geral dos requisitos do sistema

Analise os requisitos mínimos do sistema na tabela abaixo para a versão da CIF que você está usando ou planeja usar no futuro.

| Componente | Requisitos do sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas GraphQL |
| Componentes principais da CIF | [Requisitos do sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Arquétipo de projeto do AEM | [Requisitos do sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data de lançamento: Março de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.02.24.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Componentes principais da CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Site de referência CIF Venia | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Novidades {#what-is-new-march}

* Beta: Suporte ao AEM CIF Search Core Component Commerce LiveSearch
* SEO aprimorado para cenários de várias lojas: Os formatos de URL para PDP/PLP agora podem ser configurados em um nível de loja por meio das propriedades da Configuração da nuvem da CIF
* O seletor de produto oferece suporte a produtos preparados por meio da nova opção de filtro na interface do usuário.  Isso permite que os profissionais de conteúdo preparem o gerenciamento de conteúdo de produtos para lançamentos de produtos futuros
* Gerenciamento simplificado de configurações e tratamento de erros da CIF usando o nome da Configuração da nuvem da CIF em vez do url de proxy de configuração
* Seleção manual da categoria para a lista de produtos e os componentes do carrossel. Isso permite que os profissionais de conteúdo usem esses componentes em páginas de conteúdo, fora da experiência de catálogo

## Data de lançamento: Janeiro de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.01.20.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| Componentes principais da CIF | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| Site de referência CIF Venia | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### Novidades {#what-is-new-january}

* Componentes myAccount aprimorados
* O componente Recomendação de produto oferece suporte a tipos de página adicionais (página inicial, carrinho de compras, confirmação de pedido)
* **Lista de desejos**
   * Os visitantes conectados podem adicionar produtos a uma lista de desejos
   * O gerenciamento da lista de desejos e de seus produtos é possível por meio da myAccount
   * O botão “Adicionar à lista de desejos” pode ser ativado/desativado no nível de componente por meio de uma política (por exemplo, teaser de produto, detalhes do produto)
   * Disponível como um Componente principal e na loja AEM Venia

![Lista de desejos](/help/assets/CIF/wishlist.png)

---
title: Notas de versão do AEM Content and Commerce 2022
description: Notas de versão do AEM Content and Commerce 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 600a836ff7ae0be9fde107ff2828bb41e8eed98f
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 34%

---

# Visão geral da versão da Commerce Integration Framework do GitHub

## Visão geral dos requisitos do sistema

Analise os requisitos mínimos do sistema na tabela abaixo para a versão da CIF que você está usando ou planeja usar no futuro.

| Componente | Requisitos do sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas GraphQL |
| Componentes principais da CIF | [Requisitos do sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Arquétipo de projeto do AEM | [Requisitos do sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data de lançamento: Junho de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.06.xx.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| Componentes principais da CIF | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| Site de referência CIF Venia | 2022.7.2004 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Novidades {#what-is-new-june}

* O nome do modelo agora está visível no editor de Sites ao criar o modelo de catálogo de produtos

* Várias melhorias nos Componentes principais da CIF

### Correções de bugs {#bug-fixes-june}

* Adicionar token de logon à busca de preços no lado do cliente

* Componente de página incorreto no datalayer

## Data de lançamento: Maio de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.05.31.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| Componentes principais da CIF | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| Site de referência CIF Venia | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### Novidades {#what-is-new-may}

* Nova página de propriedades do cockpit de produtos para obter uma visão geral melhor e simplificada

![visão geral das propriedades do cockpit de produtos](/help/assets/CIF/product_cockpit_properties_overview.png)

* Aprimoramento da compatibilidade e robustez de conectores de terceiros na I/O Runtime

* Melhore o suporte para substituições de configuração do cliente GQL (por exemplo, definir o comportamento de armazenamento em cache personalizado)

### Correções de bugs {#bug-fixes-may}

* O campo seletor de produtos de vários valores mostra o 2º e os produtos adicionais como inválidos

* Ocasionalmente, o Seletor de produto fica oculto atrás dos componentes

## Data de lançamento: Abril de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.04.28.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| Componentes principais da CIF | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| Site de referência CIF Venia | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### Novidades {#what-is-new-april}

* Acesso rápido ao cockpit de produtos: Acesse facilmente as informações completas e detalhadas do produto com um clique no Editor de sites

   ![Habilitar lista de desejos](/help/assets/CIF/enable-wishlist.png)

* Suporte para componentes adicionais de comércio de marketing: Os componentes podem ser configurados para mostrar uma chamada para ação de adição ao carrinho e de lista de desejos

   ![Atalho do editor de sites para o cockpit de produtos](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## Data de lançamento: Fevereiro de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.02.24.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Componentes principais da CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Site de referência CIF Venia | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Novidades {#what-is-new-march}

* Beta: Suporte do componente principal de pesquisa CIF do AEM para o Commerce LiveSearch
* SEO aprimorado para cenários com várias lojas: os formatos de URL para PDP/PLP agora podem ser configurados no nível da loja por meio das propriedades de configuração da nuvem do CIF
* O seletor de produto oferece suporte a produtos preparados por meio da nova opção de filtro na interface.  Isso permite que os profissionais de conteúdo preparem o gerenciamento de conteúdo do produto para lançamentos de produtos futuros
* Gerenciamento simplificado de configurações e tratamento de erros do CIF usando o nome de configuração da nuvem do CIF em vez da configuração do URL de proxy
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
   * O gerenciamento da lista de desejos e de seus produtos é possível por meio da opção myAccount
   * O botão “Adicionar à lista de desejos” pode ser ativado/desativado no nível de componente por meio de uma política (por exemplo, teaser de produto, detalhes do produto)
   * Disponível como um Componente principal e na loja AEM Venia

![Lista de desejos](/help/assets/CIF/wishlist.png)

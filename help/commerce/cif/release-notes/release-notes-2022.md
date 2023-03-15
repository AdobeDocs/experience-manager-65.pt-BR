---
title: Notas de versão do AEM Content and Commerce 2022
description: Notas de versão do AEM Content and Commerce 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 0fdff88695646603cec120d25f156f8c918686df
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 44%

---

# Visão geral da versão da Commerce Integration Framework do GitHub

## Visão geral dos requisitos do sistema

Analise os requisitos mínimos do sistema na tabela abaixo para a versão da CIF que você está usando ou planeja usar no futuro.

| Componente | Requisitos do sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas do GraphQL |
| Componentes principais da CIF | [Requisitos do sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Arquétipo de projeto do AEM | [Requisitos do sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data de lançamento: Setembro de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.09.20.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| Componentes principais da CIF | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| Site de referência CIF Venia | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### Novidades {#what-is-new-september}

* Os autores podem enriquecer dinamicamente listas de produtos com Fragmentos de experiência (Exemplo: Colocar banner entre as listas de produtos)
* O componente de lista suporta páginas de produto/categoria associadas para mostrar dinamicamente páginas relacionadas
* Suporte para componentes do Peregrine 12.5
* Suporte para carregamento de preço no lado do cliente em teaser e carrossel de produtos

## Data de lançamento: Julho de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.08.02.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### Novidades {#what-is-new-july}

* Associação de páginas de AEM a produtos e categorias por meio das propriedades AEM página mais visão geral do cockpit de produtos
   ![associação da página de cockpit do produto](/help/assets/CIF/product_cockpit_page_association.png)

## Data de lançamento: Junho de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.07.05.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| Componentes principais da CIF | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| Site de referência CIF Venia | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Novidades {#what-is-new-june}

* O enriquecimento do catálogo de produtos agora é compatível com as páginas do AEM. Isso permite que os autores gerenciem a associação entre página e produto.

* Várias melhorias nos Componentes principais da CIF

### Correções de erros {#bug-fixes-june}

* Adicionar token de logon à busca de preços no lado do cliente

* Componente de página incorreto no datalayer

## Data de lançamento: Maio de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.05.31.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| Componentes principais da CIF | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| Site de referência CIF Venia | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### Novidades {#what-is-new-may}

* Nova página de propriedades do cockpit do produto para obter uma visão geral melhor e simplificada

![visão geral das propriedades do cockpit do produto](/help/assets/CIF/product_cockpit_properties_overview.png)

* Aprimoramento da compatibilidade e robustez de conectores de terceiros no I/O Runtime

* Melhore o suporte para substituições de configuração do cliente GQL (por exemplo, definir o comportamento de armazenamento em cache personalizado)

### Correções de erros {#bug-fixes-may}

* O campo seletor de produtos de vários valores mostra o 2º produto e os demais produtos como inválidos

* Ocasionalmente, o seletor de produto fica oculto atrás dos componentes

## Data de lançamento: Abril de 2022

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.04.28.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| Componentes principais da CIF | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| Site de referência CIF Venia | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### Novidades {#what-is-new-april}

* Acesso rápido ao cockpit de produtos: acesse facilmente as informações completas e detalhadas do produto com um clique no Editor de sites

   ![Ativar lista de desejos](/help/assets/CIF/enable-wishlist.png)

* Compatibilidade com componentes adicionais de comércio de marketing: os componentes podem ser configurados para mostrar uma chamada para ação de adição ao carrinho e de lista de desejos

   ![Atalho do Editor de sites para o cockpit de produtos](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

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

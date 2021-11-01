---
title: Notas de versão do AEM Content and Commerce 2021
description: Notas de versão do AEM Content and Commerce 2021
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 7261a71769dfb968c768e0cb4835d7d4cca97b1a
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 9%

---

# Visão geral da versão da Commerce Integration Framework do GitHub

## Visão geral dos requisitos do sistema

Analise os requisitos mínimos do sistema na tabela abaixo para a versão da CIF que você está usando ou planeja usar no futuro.

**Com a versão de abril, substituímos o Conector da CIF do GitHub pelo complemento CIF** que está disponível no [Distribuição de software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html). A mudança para o complemento vem com grandes benefícios para os projetos:

* A maioria dos novos recursos estará disponível imediatamente no AEM 6.5 (Não há mais espera pela porta lateral do recurso)
* Fácil atualização para novas versões complementares
* Pronto para Cloud Service

O conector AEM CIF antigo está em modo de manutenção e não deve mais ser usado. Substitua o Conector da CIF pelo novo complemento CIF. A maior parte dos projetos deve poder ser substituída por um pacote simples.

| Componente | Requisitos do sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas GraphQL |
| Componentes principais da CIF | [Requisitos do sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Arquétipo de projeto do AEM | [Requisitos do sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data de lançamento: Outubro de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.10.20.20 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| Componentes principais da CIF | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| Site de referência CIF Venia | 2021.11.2001 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### Novidades {#what-is-new-october}

* O complemento CIF é compatível com as versões mais recentes do Commerce v2.4.3 com novas APIs e esquemas GraphQL .

* Os autores podem adicionar links para páginas de produtos e catálogos em campos de texto usando o editor de rich text (RTE). Um ícone da CIF foi adicionado à barra de ferramentas do RTE que abrirá os seletores para pesquisar e selecionar rapidamente o produto ou a categoria sem sair do contexto.

* O carrinho de compras pop-up e o check-out existentes foram substituídos por páginas dedicadas AEM carrinho de compras e check-out. As páginas são criadas usando componentes Magento Extensible Peregrine

* Os comerciantes podem ocultar determinadas categorias de catálogo de produtos na navegação usando o backend do Commerce. O Componente principal de navegação da CIF respeita a configuração de backend de comércio &quot;incluir no menu&quot; para mostrar/ocultar categorias na navegação

* AEM Storefront Venia retorna o erro HTTP 404 se a página de categoria ou produto não for encontrada

## Data de lançamento: Setembro de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.09.27 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| Componentes principais da CIF | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| Site de referência CIF Venia | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### Novidades {#what-is-new-september}

* A nova guia &quot;conteúdo comercial associado&quot; no editor Sites aumenta a eficiência do autor ao obter rapidamente acesso ao conteúdo relevante AEM produto para o contexto atual

   ![Conteúdo comercial associado](/help/assets/CIF/associated-commerce-content.png)

* Interface do usuário do seletor de produto aprimorada para melhor experiência do usuário, maior eficiência e suporte para catálogos de produtos complexos

   ![Novo seletor de produto](/help/assets/CIF/product-picker.png)

* Respeite a propriedade &quot;include_in_menu&quot; no componente de navegação

### Correções de bugs {#bug-fixes-september}

* A limpeza do cache do menu não está funcionando como esperado

* Erros JS durante AEM etapa de implantação do CS e quando não estiver usando componentes do cliente

* Não é possível criar a configuração da nuvem CIF em pastas que têm um nó sling:configs

## Data de lançamento: Agosto de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.9.2002 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| Componentes principais da CIF | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| Site de referência CIF Venia | 2021.8.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Novidades {#what-is-new-august}

* Nova interface do usuário do Seletor de categorias para melhorar a experiência do usuário, aumentar a eficiência e oferecer melhor suporte para catálogos de produtos complexos

   ![Novo seletor de categorias](/help/assets/CIF/category-picker.png)

* Melhor suporte A11Y para os Componentes principais da CIF

### Correções de bugs {#bug-fixes-august}

* Não é possível fechar a opção de filtro de categoria depois que ela estiver aberta

* Propriedade &quot;Texto da chamada para ação&quot; quebrada no teaser do produto

* Erros de JS da CIF durante AEM etapa de implantação do CS

* Corrigir o acesso de produto bruto para itens de lista de produtos mapeados

## Data de lançamento: Julho de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.07.21 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| Componentes principais da CIF | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| Site de referência CIF Venia | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Novidades {#what-is-new-july}

* Componentes principais da CIF v2
   * Configurações simplificadas e aprimoradas para URL PDP/PLP e SEO
   * Indicador visual para dados de produto preparados no modo de criação para melhor visibilidade das alterações futuras
   * Novo componente de mapa de site para páginas de conteúdo e comércio

* Suporte para [Adobe Commerce Sensei Product Recommendation, com a tecnologia Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) no AEM Storefront usando recomendações predefinidas ou criadas dinamicamente

## Data de lançamento: Junho de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.6.2018 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| Componentes principais da CIF | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| Site de referência CIF Venia | 2021.6.2012 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Novidades {#what-is-new-june}

* Novos tipos de dados de referência de produto e categoria da CIF para Fragmentos de conteúdo (Incl. suporte à interface do usuário do seletor de categoria/produto)
* Novo Componente principal do fragmento de conteúdo de comércio
* Pesquisa de comércio de texto completo compatível com AEM backend
* Os Componentes principais do Commerce são compatíveis com a coleta de dados do Adobe Commerce Sensei Recs
* URLs compatíveis com SEO aprimorados para páginas de categoria
* Suporte para cabeçalhos HTTP personalizados por site/configuração

## Data de lançamento: Maio de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.05.26 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| Componentes principais da CIF | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| Site de referência CIF Venia | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Novidades {#what-is-new-may}

* Suporte à paginação para conteúdo associado nas propriedades do console do produto

### Correções de bugs {#bug-fixes-may}

* Miniaturas de ativos não exibidas na guia Ativo das propriedades do produto

* A navegação estrutural redefine os dados de visualização no console do produto

## Data de lançamento: Abril de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.4.22 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Componentes principais da CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de referência CIF Venia | 2021.4.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novidades {#what-is-new-april}

* Suporte para UID de categoria - Isso desbloqueia integrações de comércio de terceiros para sistemas que usam Strings para ids de categoria

* AEM extensão para PWA Studio incl. integração de exemplo

* Novo componente principal de navegação da CIF que estende o componente principal de navegação do WCM

### Correções de bugs {#bug-fixes-april}

* O campo categoria raiz não era exibido na guia Comércio nas propriedades de página das páginas de categoria

## Data de lançamento: Março de 2021 {#what-is-new-march}

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 1.9.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 1.9.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de referência CIF Venia | 2021.03.25 | [Notas de versão](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novidades

* Suporte para Magento 2.4.2

### O que foi melhorado

* Melhor reutilização do componente de detalhes do produto para páginas orientadas por conteúdo

* Melhor armazenamento em cache e menos chamadas de back-end para PDPs

* Várias correções de erros.

## Data de lançamento: Fevereiro de 2021

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 1.8.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 1.8.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de referência CIF Venia | 2021.02.24 | [Notas de versão](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novidades {#what-is-new-february}

* Gerenciamento de experiência do produto: Enriqueça as páginas do catálogo de produtos individualmente com Fragmentos de experiência.

* Propriedades do console do produto estendido para mostrar Ativos vinculados e Fragmentos de experiência, incluindo ações para navegar rapidamente para o conteúdo associado.

### O que foi melhorado  {#what-is-improved-february}

* Camada de dados do lado do cliente aprimorada com url de imagem do produto e informações de categoria.

* Várias correções de erros.

## Data de lançamento: Janeiro de 2021

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 1.7.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 1.7.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de referência CIF Venia | 2021.2.2002 | [Notas de versão](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novidades {#what-is-new-january}

* Gerenciamento de experiência do produto: Nova guia de propriedade &quot;Comércio&quot; para Ativos e Fragmentos de experiência. Esta guia permite vincular Ativos e Fragmentos de experiência a produtos e categorias. A guia também mostra dados em tempo real para objetos de comércio vinculados e um link para mostrar detalhes no console do produto.

### O que foi melhorado  {#what-is-improved-january}

* Enviar dados do usuário após a autenticação para a Camada de dados do cliente do Adobe.

* Várias correções de erros.

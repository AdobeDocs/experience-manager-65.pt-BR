---
title: Notas de versão de 2021 do Adobe Experience Manager Content and Commerce
description: Notas de versão de 2021 do Adobe Experience Manager Content and Commerce
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 2810e34f642f4643fa4dc24b31a57a68e9194e39
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 13%

---

# Visão geral da versão do GitHub da estrutura de integração do comércio

## Visão geral dos requisitos de sistema

Consulte na tabela a seguir os requisitos mínimos do sistema para saber a versão da CIF que você está usando ou pretende usar no futuro.

| Componente | Requisitos do sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: esquemas do Adobe Experience Manager (AEM) 6.5.7, Adobe Commerce 2.3.5 GraphQL |
| Componentes principais da CIF | [Requisitos do sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Arquétipo de projeto do AEM | [Requisitos do sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data de lançamento: novembro de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.11.18.00 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| Componentes principais da CIF | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| Site de referência CIF Venia | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### Novidades {#what-is-new-november}

* Componentes myAccount estendidos baseados nos componentes Peregrine extensíveis do Commerce

![Componentes myAccount estendidos](/help/assets/CIF/extended-myAccount-components.png)

* Os autores podem criar Commerce Product Recommendations ad-hoc usando tipos de recomendações adicionais

* Suporte a cartões-presente na AEM Storefront

## Data de lançamento: outubro de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.10.20.02 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| Componentes principais da CIF | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| Site de referência CIF Venia | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### Novidades {#what-is-new-october}

* O complemento CIF é compatível com a versão mais recente do Commerce v2.4.3 com novas APIs e esquemas do GraphQL

* Os autores podem adicionar links para páginas de produtos e catálogos em campos de texto usando o editor de rich text (RTE). Foi adicionado um ícone da CIF à barra de ferramentas do RTE, que abre os seletores para pesquisar e selecionar rapidamente o produto ou categoria sem sair do contexto.

* O carrinho de compras pop-up e o check-out foram substituídos por páginas dedicadas de carrinho de compras e check-out para AEM. Os componentes nessas páginas são criados usando os componentes Peregrine extensíveis do Adobe Commerce

* Os comerciantes podem ocultar determinadas categorias de catálogo de produtos na navegação usando o back-end do Commerce. O componente principal de Navegação da CIF respeita a configuração de backend de comércio &quot;incluir no menu&quot; para mostrar/ocultar categorias na navegação

* AEM Storefront Venia retorna o erro HTTP 404 se a página de categoria ou produto não for encontrada

## Data de lançamento: setembro de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.09.27 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| Componentes principais da CIF | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| Site de referência CIF Venia | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### Novidades {#what-is-new-september}

* A nova guia &quot;conteúdo de comércio associado&quot; no editor de sites aumenta a eficiência do autor, obtendo rapidamente acesso ao conteúdo de produto AEM relevante para o contexto atual

  ![Conteúdo de comércio associado](/help/assets/CIF/associated-commerce-content.png)

* Interface aprimorada do seletor de produtos para obter melhor experiência do usuário, maior eficiência e suporte para catálogos de produtos complexos

  ![Novo seletor de produtos](/help/assets/CIF/product-picker.png)

* Respeitar a propriedade &quot;include_in_menu&quot; no componente de navegação

### Correções de erros {#bug-fixes-september}

* A limpeza do cache de menu não está funcionando como esperado

* Erros JS durante a etapa de implantação do AEM CS e quando não estão usando componentes do lado do cliente

* Não é possível criar a configuração de nuvem da CIF em pastas que têm um nó sling:configs

## Data de lançamento: agosto de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.09.02 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| Componentes principais da CIF | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| Site de referência CIF Venia | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Novidades {#what-is-new-august}

* Nova interface do Seletor de categorias para melhorar a experiência do usuário, aumentar a eficiência e melhorar o suporte para catálogos de produtos complexos

  ![Novo Seletor de Categoria](/help/assets/CIF/category-picker.png)

* Melhor suporte A11Y para os Componentes principais da CIF

### Correções de erros {#bug-fixes-august}

* Não é possível fechar a opção de filtro de categoria depois que ela está aberta

* A propriedade &quot;Texto de chamada para ação&quot; foi quebrada no teaser do produto

* Erros de CIF JS durante a etapa de implantação do AEM CS

* Corrigir acesso a produto bruto para itens de lista de produtos mapeados

## Data de lançamento: julho de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.07.21 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| Componentes principais da CIF | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| Site de referência CIF Venia | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Novidades {#what-is-new-july}

* Componentes principais da CIF v2
   * Configurações simplificadas e aprimoradas para URL e SEO de PDP/PLP
   * Indicador visual para dados de produtos preparados no modo de criação para melhor visibilidade de alterações futuras
   * Novo componente de mapa de site para páginas de conteúdo e comércio

* Suporte para [Recomendação de produto do Adobe Commerce Sensei, viabilizada pela Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) na Loja AEM usando recomendações predefinidas ou criadas dinamicamente

## Data de lançamento: junho de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.06.18 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| Componentes principais da CIF | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| Site de referência CIF Venia | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Novidades {#what-is-new-june}

* Novos tipos de dados de referência de produto e categoria da CIF para fragmentos de conteúdo (inclui suporte à interface do seletor de produto/categoria)
* Novo componente principal do fragmento de conteúdo de comércio
* Pesquisa de comércio de texto completo compatível com o back-end AEM
* Os Componentes principais do Commerce são compatíveis com a coleta de dados do Adobe Commerce Sensei Recs
* URLs otimizados e compatíveis com SEO para páginas de categoria
* Suporte para cabeçalhos HTTP personalizados por site/configuração

## Data de lançamento: maio de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.05.26 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| Componentes principais da CIF | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| Site de referência CIF Venia | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Novidades {#what-is-new-may}

* Suporte à paginação para conteúdo associado nas propriedades do console do produto

### Correções de erros {#bug-fixes-may}

* As miniaturas de ativos não são exibidas na guia Ativo das propriedades do produto

* A navegação estrutural redefine os dados de visualização no console do produto

## Data de lançamento: abril de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.04.22 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Componentes principais da CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de referência CIF Venia | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novidades {#what-is-new-april}

* Suporte para UID de categoria - Isso desbloqueia integrações comerciais de terceiros para sistemas que usam Strings para IDs de categoria

* Extensão AEM para PWA Studio incl. exemplo de integração

* Novo componente principal de navegação da CIF que estende o componente principal de navegação do WCM

### Correções de erros {#bug-fixes-april}

* O campo de categoria raiz não era exibido na guia commerce nas propriedades da página de páginas de categoria

## Data de lançamento: março de 2021 {#what-is-new-march}

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 1.9.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 1.9.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de referência CIF Venia | 2021.03.25 | [Notas de versão](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novidades

* Suporte para Adobe Commerce 2.4.2

### O que foi melhorado

* Melhoria na reutilização do componente de detalhes do produto para páginas orientadas por conteúdo

* Melhor armazenamento em cache e menos chamadas de back-end para PDPs

* Várias correções de erros.

## Data de lançamento: fevereiro de 2021

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 1.8.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 1.8.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de referência CIF Venia | 2021.02.24 | [Notas de versão](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novidades {#what-is-new-february}

* Gerenciamento de experiência do produto: enriqueça as páginas do catálogo de produtos individualmente com Fragmentos de experiência.

* Propriedades do console do produto estendido para mostrar Ativos vinculados e Fragmentos de experiência, incluindo ações para navegar rapidamente até o conteúdo associado.

### O que foi melhorado  {#what-is-improved-february}

* Camada de dados aprimorada do lado do cliente com url da imagem do produto e informações da categoria.

* Várias correções de erros.

## Data de lançamento: janeiro de 2021

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 1.7.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 1.7.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de referência CIF Venia | 2021.02.02 | [Notas de versão](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novidades {#what-is-new-january}

* Gerenciamento da experiência do produto: nova guia de propriedade &quot;Comércio&quot; para Ativos e Fragmentos de experiência. Essa guia permite vincular Ativos e Fragmentos de experiência a produtos e categorias. A guia também mostra dados em tempo real para objetos de comércio vinculados e um link para mostrar detalhes no console do produto.

### O que foi melhorado  {#what-is-improved-january}

* Enviar dados do usuário após autenticação para a Camada de dados do cliente Adobe.

* Várias correções de erros.

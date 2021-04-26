---
title: Notas de versão do AEM Content and Commerce 2021
description: Notas de versão do AEM Content and Commerce 2021
translation-type: tm+mt
source-git-commit: c2fb9af056fa4be13cfd7e60e8a44485e8712c0b
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 10%

---

# Visão geral da versão da Commerce Integration Framework do GitHub

## Data de lançamento: Novembro de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 0.7.1 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 0.6.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo da CIF | 0.6.2 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-november}

* Os autores podem visualizar os detalhes do produto e as páginas da lista de produtos com produtos/categorias com uma nova opção &quot;Exibir com produto/categoria&quot; no editor Sites.

* Os autores podem marcar ativos por SKU de produto e procurar ativos específicos do produto por SKU.

* Adicionar/remover suporte a cupom adicionado ao carrinho de compras.

* Suporte ao pagamento de Braintree adicionado AEM loja Venia.

### O que foi melhorado {#what-is-improved-november}

* Seletores de categoria/produto aprimorados para respeitar a exibição de loja de Magento especificada em uma configuração de várias lojas.

* Componentes baseados em reação disponíveis como um pacote npm. Isso permite que os desenvolvedores usem o pacote Componentes React como uma dependência para um novo projeto React para permitir a personalização de componentes existentes ou desenvolver novos componentes baseados no React.

* Personalização de consulta GraphQL simplificada. Isso permite que os desenvolvedores personalizem os componentes principais da CIF com menos código.

## Data de lançamento: Outubro de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 0.6.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 0,5.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo da CIF | 0,5.0 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-october}

* Modelos totalmente criáveis para a página de detalhes do produto e a página de lista de produtos. Os autores agora podem criar novos modelos e arrastar e soltar componentes de lista de produtos e detalhes do produto nesses modelos. Além de adicionar outros componentes, os autores agora podem alterar o layout desses modelos também, dando a eles liberdade ilimitada para criar experiências incríveis combinando conteúdo de marketing e comércio.

* Todos os componentes principais da CIF compatíveis com o autor foram aprimorados para oferecer suporte ao [Sistema de estilos AEM](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html). Os estilos de exemplo foram fornecidos para o componente de lista de produtos.

* Componentes do lado do cliente com base em reação para gerenciamento de conta. Esta versão é compatível com as seguintes funcionalidades: Faça logon, Esqueceu a senha e crie a conta.

### O que foi melhorado {#what-is-improved-october}

* Os detalhes do produto e os componentes da lista de produtos foram aprimorados para mostrar dados fictícios para fornecer aos autores uma visualização do layout quando esses componentes são colocados em um modelo/página.

* Os componentes Minicart e Checkout agora usam ganchos React para maior extensibilidade.

## Data de lançamento: Setembro de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 0,5.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 0.4.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo da CIF | 0.4.0 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-september}

* Recurso de vários modelos para permitir que os autores enriqueçam uma página específica de detalhes do produto ou uma página de lista de produtos. Os autores podem criar facilmente uma página personalizada de detalhes do produto ou uma página de lista de produtos e usar o seletor de produto ou categoria para atribuir a página personalizada a um produto ou categorias específicos.

* Vínculo de vários catálogos para permitir que os autores vinculem vários catálogos no console de produto AEM. Os autores também podem editar e exibir as propriedades de vínculo do catálogo após criar o vínculo.

* Check-out do lado do cliente com base em reação e minicarrinho usando GraphQL para oferecer suporte a uma jornada de compras básica completa.

* O componente de check-out inclui formulários de endereço, seleção de pagamento e seleção de método de entrega.

### O que foi melhorado {#what-is-improved-september}

* Os componentes Teaser do produto e Carrossel do produto suportam variantes de produto.

## Data de lançamento: Agosto de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 0.4.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 0.3.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo da CIF | 0.3.0 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-august}

* A incorporação do Conector da CIF no arquétipo da CIF era opcional para oferecer mais flexibilidade aos desenvolvedores.

* Os componentes da CIF foram dissociados do estilo CSS específico de &quot;Venia&quot; para permitir que os desenvolvedores apliquem o estilo CSS de sua escolha.

* Recurso de várias lojas/sites para permitir o uso dos Componentes principais da CIF em várias estruturas de site do AEM e permitir que a implementação de cliente GraphQL subjacente se conecte a diferentes visualizações de loja/loja do Magento.

* Cache GraphQL habilitado para determinadas consultas GraphQL via HTTP GET para reduzir o tempo de resposta.

* Exibição da descrição do produto ativada no console Produtos AEM.

* O Commerce Teaser estende o componente Teaser do WCM para permitir que os autores também adicionem campos CTA a uma página de detalhes do produto ou a uma página de lista de produtos.

* Botão para permitir que os autores coloquem em uma página de AEM e vinculem a uma página de AEM, página de detalhes do produto, página de lista de produtos ou um link externo.

### O que foi melhorado {#what-is-improved-august}

* A configuração da Magento store foi movida de OSGi para AEM console Produto para tornar a configuração de integração mais fácil de criar.

## Data de lançamento: Julho de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 0.3.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 0.2.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo da CIF | 0.2.0 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-july}

* Primeiro arquétipo da CIF para fornecer aos desenvolvedores várias opções de implantação: 1. Implante AEM loja Venia 2. Implante o scaffolding para um novo projeto 3. Usar elementos da CIF em um projeto existente

* Navegação de catálogos de vários níveis para oferecer suporte à navegação por categorias e subcategorias.

* Paginação em páginas de categoria para obter um melhor UX.

* Renderização do atributo de preço no lado do cliente nos componentes Detalhes do produto e Lista de produtos para suportar a renderização dos atributos dinâmicos.

* Carrossel de produtos do lado do servidor para exibir a lista de produtos em destaque em um estilo de carrossel.

* Lista de categorias de recursos do lado do servidor para exibir a lista de categorias em uma página de AEM.

### O que foi melhorado {#what-is-improved-july}

* O suporte para Magento 2.3.2 e correções de erros relacionadas às propriedades do produto são exibidos no console do produto.

## Data de lançamento: Junho de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector da CIF | 0.2.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais da CIF | 0.1.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |

### Novidades {#what-is-new-june}

* AEM vitrine B2C com estilo CSS Venia, página de aterrissagem, navegação dinâmica de catálogos por páginas de produto e categoria, página de pesquisa de produto e recursos de carrinho de compras para iniciar e acelerar projetos comerciais.

* O Conector da CIF e as ferramentas de criação (Console do produto, Seletor de produto e Seletor de categoria) para permitir que os autores criem experiências no AEM com conteúdo comercial.

* Primeira versão dos Componentes principais da CIF compatível com o Magento 2.3.1:
   * Detalhes do produto
   * Lista de produtos
   * Teaser do produto
   * Navegação
   * Pesquisa de produto
   * Carrinho de compras (REST)


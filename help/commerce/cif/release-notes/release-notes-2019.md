---
title: Conteúdo do AEM e Notas de versão do Commerce 2019
description: Notas de versão de 2019 do Adobe Experience Manager Content and Commerce.
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 6%

---

# Visão geral da versão do GitHub do Commerce integration framework

## Data de lançamento: novembro de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector CIF | 0.7.1 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais do CIF | 0.6.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo CIF | 0.6.2 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-november}

* Os autores podem visualizar as páginas de detalhes do produto e da lista de produtos com produtos/categorias com uma nova opção &quot;Exibir com produto/categoria&quot; no editor do Sites.

* Os autores podem marcar ativos por SKU do produto e pesquisar ativos específicos do produto por SKU.

* Adicionar/remover suporte a cupom adicionado ao carrinho de compras.

* Suporte para pagamento de Braintree adicionado na loja AEM Venia.

### O que foi melhorado {#what-is-improved-november}

* Seletores de categoria/produto aprimorados para respeitar a exibição de loja da Adobe Commerce especificada em uma configuração de várias lojas.

* Os componentes baseados no React estão disponíveis como um pacote npm. Isso permite que os desenvolvedores usem o pacote de Componentes do React como uma dependência para um novo projeto do React, permitindo a personalização de componentes existentes ou o desenvolvimento de novos componentes baseados no React.

* A personalização de query do GraphQL é simplificada. Isso permite que os desenvolvedores personalizem os componentes principais do CIF com menos código.

## Data de lançamento: outubro de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector CIF | 0.6.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais do CIF | 0.5.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo CIF | 0.5.0 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-october}

* Modelos totalmente autoráveis para a página de detalhes do produto e a página da lista de produtos. Os autores agora podem criar modelos e arrastar e soltar componentes de lista de produtos e detalhes do produto nesses modelos. Além de adicionar outros componentes, os autores agora podem alterar o layout desses modelos também, dando a eles liberdade ilimitada para criar experiências surpreendentes que combinam conteúdo de marketing e comércio.

* Todos os componentes principais do CIF compatíveis com autoria foram aprimorados para oferecer suporte ao [Sistema de Estilos do AEM](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html?lang=pt-BR). Estilos de exemplo foram fornecidos para o componente da lista de produtos.

* Componentes do lado do cliente baseados no React para gerenciamento de conta. Esta versão oferece suporte às seguintes funcionalidades: Fazer logon, Esqueceu a senha e Criar uma conta.

### O que foi melhorado {#what-is-improved-october}

* Os componentes de detalhes do produto e lista de produtos foram aprimorados para mostrar dados fictícios para fornecer aos autores uma pré-visualização do layout quando esses componentes são colocados em um modelo/página.

* Os componentes Minicart e Check-out agora usam ganchos React para melhorar a extensibilidade.

## Data de lançamento: setembro de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector CIF | 0.5.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais do CIF | 0.4.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo CIF | 0.4.0 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-september}

* O recurso de vários modelos permite que os autores enriqueçam uma página de detalhes do produto ou página de lista de produtos específica. Os autores podem criar facilmente uma página de detalhes do produto ou uma página de lista de produtos personalizada e usar o seletor de produto ou categoria para atribuir a página personalizada a um produto ou categoria específica.

* Vinculação de vários catálogos para permitir que os autores vinculem vários catálogos no console do produto AEM. Os autores também podem editar e exibir as propriedades de vinculação do catálogo após criar a vinculação.

* Check-out e minicarrinho do lado do cliente baseados no React usando o GraphQL para oferecer suporte a uma jornada básica completa de compras.

* O componente de Check-out inclui formulários de endereço, seleção de pagamento e seleção de método de envio.

### O que foi melhorado {#what-is-improved-september}

* Os componentes Teaser do produto e Carrossel do produto são compatíveis com variantes de produtos.

## Data de lançamento: agosto de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector CIF | 0.4.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais do CIF | 0.3.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo CIF | 0.3.0 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-august}

* A incorporação do Conector CIF no Arquétipo CIF é opcional para oferecer mais flexibilidade aos desenvolvedores.

* Componentes de CIF dissociados do estilo CSS específico do &quot;Venia&quot; para permitir que os desenvolvedores apliquem o estilo CSS de sua escolha.

* Recurso de várias lojas/sites para permitir o uso dos Componentes principais do CIF em várias estruturas de site do AEM e permitir que a implementação de cliente GraphQL subjacente se conecte a diferentes visualizações de loja/loja da Adobe Commerce.

* O armazenamento em cache do GraphQL é ativado para determinadas consultas do GraphQL via HTTP GET para reduzir o tempo de resposta.

* A visualização de descrição do produto é ativada no console Produtos AEM.

* O Commerce Teaser estende o componente WCM Teaser para permitir que os autores também adicionem campos CTA a uma página de detalhes do produto ou página de lista de produtos.

* Botão para permitir que os autores coloquem em uma página AEM e criem links para uma página AEM, uma página de detalhes do produto, uma página de lista de produtos ou um link externo.

### O que foi melhorado {#what-is-improved-august}

* A configuração da loja do Adobe Commerce mudou do OSGi para o console do produto AEM para tornar a configuração de integração mais fácil de ser criada.

## Data de lançamento: julho de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector CIF | 0.3.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais do CIF | 0.2.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquétipo CIF | 0.2.0 | [Notas de versão](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novidades {#what-is-new-july}

* Primeiro Arquétipo CIF a fornecer aos desenvolvedores várias opções de implantação: 1.Implante a loja AEM Venia 2. Implantar andaime para um novo projeto 3. Usar elementos de CIF em um projeto existente

* Navegação de catálogo de vários níveis para oferecer suporte à navegação por categorias e subcategorias.

* Paginação em páginas de categoria para melhor UX.

* Renderização do cliente do atributo de preço nos componentes Detalhes do produto e Lista de produtos para oferecer suporte à renderização de atributos dinâmicos.

* Carrossel de produtos do lado do servidor para exibir uma lista de produtos em destaque em um estilo de carrossel.

* Lista de categorias em destaque do lado do servidor para exibir uma lista de categorias em uma página de AEM.

### O que foi melhorado {#what-is-improved-july}

* O suporte para o Adobe Commerce 2.3.2 e correções de erros relacionados às propriedades do produto é exibido no console do produto.

## Data de lançamento: junho de 2019

| GitHub | Versão | Notas de versão detalhadas |
|:-------|:-----:|---------------------:|
| Conector CIF | 0.2.0 | [Notas de versão](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principais do CIF | 0.1.0 | [Notas de versão](https://github.com/adobe/aem-core-cif-components/releases) |

### Novidades {#what-is-new-june}

* Loja B2C AEM com estilo móvel Venia CSS, página de aterrissagem, navegação dinâmica do catálogo por páginas de produto e categoria, página de pesquisa de produto e recursos de carrinho de compras para iniciar e acelerar projetos de comércio.

* Conector CIF e ferramentas de criação (Console do produto, Seletor de produto e Seletor de categoria) para permitir que os autores criem experiências no AEM com conteúdo comercial.

* Primeira versão dos componentes principais do CIF compatível com o Adobe Commerce 2.3.1:
   * Detalhes do produto
   * Lista de produtos
   * Teaser do produto
   * Navegação
   * Pesquisa de produtos
   * Carrinho de compras (REST)

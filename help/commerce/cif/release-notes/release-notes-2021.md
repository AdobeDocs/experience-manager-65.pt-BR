---
title: Notas de versão do AEM Content and Commerce 2021
description: Notas de versão do AEM Content and Commerce 2021
translation-type: tm+mt
source-git-commit: 2d0b52dbf85e1fbe91c09a8366744aa77f25cd73
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 10%

---

# Visão geral da versão da Commerce Integration Framework do GitHub

## Visão geral dos requisitos do sistema

Analise os requisitos mínimos do sistema na tabela abaixo para a versão da CIF que você está usando ou planeja usar no futuro.

**O complemento CIF agora está disponível por meio da Distribuição de software do  [Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). O conector AEM CIF antigo está em modo de manutenção e não deve mais ser usado. Por favor, migre para o novo complemento CIF.**

| Componente | Requisitos do sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas GraphQL |
| Componentes principais da CIF | [Requisitos do sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Arquétipo de projeto do AEM | [Requisitos do sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Data de lançamento: Abril de 2021

| Componente | Versão | Detalhes |
|:-------|:-----:|---------------------:|
| Complemento CIF | v2021.04.22 | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Componentes principais da CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de referência CIF Venia | 2021.4.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novidades {#what-is-new-april}

* **O complemento CIF agora está disponível por meio da Distribuição de software do  [Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). O conector AEM CIF antigo está em modo de manutenção e não deve mais ser usado. Por favor, migre para o novo complemento CIF.**

* Suporte para UID de categoria - Isso desbloqueia integrações de comércio de terceiros para sistemas que usam Strings para ids de categoria

* AEM extensão para PWA Studio incl. integração de exemplo

* Novo componente principal de navegação da CIF que estende o componente principal de navegação do WCM

* Indicador visual para dados de catálogo preparados na loja de AEM

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

* Reutilização aprimorada do componente de detalhes do produto para páginas orientadas por conteúdo

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

* Camada de dados do lado do cliente aprimorada com url de imagem do produto e informações de categoria

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

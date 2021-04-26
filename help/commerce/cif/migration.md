---
title: Migração para o complemento CIF (Commerce Integration Framework) da AEM
description: Como migrar para o complemento CIF (Commerce Integration Framework) do AEM de uma versão antiga
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 1%

---

# Guia de migração para o complemento Experience Manager {#cif-migration}

Este guia ajuda a identificar as áreas que você precisa atualizar para a migração do complemento Experience Manager.

## Complemento CIF

O complemento CIF está disponível para o AEM 6.5 por meio do [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Ele é compatível e fornece os mesmos recursos do complemento CIF para o Experience Manager como um Cloud Service.

Consulte [Introdução ao Conteúdo AEM e Comércio](getting-started.md).

Para dar suporte a projetos que implantam o CIF Adobe, forneça [AEM os Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components).

## Catálogo de produtos

A importação de dados de catálogo de produtos não é compatível com o complemento CIF. Usando os principais componentes do complemento CIF, as solicitações de produtos e catálogos são sob demanda por meio de chamadas em tempo real para uma solução de comércio externo. Acesse Integração de capítulo para saber mais sobre a integração de uma solução comercial.

>[!TIP]
>
>Se nenhuma API em tempo real estiver disponível, um cache de produto externo com APIs deverá ser usado para a integração. Exemplo [Magento open-source](https://magento.com/products/magento-open-source).

## Experiências do catálogo de produtos com renderização de AEM

Se você usar o blueprint do catálogo com a CIF clássica, precisará atualizar o fluxo de trabalho do catálogo de produtos. O complemento CIF agora renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo de AEM. Não é mais necessária a replicação de dados de produto ou páginas de produto.

## Interação entre dados não armazenáveis em cache e compras

As solicitações do lado do cliente para dados e interações que não podem ser armazenados em cache (por exemplo, adicionar ao carrinho, pesquisa) devem ir diretamente para o terminal de comércio (solução comercial ou camada de integração) via CDN/Dispatcher. Remova qualquer chamada em que AEM era apenas um proxy.

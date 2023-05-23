---
title: Migração para o complemento AEM Commerce Integration Framework (CIF)
description: Como migrar de uma versão antiga para o complemento Estrutura de integração de comércio (CIF) do AEM
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 4%

---

# Guia de migração para o complemento do Experience Manager {#cif-migration}

Este guia ajuda a identificar as áreas que você precisa atualizar para a migração do complemento Experience Manager.

## Complemento CIF

O complemento CIF está disponível para AEM 6.5 por meio de [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html). Ele é compatível e fornece os mesmos recursos do complemento CIF para o Experience Manager as a Cloud Service.

Consulte [Introdução ao conteúdo e comércio de AEM](getting-started.md).

Para dar suporte a projetos que implantam a CIF, o Adobe fornece [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components).

## Catálogo de produtos

O complemento CIF não oferece suporte à importação de dados do catálogo de produtos. Usando as entidades principais do complemento CIF, as solicitações de produtos e catálogos são feitas sob demanda por meio de chamadas em tempo real para uma solução de comércio externo. Acesse o capítulo Integração para saber mais sobre a integração de uma solução comercial.

>[!TIP]
>
>Se nenhuma API em tempo real estiver disponível, um cache de produto externo com APIs deverá ser usado para a integração. Exemplo [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

## Experiências do catálogo de produtos com renderização do AEM

Se você usa o blueprint do catálogo com a CIF clássica, é necessário atualizar o fluxo de trabalho do catálogo de produtos. O complemento CIF agora renderiza experiências de catálogo de produtos de maneira rápida usando modelos de catálogo AEM. Não é mais necessária a replicação de dados ou páginas de produtos.

## Interação de compra e dados não armazenáveis em cache

As solicitações do lado do cliente para dados e interações não armazenáveis em cache (por exemplo, adição ao carrinho, pesquisa) devem ir diretamente para o endpoint de comércio (solução de comércio ou camada de integração) por meio de CDN/Dispatcher. Remova todas as chamadas em que o AEM era apenas um proxy.

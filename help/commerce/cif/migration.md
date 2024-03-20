---
title: Migração para o complemento AEM Commerce integration framework (CIF)
description: Como migrar de uma versão antiga para o complemento AEM Commerce integration framework (CIF).
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Guia de migração para o complemento do Experience Manager {#cif-migration}

Este guia ajuda a identificar as áreas que você precisa atualizar para a migração do complemento Experience Manager.

## Complemento para CIF

O complemento CIF está disponível para AEM 6.5 por meio de [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html). Ele é compatível e fornece os mesmos recursos que o complemento CIF para o Experience Manager as a Cloud Service.

Consulte [Introdução ao conteúdo e comércio de AEM](getting-started.md).

Para apoiar projetos que implantam o CIF, o Adobe fornece [AEM Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components).

## Catálogo de produtos

A importação de dados do catálogo de produtos não é suportada pelo complemento CIF. Usando os princípios complementares do CIF, as solicitações de produtos e catálogos são feitas sob demanda por meio de chamadas em tempo real para uma solução de comércio externo. Acesse o capítulo Integração para saber mais sobre a integração de uma solução comercial.

>[!TIP]
>
>Se nenhuma API em tempo real estiver disponível, um cache de produto externo com APIs deverá ser usado para a integração. Exemplo [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

## Experiências do catálogo de produtos com renderização do AEM

Se você usar o blueprint do catálogo com CIF clássico, será necessário atualizar o fluxo de trabalho do catálogo de produtos. O complemento CIF agora renderiza experiências de catálogo de produtos de maneira instantânea usando modelos de catálogo AEM. Não é mais necessária a replicação de dados ou páginas de produtos.

## Interação de compra e dados não armazenáveis em cache

As solicitações do lado do cliente para dados e interações não armazenáveis em cache (por exemplo, adição ao carrinho, pesquisa) devem ir diretamente para o endpoint de comércio (solução de comércio ou camada de integração) por meio de CDN/Dispatcher. Remova todas as chamadas em que o AEM era apenas um proxy.

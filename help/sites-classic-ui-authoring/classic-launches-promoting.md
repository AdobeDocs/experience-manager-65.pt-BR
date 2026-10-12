---
title: Promoção de inicializações
description: É necessário promover as páginas de lançamento para mover o conteúdo de volta para a origem (produção) antes de publicar. Quando uma página de lançamento é promovida, a página de origem correspondente é substituída pelo conteúdo da página promovida.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 63%
---
# Promoção de inicializações{#promoting-launches}

É necessário promover as páginas de lançamento para mover o conteúdo de volta para a origem (produção) antes de publicar. Quando uma página de lançamento é promovida, a página de origem correspondente é substituída pelo conteúdo da página promovida. As seguintes opções estão disponíveis ao promover uma página de lançamento:

* Promover somente a página atual ou todo o lançamento.
* Promover as páginas filhas da página atual.
* Promover o lançamento completo ou somente as páginas alteradas.

## Promover páginas de lançamento {#promoting-launch-pages}

Para promover páginas, execute as seguintes etapas ao editar a página de inicialização que deseja promover:

1. Na guia **Página** do Sidekick, clique em **Promover Inicialização**.
1. Especificar as páginas a serem promovidas:

   * (Padrão) Para promover somente a página atual, selecione **Promover alterações de página para versão de produção**.
   * Para promover também as páginas secundárias da página atual, selecione **Incluir subpáginas**.
   * Para promover todas as páginas no lançamento, selecione **Promover Inicialização Completa para Versão de Produção**.

1. Para adicionar as páginas de produção a um pacote de fluxo de trabalho, selecione **Adicionar ao Pacote de Fluxo de Trabalho** e, em seguida, selecione o pacote de fluxo de trabalho.
1. Clique em **Promover**.

## Processamento de Páginas promovidas usando o fluxo de trabalho do AEM {#processing-promoted-pages-using-aem-workflow}

Use modelos de fluxo de trabalho para executar o processamento em massa das páginas de lançamento promovidas:

1. Crie um pacote de fluxo de trabalho.
1. Quando autores(as) promovem as páginas de lançamento, elas são armazenadas no pacote de fluxo de trabalho.
1. Inicie um modelo de fluxo de trabalho usando o pacote como o conteúdo.

Para iniciar um fluxo de trabalho automaticamente quando as páginas forem promovidas, [configure um iniciador de fluxo de trabalho](/help/sites-administering/workflows-starting.md#workflows-launchers) para o nó do pacote.

Por exemplo, você pode gerar solicitações de ativação de página automaticamente quando autores(as) promoverem páginas de lançamento. Configure um inicializador de fluxo de trabalho para iniciar o fluxo de trabalho Solicitar ativação quando o nó do pacote for modificado.

![chlimage_1-136](assets/chlimage_1-136.png)

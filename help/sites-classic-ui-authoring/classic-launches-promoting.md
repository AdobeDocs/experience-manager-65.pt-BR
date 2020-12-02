---
title: Promoção de lançamentos
seo-title: Promoção de lançamentos
description: Você precisa promover as páginas de lançamento para retornar o conteúdo à fonte (produção) antes de publicar. Quando uma página de lançamento é promovida, a página correspondente das páginas de origem é substituída pelo conteúdo da página promovida.
seo-description: Você precisa promover as páginas de lançamento para retornar o conteúdo à fonte (produção) antes de publicar. Quando uma página de lançamento é promovida, a página correspondente das páginas de origem é substituída pelo conteúdo da página promovida.
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 91%

---


# Promoção de lançamentos{#promoting-launches}

Você precisa promover as páginas de lançamento para retornar o conteúdo à fonte (produção) antes de publicar. Quando uma página de lançamento é promovida, a página correspondente das páginas de origem é substituída pelo conteúdo da página promovida. As seguintes opções estão disponíveis ao promover uma página de lançamento:

* Promover apenas a página atual ou o lançamento inteiro.
* Promover as páginas-filho da página atual.
* Promover o lançamento completo ou apenas as páginas que foram alteradas.

## Promoção de páginas de lançamento {#promoting-launch-pages}

Para promover páginas, realize as etapas a seguir ao editar a página de lançamento que você deseja promover:

1. Na guia **Página** no Sidekick, clique em **Promover lançamento**.
1. Especifique as páginas que serão promovidas:

   * (Padrão) Para promover somente a página atual, selecione **Promover alterações na página para a versão de produção**.
   * Para também promover as páginas secundárias da página atual, selecione **Incluir subpáginas**.
   * Para promover todas as páginas do lançamento, selecione **Promover o lançamento completo para a versão de produção**.

1. Para adicionar as páginas de produção a um pacote de fluxos de trabalho, selecione **Adicionar ao pacote de fluxo de trabalho** e selecione o pacote de fluxos de trabalho.
1. Clique em **Promover**.

## Processamento de Páginas promovidas usando o fluxo de trabalho do AEM {#processing-promoted-pages-using-aem-workflow}

Use modelos de fluxo de trabalho para realizar o processamento em massa de páginas de Lançamentos promovidos:

1. Crie um pacote de fluxos de trabalho.
1. Quando os autores promovem páginas de Lançamento, eles as armazenam no pacote de fluxos de trabalho.
1. Inicie um modelo de fluxo de trabalho usando o pacote como carga útil.

Para iniciar um fluxo de trabalho automaticamente quando as páginas forem promovidas, [configure um ativador de fluxo de trabalho](/help/sites-administering/workflows-starting.md#workflows-launchers) para o nó do pacote.

Por exemplo, você pode gerar automaticamente solicitações de ativação de página quando os autores promovem páginas de Lançamentos. Configure um ativador de fluxo de trabalho para iniciar o fluxo de trabalho Solicitar ativação quando o nó do pacote for modificado.

![chlimage_1-136](assets/chlimage_1-136.png)


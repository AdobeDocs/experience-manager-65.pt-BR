---
title: Promoção de inicializações
description: É necessário promover as páginas de inicialização para mover o conteúdo de volta para a origem (produção) antes de publicar. Quando uma página de inicialização é promovida, a página correspondente das páginas de origem é substituída pelo conteúdo da página promovida.
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 3%

---

# Promoção de inicializações{#promoting-launches}

É necessário promover as páginas de inicialização para mover o conteúdo de volta para a origem (produção) antes de publicar. Quando uma página de inicialização é promovida, a página correspondente das páginas de origem é substituída pelo conteúdo da página promovida. As seguintes opções estão disponíveis ao promover uma página de inicialização:

* Se deve promover somente a página atual ou toda a inicialização.
* Se as páginas secundárias da página atual devem ser promovidas.
* Se deve promover a inicialização completa ou somente as páginas que foram alteradas.

## Promover páginas de lançamento {#promoting-launch-pages}

Para promover páginas, execute as seguintes etapas ao editar a página de inicialização que deseja promover:

1. No **Página** no Sidekick, clique em **Promover lançamento**.
1. Especificar as páginas a serem promovidas:

   * (Padrão) Para promover somente a página atual, selecione **Promover Alterações Na Página Para A Versão De Produção**.
   * Para promover também as páginas secundárias da página atual, selecione **Incluir subpáginas**.
   * Para promover todas as páginas no lançamento, selecione **Promover Lançamento Completo Para Versão De Produção**.

1. Para adicionar as páginas de produção a um pacote de workflow, selecione **Adicionar ao pacote de fluxo de trabalho** e, em seguida, selecione o pacote de workflow.
1. Clique em **Promover**.

## Processamento de Páginas promovidas usando o fluxo de trabalho do AEM {#processing-promoted-pages-using-aem-workflow}

Usar modelos de fluxo de trabalho para executar o processamento em massa das páginas de inicializações promovidas:

1. Crie um pacote de fluxo de trabalho.
1. Quando os autores promovem as páginas do Launch, eles as armazenam no pacote de fluxo de trabalho.
1. Inicie um modelo de fluxo de trabalho usando o pacote como a carga.

Para iniciar um fluxo de trabalho automaticamente quando as páginas forem promovidas, [configurar um inicializador de fluxo de trabalho](/help/sites-administering/workflows-starting.md#workflows-launchers) para o nó do pacote.

Por exemplo, você pode gerar automaticamente solicitações de ativação de página quando os autores promovem páginas de Lançamentos. Configure um iniciador de fluxo de trabalho para iniciar o fluxo de trabalho Ativação de solicitação quando o nó do pacote for modificado.

![chlimage_1-136](assets/chlimage_1-136.png)

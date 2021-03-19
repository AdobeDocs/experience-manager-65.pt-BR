---
title: Console de Visão Geral da Live Copy
seo-title: Console de Visão Geral da Live Copy
description: Saiba mais sobre as noções básicas do Console de visão geral da Live Copy.
seo-description: Saiba mais sobre as noções básicas do Console de visão geral da Live Copy.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
feature: Gerenciamento de vários sites
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 2%

---


# Console de Visão Geral da Live Copy{#live-copy-overview-console}

O **Visão geral da Live Copy** permite:

* Exibir/gerenciar a herança em um site:

   * Exibir a árvore do blueprint e a estrutura de live copy correspondente, juntamente com o status da herança
   * Alterar o status da herança; por exemplo, suspender, retomar
   * Exibir propriedades do blueprint e da live copy

* Executar ações de implantação

## Abrir a visão geral da Live Copy {#opening-the-live-copy-overview}

Você pode abrir a Visão geral da Live Copy em:

* [Painel lateral Referências de uma página do blueprint (console Sites)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Propriedades de uma página do blueprint](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Abrindo a visão geral da Live Copy - Referências de uma página do Blueprint {#opening-live-copy-overview-references-for-a-blueprint-page}

O **Visão geral da Live Copy** pode ser aberto no painel lateral Referências **do console** Sites **:**

1. No console **Sites**, [navegue até a página do blueprint e selecione-a](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Abra o painel **[Referências](/help/sites-authoring/basic-handling.md#references)** e selecione **Live Copies**.

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >Você também pode abrir Referências primeiro e depois selecionar o blueprint.

1. Selecione **Visão geral da Live Copy** para mostrar e usar a visão geral de todas as live copies relacionadas ao blueprint selecionado.
1. Use **Close** para sair e retornar ao console **Sites**.

### Abrindo a visão geral da Live Copy - Propriedades de uma página do Blueprint {#opening-live-copy-overview-properties-of-a-blueprint-page}

O **Visão geral da Live Copy** pode ser aberto ao visualizar propriedades de uma página do blueprint:

1. Abra **Properties** para a página do blueprint apropriada.
1. Abra a guia **Blueprint** - a opção **Visão geral da Live Copy** será exibida na barra de ferramentas superior:

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. Selecione **Visão geral da Live Copy** para mostrar e usar a visão geral de todas as live copies relacionadas ao blueprint atual.

   >[!NOTE]
   >
   >Para obter mais detalhes, consulte também o artigo da Base de conhecimento [Mensagem de status Livecopy - Atualizada/Verde/Em Sincronização](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. Use **Close** para sair e retornar ao console **Sites**.

## Uso da visão geral da Live Copy {#using-the-live-copy-overview}

O **Visão geral da Live Copy** também pode ser usado para executar ações na live copy:

1. Abra o **Visão geral da Live Copy**.
1. Selecione o blueprint ou a página de Live Copy necessária - a barra de ferramentas será atualizada para mostrar as ações disponíveis. As [ações](/help/sites-administering/msm.md#terms-used) disponíveis dependem da seleção de uma página [blueprint](#actions-for-a-blueprint-page) ou [live copy](#actions-for-a-live-copy-page):

### Ações para uma Página do Blueprint {#actions-for-a-blueprint-page}

Quando você seleciona uma página do blueprint, as seguintes ações estão disponíveis:

![chlimage_1-361](assets/chlimage_1-361.png)

* Editar

   * Abra a página do blueprint para edição.

* [Implantação](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Execute uma implantação para enviar as alterações da origem para a live copy.

### Ações para uma página de Live Copy {#actions-for-a-live-copy-page}

Quando você seleciona uma página de Live Copy, as seguintes ações estão disponíveis:

![chlimage_1-362](assets/chlimage_1-362.png)

* Editar

   * Abra a página da live copy para edição.

* [Status do relacionamento](#relationship-status)

   * Exibir informações sobre o status e a herança.

* [Sincronizar](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Sincronize uma live copy para extrair as alterações da origem para a live copy.

* [Redefinir](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * Redefina uma página de Live Copy para remover todos os cancelamentos de herança e retornar a página ao mesmo estado que a página de origem.

* [Suspender](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * Desativa temporariamente a relação ativa entre uma live copy e sua página de blueprint.

* [Retomar](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * Resume permite que você reinstale uma relação suspensa.

* [Destacar](/help/sites-administering/msm.md#detaching-a-live-copy)

   * Remove permanentemente a relação ativa entre uma live copy e sua página de blueprint.

## Status do relacionamento {#relationship-status}

O console **Status do relacionamento** tem duas guias que fornecem um intervalo de funcionalidade:

* [Informações sobre o Status da Relação](#relationship-status-information)
* [Informações da Live Copy](#live-copy-information)

### Informações de Status da Relação {#relationship-status-information}

Esta guia fornece informações detalhadas sobre o status da relação entre o blueprint e a live copy:

![chlimage_1-363](assets/chlimage_1-363.png)

### Informações da Live Copy {#live-copy-information}

Esta guia permite visualizar e editar a configuração da live copy:

![chlimage_1-364](assets/chlimage_1-364.png)


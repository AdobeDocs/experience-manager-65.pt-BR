---
title: Trabalhar com conjuntos de formulários na área de trabalho do AEM Forms
seo-title: Trabalhar com conjuntos de formulários na área de trabalho do AEM Forms
description: Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para os usuários finais. Saiba como trabalhar com conjuntos de formulários na área de trabalho do AEM Forms.
seo-description: Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para os usuários finais. Saiba como trabalhar com conjuntos de formulários na área de trabalho do AEM Forms.
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---


# Trabalhar com conjuntos de formulários na área de trabalho do AEM Forms{#working-with-formsets-in-aem-forms-workspace}

Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para os usuários finais. Quando os usuários finais start para preencher um conjunto de formulários, eles são perfeitamente transitados de um formulário para outro. O conjunto de formulários pode ser submetido com apenas um clique. Para obter mais informações sobre conjuntos de formulários e como configurá-los, consulte [Conjunto de formulários no AEM Forms](../../forms/using/formset-in-aem-forms.md).

A área de trabalho do AEM Forms suporta conjuntos de formulários. Com conjuntos de formulários, vários formulários relacionados a um serviço ou processo podem ser agrupados para automatizar um processo de negócios e apresentados aos usuários finais. Nesse cenário, os usuários podem preencher o conjunto inteiro como um único e não há necessidade de arquivar, enviar e rastrear formulários ou processos individuais.

## Anexar um conjunto de formulários ao ponto de partida em um aplicativo de área de trabalho AEM Forms {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Crie o fluxo de trabalho do processo de negócios no Workbench. Para obter mais informações, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).
1. Nas propriedades do processo do ponto de partida, selecione **Usar um ativo CRX** em Apresentação e dados.

   ![1-3](assets/1-3.png)

1. Clique em ![navegar](assets/browse.png) (Procurar) ao lado do caminho do ativo CRX. A caixa de diálogo Selecionar ativo de formulário é exibida.

   ![2-1](assets/2-1.png)

1. Clique na guia **Formset**, selecione o formset relevante na lista e clique em **OK**.

1. Implante o aplicativo depois de atualizar outras propriedades relevantes do processo.

## Uso de formset na área de trabalho do AEM Forms {#using-formset-in-nbsp-aem-forms-workspace}

Quando um formset é anexado a um ponto de partida, o ponto de partida pode ser chamado, como qualquer outro ponto de partida é chamado, a partir da área de trabalho do AEM Forms.

As operações com suporte em formset pela área de trabalho do AEM Forms são:

* Salvar como rascunho
* Bloquear
* Desistir
* Enviar
* Adicionar anexos
* Adicionar notas
* Mover entre formulários em um conjunto de formulários usando os botões Voltar ou Próximo

![3-1](assets/3-1.png)

>[!NOTE]
>
>Para melhorar o desempenho durante a movimentação dos formulários anteriores e seguintes em um conjunto de formulários, todos os botões da área de trabalho (Voltar, Avançar, Salvar, Enviar e ... (Mais) são desativados até que o formulário relevante seja renderizado totalmente.


---
title: Trabalhar com conjuntos de formulários no espaço de trabalho do AEM Forms
seo-title: Working with Formsets in AEM Forms workspace
description: Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um conjunto único de formulários para os usuários finais. Saiba como trabalhar com conjuntos de formulários no AEM Forms Workspace.
seo-description: A formset is a collection of HTML5 forms grouped and presented as a single set of forms to end users. Learn how you can work with formsets in AEM Forms workspace.
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 2%

---

# Trabalhar com conjuntos de formulários no espaço de trabalho do AEM Forms{#working-with-formsets-in-aem-forms-workspace}

Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um conjunto único de formulários para os usuários finais. Quando os usuários finais começam a preencher um conjunto de formulários, eles são perfeitamente transitados de um formulário para outro. O conjunto de formulários pode ser enviado com apenas um clique. Para obter mais informações sobre conjuntos de formulários e como configurá-los, consulte [Conjunto de formulários no AEM Forms](../../forms/using/formset-in-aem-forms.md).

A área de trabalho do AEM Forms é compatível com conjuntos de formulários. Com conjuntos de formulários, vários formulários relacionados a um serviço ou processo podem ser agrupados para automatizar um processo de negócios e apresentados aos usuários finais. Nesse cenário, os usuários podem preencher todo o conjunto como um único e não há necessidade de arquivar, enviar e rastrear formulários ou processos individuais.

## Anexar um conjunto de formulários ao ponto de partida em um aplicativo do AEM Forms workspace {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Crie o fluxo de trabalho do processo de negócios no Workbench. Para obter mais informações, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).
1. Nas propriedades do processo do ponto de partida, selecione **Usar um ativo CRX** em Apresentação e dados.

   ![1-3](assets/1-3.png)

1. Clique em ![navegar](assets/browse.png) (Navegar) ao lado do caminho do ativo CRX. A caixa de diálogo Selecionar ativo do formulário é exibida.

   ![2-1](assets/2-1.png)

1. Clique no botão **Conjunto de formulários** , selecione o conjunto de formulários relevante na lista e clique em **OK**.

1. Implante o aplicativo após atualizar outras propriedades relevantes do processo.

## Uso de formset na área de trabalho do AEM Forms {#using-formset-in-nbsp-aem-forms-workspace}

Depois que um conjunto de formulários é anexado a um ponto de partida, o ponto de partida pode ser chamado, como qualquer outro ponto de partida é chamado, no espaço de trabalho do AEM Forms.

As operações compatíveis com o conjunto de formulários por meio da área de trabalho do AEM Forms são:

* Salvar como rascunho
* Bloquear
* Desistir
* Enviar
* Adicionar anexos
* Adicionar observações
* Mover entre formulários em um conjunto de formulários usando os botões Voltar ou Próximo

![3-1](assets/3-1.png)

>[!NOTE]
>
>Para melhorar o desempenho durante a movimentação de formulários anteriores e próximos em um conjunto de formulários, todos os botões do espaço de trabalho (Voltar, Próximo, Salvar, Enviar e ... (Mais)) são desativados até que o formulário relevante seja totalmente renderizado.

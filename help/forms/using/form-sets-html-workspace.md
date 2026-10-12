---
title: Trabalhar com conjuntos de formulários no espaço de trabalho do AEM Forms
description: Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para os usuários finais. Saiba como trabalhar com conjuntos de formulários no espaço de trabalho do AEM Forms.
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 3%
---
# Trabalhar com conjuntos de formulários no espaço de trabalho do AEM Forms{#working-with-formsets-in-aem-forms-workspace}

Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para os usuários finais. Quando os usuários finais começam a preencher um conjunto de formulários, eles são perfeitamente transferidos de um formulário para outro. O conjunto de formulários pode ser enviado com apenas um clique. Para obter mais informações sobre conjuntos de formulários e como configurá-los, consulte [Conjunto de formulários no AEM Forms](../../forms/using/formset-in-aem-forms.md).

O espaço de trabalho do AEM Forms é compatível com conjuntos de formulários. Com conjuntos de formulários, vários formulários relacionados a um serviço ou processo podem ser agrupados para automatizar um processo de negócios e apresentados aos usuários finais. Nesse cenário, os usuários podem preencher todo o conjunto como um só e não há necessidade de arquivar, enviar e rastrear formulários ou processos individuais.

## Anexar um conjunto de formulários ao ponto de partida em um aplicativo do espaço de trabalho do AEM Forms {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Crie o workflow do processo empresarial no Workbench. Para obter mais informações, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).
1. Nas propriedades do processo do ponto de partida, selecione **Usar um Ativo do CRX** em Apresentação e Dados.

   ![1-3](assets/1-3.png)

1. Clique em ![procurar](assets/browse.png) (Procurar) ao lado do caminho do ativo do CRX. A caixa de diálogo Selecionar ativo de formulário é exibida.

   ![2-1](assets/2-1.png)

1. Clique na guia **Formset**, selecione o conjunto de formulários relevante na lista e clique em **OK**.

1. Implante o aplicativo depois de atualizar outras propriedades relevantes do processo.

## Uso do conjunto de formulários no espaço de trabalho do AEM Forms {#using-formset-in-nbsp-aem-forms-workspace}

Depois que um conjunto de formulários é anexado a um ponto inicial, o ponto inicial pode ser chamado, como qualquer outro ponto inicial, do espaço de trabalho do AEM Forms.

As operações compatíveis com o conjunto de formulários por meio do espaço de trabalho do AEM Forms são:

* Salvar como rascunho
* Bloquear
* Desistir
* Enviar
* Adicionar anexos
* Adicionar Notas
* Mover entre formulários em um conjunto de formulários usando os botões Voltar ou Avançar

![3-1](assets/3-1.png)

>[!NOTE]
>
>Para melhorar o desempenho durante a movimentação dos formulários anteriores e seguintes em um conjunto de formulários, todos os botões do espaço de trabalho (Voltar, Avançar, Salvar, Enviar e ... (Mais)) são desativados até que o formulário relevante seja totalmente renderizado.

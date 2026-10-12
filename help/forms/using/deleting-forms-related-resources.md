---
title: Exclusão de formulários e recursos relacionados
description: Como excluir um formulário ou um ativo no AEM Forms e o impacto nos ativos referenciados e referenciadores e formulários XFA.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%
---
# Exclusão de formulários e recursos relacionados {#deleting-forms-and-related-resources}

Você pode excluir os formulários e os ativos para remover esses ativos do repositório. A operação de exclusão funciona em todos os tipos de ativos e pastas.

Se você excluir um ativo da instância do Autor, o ativo também será excluído da instância de Publicação. O servidor do AEM Forms consiste em instâncias de Autor e Publicação. A instância do Autor serve para criar e gerenciar ativos e recursos de formulários. A instância de Publicação contém os ativos de formulários publicados e recursos relacionados que estão disponíveis para usuários finais.

## Como excluir um formulário {#how-to-delete-a-form}

1. Faça logon na interface de usuário do AEM Forms, acessando `https://[hostname]:'port'/aem/forms.html.`
1. Navegue até o formulário que deseja excluir e selecione-o. Clique em Excluir ![aem6forms_delete2](assets/aem6forms_delete2.png) na barra de ferramentas e confirme a operação de exclusão.

   >[!NOTE]
   >
   >Somente um formulário pode ser excluído por vez. Exclua vários formulários individualmente ou exclua a pasta principal.

1. Antes de excluir um ativo, o AEM Forms verifica se há referências e solicita uma confirmação explícita. Clique em Forçar exclusão se desejar excluir o ativo independentemente do status do relacionamento.

   >[!NOTE]
   >
   >Excluir um ativo que é referenciado por outros ativos pode causar problemas funcionais.

   >[!NOTE]
   >
   >Se o ativo selecionado for uma pasta e contiver esse ativo em sua hierarquia, exclua outros ativos individualmente ou exclua a pasta inteira.

## Impacto da exclusão de um formulário XFA referenciado {#impact-of-deleting-a-referenced-xfa-form}

No AEM Forms, um modelo de formulário XFA pode ser referenciado por um formulário adaptável ou outro modelo de formulário XFA. Além disso, um modelo pode se referir a um recurso ou outro modelo XFA.

Não é aconselhável excluir um formulário XFA que esteja sendo referenciado por um formulário adaptável, pois ele pode corromper o formulário adaptável. Quando um formulário adaptável se refere a um formulário XFA, seus campos são vinculados. Após a exclusão de XFA, o formulário adaptável não pode sincronizar seus campos com os campos XFA e exibe uma mensagem de erro para esses campos. Para saber mais sobre o impacto da exclusão XFA referenciada e sobre AFs sujos, consulte [Atualização de formulários XFA referenciados](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

Para excluir esse formulário XFA, atualize o formulário adaptável e remova as associações com os campos XFA.

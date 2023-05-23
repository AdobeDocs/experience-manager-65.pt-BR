---
title: Exclusão de formulários e recursos relacionados
seo-title: Deleting forms and related resources
description: Como excluir um formulário ou um ativo no AEM Forms e o impacto nos ativos referenciados e referenciadores e formulários XFA.
seo-description: How to delete a form or an asset in AEM Forms and the impact on referenced and referring assets and XFA forms.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
role: Admin
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Exclusão de formulários e recursos relacionados {#deleting-forms-and-related-resources}

Você pode excluir os formulários e os ativos para remover esses ativos do repositório. A operação de exclusão funciona em todos os tipos de ativos e pastas.

Se você excluir um ativo da instância do Autor, o ativo também será excluído da instância de Publicação. O servidor do AEM Forms consiste em instâncias de Autor e Publicação. A instância do Autor serve para criar e gerenciar ativos e recursos de formulários. A instância de Publicação contém os ativos de formulários publicados e recursos relacionados que estão disponíveis para usuários finais.

## Como excluir um formulário {#how-to-delete-a-form}

1. Faça logon na interface do usuário do AEM Forms, acessando `https://[hostname]:'port'/aem/forms.html.`
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

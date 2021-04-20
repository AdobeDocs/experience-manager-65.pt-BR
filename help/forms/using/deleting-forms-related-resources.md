---
title: Exclusão de formulários e recursos relacionados
seo-title: Exclusão de formulários e recursos relacionados
description: Como excluir um formulário ou ativo no AEM Forms e o impacto nos ativos referenciados e de referência e formulários XFA.
seo-description: Como excluir um formulário ou ativo no AEM Forms e o impacto nos ativos referenciados e de referência e formulários XFA.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# Exclusão de formulários e recursos relacionados {#deleting-forms-and-related-resources}

É possível excluir os formulários e ativos para remover esses ativos do repositório. A operação de exclusão funciona em todos os tipos de ativos e pastas.

Se você excluir um ativo da instância do autor, o ativo também é excluído da instância de publicação. O servidor do AEM Forms consiste em instâncias de Autor e Publicação. A instância Autor é para criar e gerenciar ativos e recursos de formulários. A instância de publicação contém os ativos de formulários publicados e os recursos relacionados disponíveis para os usuários finais.

## Como excluir um formulário {#how-to-delete-a-form}

1. Faça logon na interface do usuário do AEM Forms acessando `https://[hostname]:'port'/aem/forms.html.`
1. Navegue até o formulário que deseja excluir e selecione-o. Clique em Excluir ![aem6forms_delete2](assets/aem6forms_delete2.png) na barra de ferramentas e confirme a operação de exclusão.

   >[!NOTE]
   >
   >Somente um formulário pode ser excluído de cada vez. Exclua vários formulários individualmente ou exclua a pasta principal.

1. Antes de excluir um ativo, o AEM Forms verifica referências e solicita uma confirmação explícita. Clique em Forçar exclusão se desejar excluir o ativo independentemente do status do relacionamento.

   >[!NOTE]
   >
   >A exclusão de um ativo referenciado por outros ativos pode causar problemas funcionais.

   >[!NOTE]
   >
   >Se o ativo selecionado for uma pasta e contiver esse ativo na hierarquia, exclua outros ativos individualmente ou exclua a pasta inteira.

## Impacto da exclusão de um formulário XFA referenciado {#impact-of-deleting-a-referenced-xfa-form}

No AEM Forms, um template de formulário XFA pode ser referenciado por um formulário adaptável ou outro template de formulário XFA. Além disso, um template pode se referir a um recurso ou outro template XFA.

Não é aconselhável excluir um formulário XFA que está sendo referenciado por um formulário adaptável, pois ele pode corromper o formulário adaptável. Quando um formulário adaptável se refere a um formulário XFA, seus campos são vinculados. Após a exclusão do XFA, o formulário adaptável não poderá sincronizar seus campos com os campos XFA e exibirá uma mensagem de erro para esses campos. Para saber mais sobre o impacto da exclusão de XFA referenciada e sobre AFs sujos, consulte [Atualização de formulários XFA referenciados](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

Para excluir esse formulário XFA, atualize o formulário adaptável e remova os vínculos com os campos XFA.

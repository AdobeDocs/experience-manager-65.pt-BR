---
title: Excluindo formulários e recursos relacionados
seo-title: Excluindo formulários e recursos relacionados
description: Como excluir um formulário ou ativo no AEM Forms e o impacto nos ativos referenciados e referenciadores e formulários XFA.
seo-description: Como excluir um formulário ou ativo no AEM Forms e o impacto nos ativos referenciados e referenciadores e formulários XFA.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Excluindo formulários e recursos relacionados {#deleting-forms-and-related-resources}

É possível excluir os formulários e ativos para remover esses ativos do repositório. A operação de exclusão funciona em todos os tipos de ativos e pastas.

Se você excluir um ativo da instância Autor, o ativo também será excluído da instância Publicar. O servidor de formulários AEM consiste em instâncias de autor e publicação. A instância Autor destina-se a criar e gerenciar ativos e recursos de formulários. A instância Publicar contém os ativos de formulários publicados e os recursos relacionados que estão disponíveis para usuários finais.

## Como excluir um formulário {#how-to-delete-a-form}

1. Faça logon na interface do usuário do AEM Forms acessando `https://[hostname]:'port'/aem/forms.html.`
1. Navegue até o formulário que deseja excluir e selecione-o. Clique em Excluir ![aem6forms_delete2](assets/aem6forms_delete2.png) da barra de ferramentas e confirme a operação de exclusão.

   >[!NOTE]
   >
   >Somente um formulário pode ser excluído por vez. Exclua vários formulários individualmente ou exclua a pasta pai.

1. Antes de excluir um ativo, o AEM Forms verifica se há referências e solicita uma confirmação explícita. Clique em Forçar exclusão se desejar excluir o ativo independentemente do status do relacionamento.

   >[!NOTE]
   >
   >A exclusão de um ativo referenciado por outros ativos pode causar problemas funcionais.

   >[!NOTE]
   >
   >Se o ativo selecionado for uma pasta e contiver esse ativo em sua hierarquia, exclua outros ativos individualmente ou exclua a pasta inteira.

## Impacto da exclusão de um formulário XFA referenciado {#impact-of-deleting-a-referenced-xfa-form}

No AEM Forms, um modelo de formulário XFA pode ser referenciado por um formulário adaptável ou outro modelo de formulário XFA. Além disso, um modelo pode fazer referência a um recurso ou outro modelo XFA.

Não é aconselhável excluir um formulário XFA que esteja sendo referenciado por um formulário adaptável, pois ele pode corromper o formulário adaptável. Quando um formulário adaptável se refere a um formulário XFA, seus campos são vinculados. Após a exclusão do XFA, o formulário adaptável não pode sincronizar seus campos com os campos XFA e exibe uma mensagem de erro para esses campos. Para saber mais sobre o impacto da exclusão XFA referenciada e sobre AFs sujos, consulte [Atualização de formulários](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)XFA referenciados.

Para excluir um formulário XFA, atualize o formulário adaptável e remova os vínculos com os campos XFA.

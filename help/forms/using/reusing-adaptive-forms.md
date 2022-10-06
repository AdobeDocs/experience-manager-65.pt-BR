---
title: Reutilização de formulários adaptáveis
seo-title: Reusing adaptive forms
description: É possível reutilizar um formulário adaptável existente para criar novos formulários adaptáveis.
seo-description: You can reuse an existing adaptive form to create new adaptive forms.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Reutilização de formulários adaptáveis {#reusing-adaptive-forms}

## Introdução {#introduction}

Se você quiser usar algumas das propriedades de um formulário adaptável existente para gerar um novo formulário, basta usar a funcionalidade copiar e colar. Além disso, é possível colar o novo formulário adaptável no caminho de pasta desejado. Todas as propriedades de metadados são replicadas e os XFA e os XSDs para formulários adaptáveis baseados em XFA e XSD também são copiados.

>[!NOTE]
>
>O status e os detalhes da revisão não são copiados. Por exemplo, se o formulário adaptável for publicado e, ao copiá-lo, o formulário adaptável colado estará no estado não publicado. Da mesma forma, se um ativo copiado estiver sob revisão, o ativo colado não estará sob a mesma revisão.

### Copiar um formulário adaptável {#copy-an-adaptive-form}

Copie um formulário adaptável usando uma das seguintes abordagens:

1. Clique em copiar ![aem6forms_copy](assets/aem6forms_copy.png) ícone das Ações rápidas.

   >[!NOTE]
   >
   >As ações rápidas são itens de ação exibidos em uma miniatura ao passar o mouse.

1. Selecione o formulário adaptável. O processo de seleção é diferente para diferentes exibições.

   Se você estiver na exibição de cartão, vá para o modo de seleção clicando na seleção ![aem6forms_check-círculo](assets/aem6forms_check-circle.png) e clique em todos os formulários adaptáveis que deseja copiar.

   Se você estiver na exibição em lista, clique nas caixas de seleção de todos os formulários adaptáveis para selecioná-los.

   >[!NOTE]
   >
   >Todos os ativos selecionados devem ser formulários adaptáveis, pois a funcionalidade copiar-colar é suportada somente para formulários adaptáveis e todos os ativos selecionados devem estar presentes na mesma pasta.

   Depois de selecionar os ativos, clique no botão copiar ![aem6forms_copy](assets/aem6forms_copy.png) ícone presente na barra de ferramentas para copiar o formulário adaptável selecionado.

### Colar um formulário adaptável {#paste-an-adaptive-form}

Clicar na ação de cópia sai automaticamente do modo de seleção e faz com que a colagem ![aem6forms_paste](assets/aem6forms_paste.png) ícone visível. Agora vá para o caminho da pasta desejada e clique no botão colar ![aem6forms_paste](assets/aem6forms_paste.png) ícone para colar o formulário adaptável copiado.

Se você estiver colando na mesma pasta ou em outro arquivo com o mesmo nome de nó (com o qual está armazenado no repositório CRX) existir nessa pasta de destino, 1 será anexado ao sufixo (por exemplo, myaf se torna myaf1 e se myaf1 existir no mesmo local, myaf se torna myaf2. Todas as outras propriedades permanecem iguais ao formulário adaptável original.

Depois de clicar no botão colar ![aem6forms_paste](assets/aem6forms_paste.png) ícone , ele ficará novamente oculto. De uma vez, você só pode colar uma vez. Para criar novamente uma cópia do mesmo ativo, copie-o novamente.

### Alterar conteúdo do novo formulário adaptável {#change-contents-of-new-adaptive-form}

O conteúdo de um formulário adaptável colado pode ser alterado usando as seguintes abordagens para torná-lo diferente do formulário copiado:

1. **Alterar propriedades de metadados:**

   É possível alterar as propriedades de metadados do formulário adaptável, por exemplo, título e descrição. Para obter mais detalhes sobre as propriedades de metadados e como eles podem ser alterados, consulte [Gerenciamento de metadados de formulário](/help/forms/using/manage-form-metadata.md)

1. **Altere o XFA/XSD para o Forms adaptável baseado em XFA/XSD:**

   Você pode alterar o XFA/XSD usado em formulários adaptáveis. Para saber como esses formulários adaptáveis podem ser alterados, consulte [Gerenciamento de metadados de formulário](/help/forms/using/manage-form-metadata.md)

1. **Publicar novamente:**

   O ativo colado é diferente do copiado. Você pode publicá-lo como um novo ativo para torná-lo disponível para os usuários finais. Para saber como publicar um ativo, consulte [Publicar e desfazer a publicação de formulários](/help/forms/using/publishing-unpublishing-forms.md)

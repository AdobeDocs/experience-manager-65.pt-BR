---
title: Alterar a aparência
description: Saiba como editar o script comment.hbs responsável pela criação do HTML geral para cada comentário nas comunidades do Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Alterar a aparência {#alter-the-appearance}

## Modificar o script {#modify-the-script}

O script `comment.hbs` é responsável pela criação do HTML geral para cada comentário.

Para não exibir o avatar ao lado de cada comentário publicado:

1. Copiar `comment.hbs`de `libs`para `apps`

   1. Selecionar `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Selecionar **[!UICONTROL Cópia]**
   1. Selecionar `/apps/social/commons/components/hbs/comments/comment`
   1. Selecionar **[!UICONTROL Colar]**

1. Abrir o `comment.hbs` sobreposto

   * Clique duas vezes no nó `comment.hbs` em `/apps/social/commons/components/hbs/comments/comment folder`

1. Localize as linhas a seguir e exclua-as ou comente-as:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Exclua as linhas ou coloque-as entre `<!--` e `-->` e comente-as. Além disso, os caracteres &quot;xxx&quot; estão sendo adicionados como um indicador visual de onde o avatar estaria.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Replicar a sobreposição {#replicate-the-overlay}

Envie o componente de comentários sobrepostos para a instância de publicação usando a Ferramenta de replicação.

>[!NOTE]
>
>Uma forma mais robusta de replicação seria criar um pacote no Gerenciador de Pacotes e [ativá-lo](/help/sites-administering/package-manager.md#replicating-packages). Um pacote pode ser exportado e arquivado.

Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** e clique em **[!UICONTROL Ativar árvore]**.

Para o Caminho Inicial, insira `/apps/social/commons` e selecione **[!UICONTROL Ativar]**.

![verificar-modelo-conteúdo](assets/verify-content-template.png)

### Exibir resultados {#view-results}

Se você fizer logon na instância de publicação como administrador, por exemplo, https://localhost:4503/crx/de como administrador/administrador, será possível verificar se os componentes sobrepostos estão lá.

Se você fizer logoff, depois fazer logon como `aaron.mcdonald@mailinator.com/password` e atualizar a página, verá que um avatar não será exibido com o comentário postado. Em vez disso, um simples &quot;xxx&quot; é exibido.

![criar-componente-modelo](assets/create-template-component.png)

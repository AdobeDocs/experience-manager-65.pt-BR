---
title: Alterar a aparência
seo-title: Alterar a aparência
description: Modificar o script
seo-description: Modificar o script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Altere a aparência {#alter-the-appearance}

## Modificar o script {#modify-the-script}

O script comment.hbs é responsável pela criação do HTML geral para cada comentário.

Para não exibir o avatar ao lado de cada comentário publicado:

1. Copiar `comment.hbs`de `libs`para `apps`

   1. Selecionar `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Selecione **[!UICONTROL Copiar]**
   1. Selecionar `/apps/social/commons/components/hbs/comments/comment`
   1. Selecione **[!UICONTROL Colar]**

1. Abra o `comment.hbs` sobreposto

   * Duplo clique no nó `comment.hbs` em `/apps/social/commons/components/hbs/comments/comment folder`

1. Encontre as seguintes linhas e exclua-as ou comente-as:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Exclua as linhas ou rode-as com `<!--` e `-->` para comentá-las. Além disso, os caracteres &#39;xxx&#39; estão sendo adicionados como um indicador visual de onde o avatar estaria.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Replicar a sobreposição {#replicate-the-overlay}

Encaminhe o componente de comentários sobrepostos para a instância de publicação usando a Ferramenta de Replicação.

>[!NOTE]
>
>Uma forma mais robusta de replicação seria criar um pacote no Package Manager e [ativá-lo](/help/sites-administering/package-manager.md#replicating-packages). Um pacote pode ser exportado e arquivado.

Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** e clique em **[!UICONTROL Ativar árvore]**.

Para Caminho do Start, digite `/apps/social/commons` e selecione **[!UICONTROL Ativar]**.

![verify-content-template](assets/verify-content-template.png)

### Resultados da visualização {#view-results}

Se você fizer logon na instância de publicação como administrador, por exemplo, https://localhost:4503/crx/de como administrador/administrador, poderá verificar se os componentes sobrepostos estão lá.

Se você efetuar logout e login novamente como `aaron.mcdonald@mailinator.com/password` e atualizar a página, você observará que o comentário publicado não é mais exibido com um avatar, em vez disso, um simples &#39;xxx&#39; é exibido.

![create-template-component](assets/create-template-component.png)


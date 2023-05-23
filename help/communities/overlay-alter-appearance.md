---
title: Alterar a aparência
seo-title: Alter the Appearance
description: Modificar o script
seo-description: Modify the script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# Alterar a aparência {#alter-the-appearance}

## Modificar o script {#modify-the-script}

O script comment.hbs é responsável pela criação do HTML geral para cada comentário.

Para não exibir o avatar ao lado de cada comentário publicado:

1. Copiar `comment.hbs`de `libs`para `apps`

   1. Selecionar `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Selecionar **[!UICONTROL Copiar]**
   1. Selecionar `/apps/social/commons/components/hbs/comments/comment`
   1. Selecionar **[!UICONTROL Colar]**

1. Abrir a sobreposta `comment.hbs`

   * Clique duas vezes no nó `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. Localize as linhas a seguir e exclua-as ou comente-as:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Exclua as linhas ou coloque-as em volta `<!--` e `-->` para comentá-los. Além disso, os caracteres &quot;xxx&quot; estão sendo adicionados como um indicador visual de onde o avatar estaria.

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
>Uma forma mais robusta de replicação seria criar um pacote no Gerenciador de pacotes e [ativar](/help/sites-administering/package-manager.md#replicating-packages) o mesmo. Um pacote pode ser exportado e arquivado.

Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** e clique em **[!UICONTROL Ativar árvore]**.

No Caminho inicial, digite `/apps/social/commons` e selecione **[!UICONTROL Ativar]**.

![verify-content-template](assets/verify-content-template.png)

### Exibir resultados {#view-results}

Se você fizer logon na instância de publicação como administrador, por exemplo, https://localhost:4503/crx/de como administrador/administrador, poderá verificar se os componentes sobrepostos estão lá.

Se você fizer logout e fizer logon novamente como `aaron.mcdonald@mailinator.com/password` e, ao atualizar a página, você observará que o comentário publicado não é mais exibido com um avatar, em vez de um simples &quot;xxx&quot; ser exibido.

![create-template-component](assets/create-template-component.png)

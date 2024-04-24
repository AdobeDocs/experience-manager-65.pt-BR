---
title: Alterar a aparência (HBS)
description: Saiba como alterar a aparência (HBS) editando os scripts HBS.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Alterar a aparência (HBS) {#alter-the-appearance-hbs}

Agora que os componentes do sistema de comentários personalizado no diretório de aplicativos (/apps) estão em vigor, com um resourceSuperType fazendo referência ao sistema de comentários padrão e o Modelo/Exibição personalizado registrado, você pode editar a implementação.

Para uma demonstração simples, um recurso visual, o avatar mostrado do usuário conectado que publica um comentário, é removido.

>[!NOTE]
>
>Para usar a extensão, a instância do sistema de comentários em um site a ser afetado (/content) deve definir seu resourceType como o sistema de comentários personalizado.

## Modificar os scripts HBS {#modify-the-hbs-scripts}

Usar [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Abertura [/apps/custom/components/comments/comment/**comentário.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Comente a tag que inclui o avatar em uma postagem de comentário (~ linha 21):

     ```
       <!--
        <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
        -->
     ```

* Abertura [/apps/custom/components/comments/**comentários.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * Comente a tag que inclui o avatar na próxima entrada de comentário (~ linha 44):

     ```
       <!--
        <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
        -->
     ```

* Selecionar **Salvar tudo**

### Replicar aplicativo personalizado {#replicate-custom-app}

Após a modificação do aplicativo, é necessário replicar novamente o componente personalizado.

Uma maneira de fazer isso é:

* No menu principal

   * Selecionar **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**.
   * Selecionar **[!UICONTROL Ativar árvore]**.
   * Definir `Start Path` para `/apps/custom`.
   * Desmarcar **[!UICONTROL Somente modificados]**.
   * Selecionar **[!UICONTROL Ativar]** botão.

### Exibir comentário modificado na página de exemplo publicada {#view-modified-comment-on-published-sample-page}

[Continuar a experiência](/help/communities/extend-sample-page.md#publish-sample-page) na instância de publicação, ainda conectada como o mesmo usuário, agora é possível atualizar a página no ambiente de publicação para exibir a modificação para remover o avatar:

![view-modified-content](assets/view-modified-content.png)

### Exemplo de pacote de extensão de comentário {#sample-comment-extension-package}

Anexado está um pacote do aplicativo de comentários personalizados criado neste tutorial.

[Obter arquivo](assets/sample-comment-extension-6-1-fp3.zip)

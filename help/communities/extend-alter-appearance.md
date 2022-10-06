---
title: Alterar a aparência (HBS)
seo-title: Alter the Appearance
description: Modificar os scripts HBS
seo-description: Modify the HBS scripts
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Alterar a aparência (HBS) {#alter-the-appearance-hbs}

Agora que os componentes do sistema de comentários personalizado no diretório do aplicativo (/apps) estão em vigor, com um resourceSuperType referenciando o sistema de comentários padrão e o Modelo/Exibição personalizado registrado, é possível modificar a implementação.

Para uma demonstração simples, um recurso visual, o avatar mostrado do usuário conectado que publica um comentário, é removido.

>[!NOTE]
>
>Para usar a extensão, a instância do sistema de comentários em um site a ser afetado (/content) deve definir resourceType para ser o sistema de comentários personalizado.

## Modificar os scripts HBS {#modify-the-hbs-scripts}

Usando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Abrir [/apps/custom/components/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Comente a tag que inclui o avatar de uma postagem de comentário (~ linha 21):

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* Abrir [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * Comente a tag que inclui o avatar da próxima entrada de comentário (~ linha 44):

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

### Exibir Comentário Modificado na Página de Amostra Publicada {#view-modified-comment-on-published-sample-page}

[Continuar a experiência](/help/communities/extend-sample-page.md#publish-sample-page) na instância de publicação, ainda conectado como o mesmo usuário, agora é possível atualizar a página no ambiente de publicação para exibir a modificação e remover o avatar:

![view-modified-content](assets/view-modified-content.png)

### Pacote de extensão de comentário de amostra {#sample-comment-extension-package}

Anexado há um pacote de comentários personalizados criados neste tutorial.

[Obter arquivo](assets/sample-comment-extension-6-1-fp3.zip)

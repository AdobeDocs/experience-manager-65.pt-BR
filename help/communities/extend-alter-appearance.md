---
title: Alterar a aparência (HBS)
seo-title: Alterar a aparência
description: Modificar os scripts HBS
seo-description: Modificar os scripts HBS
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Alterar a aparência (HBS) {#alter-the-appearance-hbs}

Agora que os componentes do sistema de comentários personalizado no diretório do aplicativo (/apps) estão em vigor, com um resourceSuperType referenciando o sistema de comentários padrão e o Modelo/Visualização personalizado registrado, é possível modificar a implementação.

Para uma demonstração simples, um recurso visual, o avatar mostrado pelo usuário conectado que publica um comentário, é removido.

>[!NOTE]
>
>Para usar a extensão, a instância do sistema de comentários em um site a ser afetado (/content) deve definir resourceType como o sistema de comentários personalizado.

## Modificar os scripts HBS {#modify-the-hbs-scripts}

Usando o [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Abrir [/apps/custom/components/comments/**comment.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * comente a tag que inclui o avatar para uma postagem de comentário (~ linha 21):

      ```
      <!--
       <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
       -->
      ```

* Abrir [/apps/custom/components/comments/**comments.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * comente a tag que inclui o avatar para a próxima entrada de comentário (~ linha 44):

      ```
      <!--
       <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
       -->
      ```

* Selecione **Salvar tudo**

### Replicar aplicativo personalizado {#replicate-custom-app}

Após a modificação do aplicativo, é necessário rereplicar o componente personalizado.

Uma maneira de o fazer é

* No menu principal

   * selecione **Ferramentas > Operações > Replicação**
   * select `Activate Tree`
   * definido `Start Path`: to `/apps/custom`
   * deselect `Only Modified`
   * botão Selecionar `Activate`

### Página Comentário modificado da Visualização sobre amostra publicada {#view-modified-comment-on-published-sample-page}

[Continuando com a experiência](/help/communities/extend-sample-page.md#publish-sample-page) na instância de publicação, ainda conectado como o mesmo usuário, agora é possível atualizar a página no ambiente de publicação para visualização da modificação para remover o avatar:

![chlimage_1-136](assets/chlimage_1-136.png)

### Pacote de extensão de comentário de amostra {#sample-comment-extension-package}

Anexado é um pacote do aplicativo de comentários personalizado criado neste tutorial.

[Obter arquivo](assets/sample-comment-extension-6-1-fp3.zip)

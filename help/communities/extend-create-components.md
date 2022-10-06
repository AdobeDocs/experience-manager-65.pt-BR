---
title: Criar os componentes
seo-title: Create the Components
description: Criar o componente Comentários
seo-description: Create the Comments component
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 4%

---

# Criar os componentes  {#create-the-components}

O exemplo de extensão de componentes usa o sistema de comentários, que na verdade é composto por dois componentes

* Comentários - O sistema de comentários abrangente que é o componente colocado em uma página.
* Comentário - o componente que captura uma instância de um comentário publicado.

Ambos os componentes precisam ser implementados, especialmente se personalizar a aparência de um comentário publicado.

>[!NOTE]
>
>Somente um sistema de comentários por página do site é permitido.
>
>Muitos recursos das Comunidades já incluem um sistema de comentários cujo resourceType pode ser modificado para fazer referência ao sistema de comentários estendido.

## Criar o componente Comentários {#create-the-comments-component}

Essas instruções especificam um **Grupo** valor diferente de `.hidden` assim, o componente pode ser disponibilizado no navegador de componentes (sidekick).

A exclusão do arquivo JSP criado automaticamente ocorre porque o arquivo HBS padrão será usado.

1. Navegue até **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Crie um local para aplicativos personalizados:

   * Selecione o `/apps` nó

      * **Criar pasta** nomeado **[!UICONTROL custom]**
   * Selecione o `/apps/custom` nó

      * **Criar pasta** nomeado **[!UICONTROL componentes]**


1. Selecione o `/apps/custom/components` nó

   * **[!UICONTROL Criar > Componente...]**

      * **Rótulo**: *comentários*
      * **Título**: *Comentários Alt*
      * **Descrição**: *Estilo de comentários alternativos*
      * **Supertipo**: *social/commons/components/hbs/comments*
      * **Grupo**: *Personalizado*
   * Selecione **[!UICONTROL Próximo]**
   * Selecione **[!UICONTROL Próximo]**
   * Selecione **[!UICONTROL Próximo]**
   * Selecionar **[!UICONTROL OK]**


1. Expanda o nó recém-criado: `/apps/custom/components/comments`
1. Selecionar **[!UICONTROL Salvar tudo]**
1. Clique com o botão direito do mouse `comments.jsp`
1. Selecionar **[!UICONTROL Excluir]**
1. Selecionar **[!UICONTROL Salvar tudo]**

![criar-componente](assets/create-component.png)

### Criar o componente Comentário secundário {#create-the-child-comment-component}

Estas instruções foram definidas **Grupo** para `.hidden` como somente o componente principal deve ser incluído em uma página.

A exclusão do arquivo JSP criado automaticamente ocorre porque o arquivo HBS padrão será usado.

1. Navegue até o `/apps/custom/components/comments` nó
1. Clique com o botão direito do mouse no nó

   * Selecionar **[!UICONTROL Criar]** > **[!UICONTROL Componente...]**

      * **Rótulo**: *comentário*
      * **Título**: *Comentário alternativo*
      * **Descrição**: *Estilo de comentário alternativo*
      * **Supertipo**: *social/commons/components/hbs/comments/comment*
      * **Grupo**: `*.hidden*`
   * Selecione **[!UICONTROL Próximo]**
   * Selecione **[!UICONTROL Próximo]**
   * Selecione **[!UICONTROL Próximo]**
   * Selecionar **[!UICONTROL OK]**


1. Expanda o nó recém-criado: `/apps/custom/components/comments/comment`
1. Selecionar **[!UICONTROL Salvar tudo]**
1. Clique com o botão direito do mouse `comment.jsp`
1. Selecionar **[!UICONTROL Excluir]**
1. Selecionar **[!UICONTROL Salvar tudo]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Copiar e modificar os scripts HBS padrão {#copy-and-modify-the-default-hbs-scripts}

Usando [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Copiar `comments.hbs`

   * De [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * Para [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Editar `comments.hbs` para:

   * Altere o valor da variável `data-scf-component` atributo (~linha 20):

      * De `social/commons/components/hbs/comments`
      * Para `/apps/custom/components/comments`
   * Modifique para incluir o componente de comentário personalizado (~linha 75):

      * Substituir `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Com `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* Copiar `comment.hbs`

   * De [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * Para [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Editar `comment.hbs` para:

   * Alterar o valor do atributo data-scf-component (~ linha 19)

      * De `social/commons/components/hbs/comments/comment`
      * Para `/apps/custom/components/comments/comment`

* Selecionar `/apps/custom` nó
* Selecionar **[!UICONTROL Salvar tudo]**

## Criar uma pasta da biblioteca do cliente {#create-a-client-library-folder}

Para evitar a necessidade de incluir explicitamente essa biblioteca do cliente, o valor das categorias para a clientlib do sistema de comentários padrão pode ser usado ( `cq.social.author.hbs.comments`), mas essa clientlib também seria incluída para todas as instâncias do componente padrão.

Usando [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Selecionar `/apps/custom/components/comments` nó
* Selecionar **[!UICONTROL Criar nó]**

   * **Nome**: `clientlibs`
   * **Tipo**: `cq:ClientLibraryFolder`
   * Adicionar a **[!UICONTROL Propriedades]** guia :

      * **Nome** `categories` **Tipo** `String` **Valor** `cq.social.author.hbs.comments` `Multi`
      * **Nome** `dependencies` **Tipo** `String` **Valor** `cq.social.scf` `Multi`

* Selecionar **[!UICONTROL Salvar tudo]**
* Com `/apps/custom/components/comments/clientlib`No nó s selecionado, crie 3 arquivos:

   * **Nome**: `css.txt`
   * **Nome**: `js.txt`
   * **Nome**: customcommentsystem.js

* Insira &quot;customcommentsystem.js&quot; como o conteúdo de `js.txt`
* Selecionar **[!UICONTROL Salvar tudo]**

![comments-clientlibs](assets/comments-clientlibs.png)

## Registre o modelo e a visualização do SCF {#register-the-scf-model-view}

Ao estender (substituir) um componente do SCF, o resourceType é diferente (a sobreposição faz uso do mecanismo de pesquisa relativo que pesquisa por `/apps` before `/libs` para que o resourceType permaneça o mesmo). É por isso que é necessário gravar o JavaScript (na biblioteca do cliente) para registrar o modelo JS SCF e visualizar o resourceType personalizado.

Insira o seguinte texto como o conteúdo de `customcommentsystem.js`:

### customcommentsystem.js {#customcommentsystem-js}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";

    var CustomComment = SCF.Components["social/commons/components/hbs/comments/comment"].Model;
    var CustomCommentView = SCF.Components["social/commons/components/hbs/comments/comment"].View;

    var CustomCommentSystem = SCF.Components["social/commons/components/hbs/comments"].Model;
    var CustomCommentSystemView = SCF.Components["social/commons/components/hbs/comments"].View;

    SCF.registerComponent('/apps/custom/components/comments/comment', CustomComment, CustomCommentView);
    SCF.registerComponent('/apps/custom/components/comments', CustomCommentSystem, CustomCommentSystemView);

})($CQ, _, Backbone, SCF);
```

* Selecionar **[!UICONTROL Salvar tudo]**

## Publicar o aplicativo {#publish-the-app}

Para experimentar o componente estendido no ambiente de publicação, é necessário replicar o componente personalizado.

Uma maneira de fazer isso é:

* Da navegação global,

   * Selecionar **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]**
   * Selecionar **[!UICONTROL Ativar árvore]**
   * Definir `Start Path` para `/apps/custom`
   * Desmarcar **[!UICONTROL Somente modificados]**
   * Selecionar **[!UICONTROL Ativar]** botão

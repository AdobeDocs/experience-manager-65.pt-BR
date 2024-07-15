---
title: Criar os componentes
description: Saiba como estender componentes usando o sistema de comentários composto por componentes Comentários e Comentários.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Criar os componentes  {#create-the-components}

O exemplo de extensão de componentes usa o sistema de comentários, que é composto por dois componentes.

* Comentários - o sistema de comentários abrangente que é o componente colocado em uma página.
* Comentário - O componente que captura uma instância de um comentário publicado.

Ambos os componentes devem ser implementados, especialmente se você personalizar a aparência de um comentário publicado.

>[!NOTE]
>
>Somente um sistema de comentários por página do site é permitido.
>
>Muitos recursos das Comunidades já incluem um sistema de comentários cujo resourceType pode ser modificado para fazer referência ao sistema de comentários estendidos.

## Criar o componente de Comentários {#create-the-comments-component}

Estas direções especificam um valor de **Grupo** diferente de `.hidden`, portanto, o componente pode ser disponibilizado pelo navegador de componentes (sidekick).

A exclusão do arquivo JSP criado automaticamente ocorre porque o arquivo HBS padrão é usado em seu lugar.

1. Navegue até **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Criar um local para aplicativos personalizados:

   * Selecionar o nó `/apps`

      * **Criar pasta** chamada **[!UICONTROL personalizada]**

   * Selecionar o nó `/apps/custom`

      * **Criar pasta** chamada **[!UICONTROL componentes]**

1. Selecionar o nó `/apps/custom/components`

   * **[!UICONTROL Criar > Componente...]**

      * **Rótulo**: *comentários*
      * **Título**: *Comentários Alternativos*
      * **Descrição**: *Estilo de comentários alternativos*
      * **Supertipo**: *social/commons/components/hbs/comments*
      * **Grupo**: *Personalizado*

   * Selecionar **[!UICONTROL Próximo]**
   * Selecionar **[!UICONTROL Próximo]**
   * Selecionar **[!UICONTROL Próximo]**
   * Selecione **[!UICONTROL OK]**

1. Expanda o nó criado: `/apps/custom/components/comments`
1. Selecione **[!UICONTROL Salvar tudo]**
1. Clique com o botão direito do mouse em `comments.jsp`
1. Selecionar **[!UICONTROL Excluir]**
1. Selecione **[!UICONTROL Salvar tudo]**

![criar-componente](assets/create-component.png)

### Criar o componente de Comentário secundário {#create-the-child-comment-component}

Estas direções definem **Grupo** como `.hidden`, pois somente o componente principal deve ser incluído em uma página.

A exclusão do arquivo JSP criado automaticamente ocorre porque o arquivo HBS padrão é usado em seu lugar.

1. Navegue até o nó `/apps/custom/components/comments`
1. Clique com o botão direito do mouse no nó

   * Selecione **[!UICONTROL Criar]** > **[!UICONTROL Componente...]**

      * **Rótulo**: *comentário*
      * **Título**: *Comentário Alternativo*
      * **Descrição**: *Estilo de comentário alternativo*
      * **Supertipo**: *social/commons/components/hbs/comments/comment*
      * **Grupo**: `*.hidden*`

   * Selecionar **[!UICONTROL Próximo]**
   * Selecionar **[!UICONTROL Próximo]**
   * Selecionar **[!UICONTROL Próximo]**
   * Selecione **[!UICONTROL OK]**

1. Expanda o nó criado: `/apps/custom/components/comments/comment`
1. Selecione **[!UICONTROL Salvar tudo]**
1. Clique com o botão direito do mouse em `comment.jsp`
1. Selecionar **[!UICONTROL Excluir]**
1. Selecione **[!UICONTROL Salvar tudo]**

![criar-componente-filho](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Copiar e modificar os scripts HBS padrão {#copy-and-modify-the-default-hbs-scripts}

Usando [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Copiar `comments.hbs`

   * De [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * Para [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Editar `comments.hbs` para:

   * Alterar o valor do atributo `data-scf-component` (linha~20):

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

* Selecionar nó `/apps/custom`
* Selecione **[!UICONTROL Salvar tudo]**

## Criar uma pasta da biblioteca do cliente {#create-a-client-library-folder}

Para evitar a necessidade de incluir essa biblioteca do cliente, o valor das categorias para a clientlib do sistema de comentários padrão pode ser usado ( `cq.social.author.hbs.comments`). No entanto, essa clientlib também teria que ser incluída para todas as instâncias do componente padrão.

Usando [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Selecionar nó `/apps/custom/components/comments`
* Selecionar **[!UICONTROL Criar Nó]**

   * **Nome**: `clientlibs`
   * **Tipo**: `cq:ClientLibraryFolder`
   * Adicionar à guia **[!UICONTROL Propriedades]**:

      * **Nome** `categories` **Tipo** `String` **Valor** `cq.social.author.hbs.comments` `Multi`
      * **Nome** `dependencies` **Tipo** `String` **Valor** `cq.social.scf` `Multi`

* Selecione **[!UICONTROL Salvar tudo]**
* Com o nó `/apps/custom/components/comments/clientlib`s selecionado, crie três arquivos:

   * **Nome**: `css.txt`
   * **Nome**: `js.txt`
   * **Nome**: customcommentsystem.js

* Inserir &#39;customcommentsystem.js&#39; como conteúdo de `js.txt`
* Selecione **[!UICONTROL Salvar tudo]**

![comentários-clientlibs](assets/comments-clientlibs.png)

## Registrar o modelo e a visualização do SCF {#register-the-scf-model-view}

Ao estender (substituir) um componente SCF, o resourceType é diferente (a sobreposição usa o mecanismo de pesquisa relativo que pesquisa `/apps` antes de `/libs` para que o resourceType permaneça o mesmo). É por isso que é necessário escrever o JavaScript (na biblioteca do cliente) para registrar o modelo JS SCF e visualizar o resourceType personalizado.

Digite o seguinte texto como conteúdo de `customcommentsystem.js`:

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

* Selecione **[!UICONTROL Salvar tudo]**

## Publish o aplicativo {#publish-the-app}

Para experimentar o componente estendido no ambiente de publicação, é necessário replicar o componente personalizado.

Uma maneira de fazer isso é:

* Na navegação global,

   * Selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]**
   * Selecionar **[!UICONTROL Ativar árvore]**
   * Configurar `Start Path` para `/apps/custom`
   * Desmarcar **[!UICONTROL Somente modificados]**
   * Selecionar o botão **[!UICONTROL Ativar]**

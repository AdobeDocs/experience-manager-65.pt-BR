---
title: Criar nós
seo-title: Criar nós
description: Sobrepor o sistema de comentários
seo-description: Sobrepor o sistema de comentários
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 8%

---


# Criar nós {#create-nodes}

Sobreponha o sistema de comentários com uma versão personalizada copiando o número mínimo de arquivos necessários de `/libs` para `/apps` e modificando-os em `/apps`.

>[!CAUTION]
>
>O conteúdo da pasta /libs nunca é editado porque qualquer reinstalação ou atualização pode excluir ou substituir a pasta /libs enquanto o conteúdo da pasta /apps é deixado inalterado.

Usando [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) em uma instância do autor, comece criando um caminho na pasta /apps que é idêntico ao caminho para os componentes sobrepostos na pasta /libs.

O caminho que está sendo duplicado é:

* `/libs/social/commons/components/hbs/comments/comment`

Alguns nós no caminho são pastas e alguns são componentes.

1. Navegue até [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Criar `/apps/social` (se ainda não existir)
   * Selecionar `/apps` nó
   * **[!UICONTROL Criar > Pasta ...]**
      * Digite o nome: `social`
1. Selecionar `social` nó
   * **[!UICONTROL Criar]** >  **[!UICONTROL Pasta...]**
      * Digite o nome: `commons`
1. Selecionar `commons` nó
   * **[!UICONTROL Criar > Pasta...]**
      * Digite o nome: `components`
1. Selecionar `components` nó
   * **[!UICONTROL Criar > Pasta..]**.
      * Digite o nome: `hbs`
1. Selecionar `hbs` nó
   * **[!UICONTROL Criar]** >  **[!UICONTROL Criar componente...]**
      * Digite o rótulo: `comments`
      * Inserir Título: `Comments`
      * Digite a descrição: `List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * Inserir grupo: `Communities`
      * Clique em **[!UICONTROL Próximo]** até **[!UICONTROL OK]**
1. Selecionar `comments` nó

   * **[!UICONTROL Criar]** >  **[!UICONTROL Criar componente...]**

      * Digite o rótulo: `comment`
      * Inserir Título: `Comment`
      * Digite a descrição: `A comment instance without avatars`
      * Supertipo: `social/commons/components/comments/comment`
      * Inserir grupo: `.hidden`
      * Clique em **[!UICONTROL Próximo]** até **[!UICONTROL OK]**
   * Selecione **[!UICONTROL Salvar tudo]**
1. Excluir o padrão `comments.jsp`
   * Selecionar nó `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Selecione **[!UICONTROL Eliminar]**
1. Exclua o arquivo comment.jsp padrão
   * selecionar nó `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Selecione **[!UICONTROL Eliminar]**
   * Selecione **[!UICONTROL Salvar tudo]**

>[!NOTE]
>
>Para preservar a cadeia de herança, `Super Type` (propriedade `sling:resourceSuperType`) dos componentes de sobreposição são definidos com o mesmo valor de `Super Type` dos componentes que estão sendo sobrepostos, neste caso:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


A própria sobreposição `Type`(propriedade `sling:resourceType`) deve ser uma referência automática relativa para que qualquer conteúdo não encontrado em /apps seja procurado em /libs.
* Nome: `sling:resourceType`
* Tipo: `String`
* Valor: `social/commons/components/hbs/comments`

1. Selecione a cor verde `[+] Add`
   * Nome: `sling:resourceType`
   * Tipo: `String`
   * Valor: `social/commons/components/hbs/comments/comment`
1. Selecione a cor verde `[+] Add`
   * Selecione **[!UICONTROL Salvar tudo]**

![create-nodes](assets/create-nodes.png)


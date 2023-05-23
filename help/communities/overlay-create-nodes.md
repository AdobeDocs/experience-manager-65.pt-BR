---
title: Criar nós
seo-title: Create Nodes
description: Sobrepor o sistema de comentários
seo-description: Overlay the comments system
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 11%

---

# Criar nós {#create-nodes}

Sobreponha o sistema de comentários a uma versão personalizada copiando o número mínimo de arquivos necessários do `/libs` em `/apps` e modificá-los em `/apps`.

>[!CAUTION]
>
>O conteúdo da pasta /libs nunca é editado porque qualquer reinstalação ou atualização pode excluir ou substituir a pasta /libs enquanto o conteúdo da pasta /apps não for tocado.

Usar [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) em uma instância do autor, comece criando um caminho na pasta /apps que seja idêntico ao caminho para os componentes sobrepostos na pasta /libs.

O caminho sendo duplicado é:

* `/libs/social/commons/components/hbs/comments/comment`

Alguns nós no caminho são pastas e alguns são componentes.

1. Navegue até [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Criar `/apps/social` (se ainda não existir)
   * Selecionar `/apps` nó
   * **[!UICONTROL Criar > Pasta ...]**
      * Digite o nome: `social`
1. Selecionar `social` nó
   * **[!UICONTROL Criar]** > **[!UICONTROL Pasta...]**
      * Digite o nome: `commons`
1. Selecionar `commons` nó
   * **[!UICONTROL Criar > Pasta...]**
      * Digite o nome: `components`
1. Selecionar `components` nó
   * **[!UICONTROL Criar > Pasta..]**.
      * Digite o nome: `hbs`
1. Selecionar `hbs` nó
   * **[!UICONTROL Criar]** > **[!UICONTROL Criar componente...]**
      * Inserir rótulo: `comments`
      * Insira o título: `Comments`
      * Inserir descrição: `List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * Inserir grupo: `Communities`
      * Clique em **[!UICONTROL Próxima]** até **[!UICONTROL OK]**
1. Selecionar `comments` nó

   * **[!UICONTROL Criar]** > **[!UICONTROL Criar componente...]**

      * Inserir rótulo: `comment`
      * Insira o título: `Comment`
      * Inserir descrição: `A comment instance without avatars`
      * Super Type: `social/commons/components/comments/comment`
      * Inserir grupo: `.hidden`
      * Clique em **[!UICONTROL Próxima]** até **[!UICONTROL OK]**
   * Selecionar **[!UICONTROL Salvar tudo]**
1. Excluir o padrão `comments.jsp`
   * Selecionar nó `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Selecione **[!UICONTROL Excluir]**
1. Excluir o comment.jsp padrão
   * selecionar nó `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Selecione **[!UICONTROL Excluir]**
   * Selecionar **[!UICONTROL Salvar tudo]**

>[!NOTE]
>
>A fim de preservar a cadeia de herança, a `Super Type` (propriedade) `sling:resourceSuperType`) dos componentes de sobreposição são definidos com o mesmo valor da variável `Super Type` dos componentes que estão sendo sobrepostos, neste caso:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


A própria sobreposição `Type`(propriedade) `sling:resourceType`) deve ser uma autorreferência relativa para que qualquer conteúdo não encontrado em /apps seja procurado em /libs.
* Nome: `sling:resourceType`
* Tipo: `String`
* Valor: `social/commons/components/hbs/comments`

1. Selecione o verde `[+] Add`
   * Nome: `sling:resourceType`
   * Tipo: `String`
   * Valor: `social/commons/components/hbs/comments/comment`
1. Selecione o verde `[+] Add`
   * Selecionar **[!UICONTROL Salvar tudo]**

![create-nodes](assets/create-nodes.png)

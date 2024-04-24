---
title: Criar nós
description: Saiba como sobrepor o sistema de comentários a uma versão personalizada copiando o número mínimo de arquivos necessários de /libs e editando-os em /apps.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

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
   * **[!UICONTROL Criar > Pasta]**
      * Digite o nome: `social`
1. Selecionar `social` nó
   * **[!UICONTROL Criar]** > **[!UICONTROL Pasta]**
      * Digite o nome: `commons`
1. Selecionar `commons` nó
   * **[!UICONTROL Criar > Pasta]**
      * Digite o nome: `components`
1. Selecionar `components` nó
   * **[!UICONTROL Criar > Pasta]**.
      * Digite o nome: `hbs`
1. Selecionar `hbs` nó
   * **[!UICONTROL Criar]** > **[!UICONTROL Criar componente]**
      * Inserir rótulo: `comments`
      * Insira o título: `Comments`
      * Insira a descrição: `List of comments without showing avatars`
      * Supertipo: `social/commons/components/comments`
      * Inserir grupo: `Communities`
      * Clique em **[!UICONTROL Próxima]** até **[!UICONTROL OK]**
1. Selecionar `comments` nó

   * **[!UICONTROL Criar]** > **[!UICONTROL Criar componente]**

      * Inserir rótulo: `comment`
      * Insira o título: `Comment`
      * Insira a descrição: `A comment instance without avatars`
      * Supertipo: `social/commons/components/comments/comment`
      * Inserir grupo: `.hidden`
      * Clique em **[!UICONTROL Próxima]** até **[!UICONTROL OK]**
   * Selecionar **[!UICONTROL Salvar tudo]**
1. Excluir o padrão `comments.jsp`
   * Selecionar nó `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Selecionar **[!UICONTROL Excluir]**
1. Excluir o comment.jsp padrão
   * selecionar nó `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Selecionar **[!UICONTROL Excluir]**
   * Selecionar **[!UICONTROL Salvar tudo]**

>[!NOTE]
>
>Para preservar a cadeia de herança, a variável `Super Type` (propriedade) `sling:resourceSuperType`) dos componentes de sobreposição são definidos com o mesmo valor da variável `Super Type` dos componentes que estão sendo sobrepostos, neste caso:
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

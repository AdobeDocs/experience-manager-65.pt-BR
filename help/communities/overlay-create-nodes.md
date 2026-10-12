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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%
---
# Criar nós {#create-nodes}

Sobreponha o sistema de comentários com uma versão personalizada copiando o número mínimo de arquivos necessários de `/libs` para `/apps` e modificando-os em `/apps`.

>[!CAUTION]
>
>O conteúdo da pasta /libs nunca é editado porque qualquer reinstalação ou atualização pode excluir ou substituir a pasta /libs enquanto o conteúdo da pasta /apps não for tocado.

Usando o [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) em uma instância de autor, comece criando um caminho na pasta /apps que seja idêntico ao caminho para os componentes sobrepostos na pasta /libs.

O caminho sendo duplicado é:

* `/libs/social/commons/components/hbs/comments/comment`

Alguns nós no caminho são pastas e alguns são componentes.

1. Navegue até [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Criar `/apps/social` (se ainda não existir)
   * Selecionar nó `/apps`
   * **[!UICONTROL Criar > Pasta]**
     * Inserir Nome: `social`
1. Selecionar nó `social`
   * **[!UICONTROL Criar]** > **[!UICONTROL Pasta]**
     * Inserir Nome: `commons`
1. Selecionar nó `commons`
   * **[!UICONTROL Criar > Pasta]**
     * Inserir Nome: `components`
1. Selecionar nó `components`
   * **[!UICONTROL Criar > Pasta]**.
     * Inserir Nome: `hbs`
1. Selecionar nó `hbs`
   * **[!UICONTROL Criar]** > **[!UICONTROL Criar Componente]**
     * Inserir Rótulo: `comments`
     * Digite o título: `Comments`
     * Inserir Descrição: `List of comments without showing avatars`
     * Supertipo: `social/commons/components/comments`
     * Inserir Grupo: `Communities`
     * Clique em **[!UICONTROL Avançar]** até **[!UICONTROL OK]**
1. Selecionar nó `comments`

   * **[!UICONTROL Criar]** > **[!UICONTROL Criar Componente]**

     * Inserir Rótulo: `comment`
     * Digite o título: `Comment`
     * Inserir Descrição: `A comment instance without avatars`
     * Supertipo: `social/commons/components/comments/comment`
     * Inserir Grupo: `.hidden`
     * Clique em **[!UICONTROL Avançar]** até **[!UICONTROL OK]**
   * Selecione **[!UICONTROL Salvar tudo]**
1. Excluir o padrão `comments.jsp`
   * Selecionar nó `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Selecionar **[!UICONTROL Excluir]**
1. Excluir o comment.jsp padrão
   * selecionar nó `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Selecionar **[!UICONTROL Excluir]**
   * Selecione **[!UICONTROL Salvar tudo]**

>[!NOTE]
>
>Para preservar a cadeia de herança, a `Super Type` (propriedade `sling:resourceSuperType`) dos componentes de sobreposição é definida com o mesmo valor que `Super Type` dos componentes que estão sendo sobrepostos, neste caso:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

A própria sobreposição `Type`(propriedade `sling:resourceType`) deve ser uma autorreferência relativa para que qualquer conteúdo não encontrado em /apps seja procurado em /libs.
* Nome: `sling:resourceType`
* Tipo: `String`
* Valor: `social/commons/components/hbs/comments`

1. Selecione o `[+] Add` verde
   * Nome: `sling:resourceType`
   * Tipo: `String`
   * Valor: `social/commons/components/hbs/comments/comment`
1. Selecione o `[+] Add` verde
   * Selecione **[!UICONTROL Salvar tudo]**

![criar-nós](assets/create-nodes.png)

---
title: Clientlibs para componentes das comunidades
description: Saiba como adicionar bibliotecas do lado do cliente (clientlibs) a uma página para que você possa coletar detalhes de uso e usar ferramentas de depuração para componentes do Communities.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Clientlibs para componentes das comunidades {#clientlibs-for-communities-components}

## Introdução {#introduction}

Esta seção da documentação descreve como adicionar bibliotecas do lado do cliente (clientlibs) a uma página para componentes de Comunidades.

Para obter informações básicas, consulte o seguinte:

* [Usando Bibliotecas do Lado do Cliente](/help/sites-developing/clientlibs.md) que fornece detalhes de uso e ferramentas de depuração
* [Clientlibs para SCF](/help/communities/client-customize.md#clientlibs) que fornece informações úteis ao personalizar componentes SCF


## Por que as bibliotecas de clientes são necessárias {#why-clientlibs-are-required}

As bibliotecas de clientes são necessárias para o funcionamento adequado (JavaScript) e o estilo (CSS) de um componente.

Quando existe uma [função de comunidade](/help/communities/functions.md) para um recurso, todos os componentes e configurações necessários, incluindo as clientlibs necessárias, estão presentes no site da comunidade. Somente se os componentes adicionais estiverem disponíveis para os autores, é necessário adicionar mais clientlibs.

Quando as clientlibs necessárias estiverem ausentes, [adicionar um componente de Comunidades a uma página](/help/communities/author-communities.md) poderá resultar em erros de JavaScript e em uma aparência inesperada.

### Exemplo: análises colocadas sem clientlibs {#example-placed-reviews-without-clientlibs}

![avaliações_colocadas](assets/placed-reviews.png)

### Exemplo: Análises Feitas com Clientlibs {#example-placed-reviews-with-clientlibs}

![comentários-clientlibs](assets/reviews-clientlibs.png)

## Identificação das clientlibs necessárias {#identifying-required-clientlibs}

As informações essenciais do recurso para desenvolvedores identificam as clientlibs necessárias.

Além disso, a partir de uma instância do AEM, navegar até o [Guia de Componentes da Comunidade](/help/communities/components-guide.md) fornece acesso a uma lista de categorias de clientlib necessárias para um componente.

Por exemplo, na parte superior da [página Análises](https://localhost:4502/content/community-components/en/reviews.html), as bibliotecas de clientes necessárias listadas são

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-comentários](assets/clientlibs-reviews.png)

## Adicionar Clientlibs Necessárias {#adding-required-clientlibs}

Quando quiser adicionar um componente Comunidades a uma página, será necessário adicionar as clientlibs necessárias para o componente, se ainda não estiver presente.

Use o [CRXDE|Lite](#using-crxde-lite) para modificar uma clientlibslist existente para uma página de site da comunidade.

Para adicionar um clientlib para um site da comunidade usando o [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Navegue até [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Localize o nó `clientlibslist` da página em que você deseja adicionar o componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Com o nó `clientlibslist` selecionado:

   * Localize a propriedade `scg:requiredClientLibs` da Cadeia de Caracteres [].
   * Selecione seu `Value` para poder acessar a caixa de diálogo Matriz de cadeia de caracteres.

      * Role para baixo, se necessário.
      * Selecione + para inserir uma nova biblioteca do cliente.

         * Repita para adicionar mais bibliotecas de clientes.

         * Selecione **OK**.

   * Selecione **Salvar tudo**.

>[!NOTE]
>
>Se o site não for um site da comunidade, a existência ou o local das bibliotecas de clientes em uso para o site devem ser descobertos.

Usando o exemplo de [Introdução ao AEM Communities](/help/communities/getting-started.md), em que `site-name` é *engajamento*, esta é a forma como a clientliblist aparecerá se o componente de revisões for adicionado:

![componente de revisão](assets/review-component.png)

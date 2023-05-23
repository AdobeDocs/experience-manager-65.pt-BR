---
title: Clientlibs para componentes das comunidades
seo-title: Clientlibs for Communities Components
description: Bibliotecas do lado do cliente para comunidades
seo-description: Client-side libraries for Communities
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Clientlibs para componentes das comunidades {#clientlibs-for-communities-components}

## Introdução {#introduction}

Esta seção da documentação descreve como adicionar bibliotecas do lado do cliente (clientlibs) a uma página para componentes de Comunidades.

Para informações básicas, visite:

* [Uso de bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md) que fornece detalhes de uso e ferramentas de depuração
* [Clientlibs para SCF](/help/communities/client-customize.md#clientlibs) que fornece informações úteis ao personalizar componentes SCF


## Por que as bibliotecas de clientes são necessárias {#why-clientlibs-are-required}

As bibliotecas de clientes são necessárias para o funcionamento adequado (JavaScript) e o estilo (CSS) de um componente.

Quando existe uma [função da comunidade](/help/communities/functions.md) para um recurso, todos os componentes e configurações necessários, incluindo as clientlibs necessárias, estarão presentes no site da comunidade. Somente se os componentes adicionais estiverem disponíveis para os autores, as bibliotecas de clientes adicionais precisarão ser adicionadas.

Quando as clientlibs necessárias estiverem ausentes, [adição de um componente Comunidades a uma página](/help/communities/author-communities.md) pode resultar em erros de javascript, bem como em uma aparência inesperada.

### Exemplo: análises colocadas sem clientlibs {#example-placed-reviews-without-clientlibs}

![places-review](assets/placed-reviews.png)

### Exemplo: Análises Feitas com Clientlibs {#example-placed-reviews-with-clientlibs}

![review-clientlibs](assets/reviews-clientlibs.png)

## Identificação das clientlibs necessárias {#identifying-required-clientlibs}

As informações essenciais do recurso para desenvolvedores identificam as clientlibs necessárias.

Além disso, em uma instância do AEM, navegar até o [Guia de componentes da comunidade](/help/communities/components-guide.md) O fornece acesso a uma lista de categorias clientlib necessárias para um componente.

Por exemplo, na parte superior do [Página de análises](https://localhost:4502/content/community-components/en/reviews.html) as clientlibs necessárias listadas são

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Adicionar Clientlibs Necessárias {#adding-required-clientlibs}

Quando quiser adicionar um componente Comunidades a uma página, será necessário adicionar as clientlibs necessárias para o componente, se ainda não estiver presente.

Uso [CRXDE|Lite](#using-crxde-lite) para modificar uma clientlibslist existente para uma página de site da comunidade.

Para adicionar uma clientlib para um site da comunidade usando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Navegue até [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Localize o `clientlibslist` para a página em que deseja adicionar o componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Com `clientlibslist` nó selecionado:

   * Localize a string[] propriedade `scg:requiredClientLibs`.
   * Selecionar sua `Value` para acessar a caixa de diálogo Matriz de string.

      * Role para baixo, se necessário.
      * Selecione + para inserir uma nova biblioteca do cliente.

         * Repita para adicionar mais bibliotecas de clientes.

         * Selecionar **OK**.
   * Selecionar **Salvar tudo**.


>[!NOTE]
>
>Se o site não for um site da comunidade, a existência ou o local das bibliotecas de clientes em uso para o site precisará ser descoberto.

Usar o [Introdução ao AEM Communities](/help/communities/getting-started.md) exemplo, onde `site-name` é *engajar*, é assim que a clientliblist apareceria se adicionasse o componente de revisões:

![componente de revisão](assets/review-component.png)

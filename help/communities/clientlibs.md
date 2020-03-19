---
title: Clientlibs para componentes de comunidades
seo-title: Clientlibs para componentes de comunidades
description: Bibliotecas do cliente para Comunidades
seo-description: Bibliotecas do cliente para Comunidades
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
translation-type: tm+mt
source-git-commit: 5b8b1544645465d10e7c2018364b6a74f1ad9a8e

---


# Clientlibs para componentes de comunidades {#clientlibs-for-communities-components}

## Introdução {#introduction}

Esta seção da documentação descreve como adicionar bibliotecas do lado do cliente (clientlibs) a uma página para componentes do Communities.

Para obter informações básicas, visite :

* [Usar bibliotecas](/help/sites-developing/clientlibs.md) do lado do cliente que fornecem detalhes de uso e ferramentas de depuração
* [Clientlibs para SCF](/help/communities/client-customize.md#clientlibs) , que fornece informações úteis ao personalizar componentes SCF
* [Blog : Bibliotecas do cliente AEM explicadas por exemplo](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Por que os clientlibs são obrigatórios {#why-clientlibs-are-required}

Clientlibs são necessários para o funcionamento correto (JavaScript) e o estilo (CSS) de um componente.

Quando houver uma função [da](/help/communities/functions.md) comunidade para um recurso, todos os componentes e configurações necessários, incluindo os clientlibs necessários, estarão presentes no site da comunidade. Somente se componentes adicionais estiverem disponíveis para os autores precisariam ser adicionados clientlibs adicionais.

Quando faltam os clientlibs necessários, [adicionar um componente Comunidades a uma página](/help/communities/author-communities.md) pode resultar em erros de javascript, bem como em uma aparência inesperada.

### Exemplo: Revisões feitas sem Clientlibs {#example-placed-reviews-without-clientlibs}

![chlimage_1-132](assets/chlimage_1-132.png)

### Exemplo: Revisões feitas com Clientlibs {#example-placed-reviews-with-clientlibs}

![chlimage_1-133](assets/chlimage_1-133.png)

## Como identificar clientlibs obrigatórios {#identifying-required-clientlibs}

As informações de recursos essenciais para desenvolvedores identificam os clientlibs necessários.

Além disso, de uma instância do AEM, navegar até o Guia [de componentes da](/help/communities/components-guide.md) comunidade fornece acesso a uma lista de categorias clientlib necessárias para um componente.

Por exemplo, na parte superior da página [](https://localhost:4502/content/community-components/en/reviews.html) Revisões, os clientlibs necessários listados são

* cq.ckeditor
* cq.social.hbs.views

![chlimage_1-134](assets/chlimage_1-134.png)

## Adicionando Clientlibs Obrigatórios {#adding-required-clientlibs}

Quando for desejado adicionar um componente Comunidades a uma página, será necessário adicionar os clientlibs necessários para o componente, caso ainda não estejam presentes.

Use [CRXDE|Lite](#using-crxde-lite) para modificar uma lista de clientlibslist existente para uma página do site da comunidade.

Para adicionar uma clientlib para um site da comunidade usando o [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Navegue até [https://&lt;servidor>:&lt;porta>/crx/de](https://localhost:4502/crx/de)
* Localize o `clientlibslist` nó da página na qual você deseja adicionar o componente

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Com o `clientlibslist` nó selecionado

   * Localizar a propriedade String[]`scg:requiredClientLibs`
   * Selecione sua opção `Value` para acessar a caixa de diálogo String

      * Role para baixo se necessário
      * Selecione + para inserir uma nova biblioteca de cliente

         * Repita o procedimento para adicionar mais bibliotecas de clientes
      * Selecionar **OK**
   * Selecione **Salvar tudo**



>[!NOTE]
>
>Se o site não for um site da comunidade, a existência ou o local das bibliotecas clientes em uso para o site precisará ser descoberto.

Usando o exemplo [Introdução ao AEM Communities](/help/communities/getting-started.md) , onde `site-name` há *envolvimento*, esta é a forma como a clientliblist aparecerá se você adicionar o componente de revisões :

![chlimage_1-135](assets/chlimage_1-135.png)


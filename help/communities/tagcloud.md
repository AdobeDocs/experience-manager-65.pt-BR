---
title: Uso da Social Tag Cloud
seo-title: Using Social Tag Cloud
description: Adicionar um componente da Social Tag Cloud a uma página
seo-description: Adding a Social Tag Cloud component to a page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 5%

---

# Uso da Social Tag Cloud {#using-social-tag-cloud}

## Introdução {#introduction}

A variável `Social Tag Cloud` o componente destaca as tags aplicadas pelos membros da comunidade ao publicar conteúdo. É um meio de identificar tópicos de tendência e permitir que os visitantes do site localizem rapidamente o conteúdo marcado.

Para outros meios de identificar tendências atuais, visite [Tendências da atividade](trends.md).

Esta página documenta a `Social Tag Cloud` configurações da caixa de diálogo do componente e descreve a experiência do usuário.

Para obter informações detalhadas para desenvolvedores, consulte [Fundamentos de tags](tag.md).

Consulte [Administração de tags](../../help/sites-administering/tags.md) para obter informações sobre como criar e gerenciar tags e sobre quais tags de conteúdo foram aplicadas.

## Adicionar uma nuvem de tag social {#adding-a-social-tag-cloud}

Para adicionar um `Social Tag Cloud` para uma página no modo de autor, use o navegador de componentes para localizar `Communities / Social Tag Cloud` e arraste-a para o local em uma página onde a nuvem de tags deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](tag.md#essentials-for-client-side) são incluídos, é assim que a variável `Social Tag Cloud` componente aparecerá:

![social-tag](assets/social-tag.png)

## Configuração da Social Tag Cloud {#configuring-social-tag-cloud}

Selecione o colocado `Social Tag Cloud` para acessar e selecionar a variável `Configure` ícone que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

No **[!UICONTROL Tags em nuvem do Social]** especifique quais tags serão exibidas e, se as tags forem links ativos, o local da página para os resultados da pesquisa:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Tags do Social a serem exibidas]**
Identifique quais tags UGC serão exibidas. As opções suspensas são:

   * `From page and child pages`
   * `All tags`

  O padrão é `From page and child pages`, onde &quot;página&quot; se refere à **Página** abaixo.

* **[!UICONTROL Página]**

  (Obrigatório se não for `All tags)` O caminho para o UGC de uma página. O padrão é a página atual, se deixada em branco.

* **[!UICONTROL Não há links nas tags]**

  Se marcadas, as tags serão exibidas na nuvem de tags como texto simples. Se desmarcada, as tags são exibidas como links ativos que pesquisam em todo o conteúdo ao qual essa tag é aplicada. O padrão está desmarcado e requer o **[!UICONTROL Caminho do resultado da pesquisa]** a definir.

* **[!UICONTROL Pesquisar caminho de resultados]**

  O caminho para uma página na qual um `Search Result` componente foi colocado, configurado para fazer referência a UGC que inclui o caminho UGC especificado pelo **Página** configuração.

## Alterar exibição da Tags em nuvem do Social {#change-display-of-social-tag-cloud}

Para editar a exibição do **Tags em nuvem do Social**, insira [Modo Design](../../help/sites-authoring/default-components-designmode.md) e clique duas vezes no local `Social Tag Cloud` para abrir uma caixa de diálogo com uma guia adicional.

Usar o **[!UICONTROL Tags em nuvem do Social (Design)]** especifique como as tags são exibidas. Uma tag pode ser uma tag simples, uma única palavra no namespace padrão ou uma taxonomia hierárquica:

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Mostrar caminhos completos do título]**

  Se marcado, mostra os títulos das tags principais e o namespace de cada tag aplicada.

  Por exemplo:

   * Marcado: `Geometrixx Media: Gadgets / Cars`
   * Desmarcado: `Cars`

  Não há diferença para uma tag simples.

  O padrão está desmarcado.

* **[!UICONTROL Mostrar apenas tags de folha]**

  Se marcado, mostra somente as tags aplicadas que não contêm outras tags.

  Por exemplo, considerando a TagID de:

  `Geometrixx Media: Gadgets / Cars`

  Há 3 tags que podem ser aplicadas:

  `Geometrixx Media (the namespace)`, `Gadgets`, e `Cars`

   * Marcado: somente `Cars` será exibida, se aplicada.
   * Desmarcado: `Geometrixx Media` e `Gadgets`bem como `Cars` será exibida, se aplicada.

  Uma tag simples é uma tag folha.

  O padrão está desmarcado.

* **[!UICONTROL Modelo do link]**

  Um modelo, diferente de um padrão, usado para exibir os links em uma nuvem de tags, quando os links são ativados por meio da caixa de diálogo de edição do componente.

* **[!UICONTROL Mesmo tamanho para todas as tags]**

  Se marcada, todas as palavras na nuvem de tags serão estilizadas da mesma forma. Se desmarcada, as palavras são estilizadas de forma diferente de acordo com seu uso. O padrão está desmarcado.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos de tags](tag.md) página para desenvolvedores.

Consulte [Marcação do conteúdo gerado pelo usuário](tag-ugc.md) (UGC) para obter informações sobre como criar e gerenciar tags.

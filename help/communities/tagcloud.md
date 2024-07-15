---
title: Uso da Social Tag Cloud
description: Saiba como adicionar um componente do Social Tag Cloud a uma página que permite que os membros da comunidade conectados identifiquem rapidamente os tópicos de tendência e localizem o conteúdo marcado.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# Uso da Social Tag Cloud {#using-social-tag-cloud}

## Introdução {#introduction}

O componente `Social Tag Cloud` destaca as marcas aplicadas pelos membros da comunidade ao postar conteúdo. É um meio de identificar tópicos de tendência e permitir que os visitantes do site localizem rapidamente o conteúdo marcado.

Para outro meio de identificar tendências atuais, visite [Tendências da atividade](trends.md).

Esta página documenta as configurações da caixa de diálogo do componente `Social Tag Cloud` e descreve a experiência do usuário.

Para obter informações detalhadas para desenvolvedores, consulte o [Tag Essentials](tag.md).

Consulte [Administrando tags](../../help/sites-administering/tags.md) para obter informações sobre como criar e gerenciar tags e às quais tags de conteúdo foram aplicadas.

## Adicionar uma nuvem de tag social {#adding-a-social-tag-cloud}

Para adicionar um componente `Social Tag Cloud` a uma página no modo de autor, use o navegador de componentes para localizar `Communities / Social Tag Cloud` e arrastá-lo para o local em uma página onde a nuvem de tags deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](tag.md#essentials-for-client-side) são incluídas, é assim que o componente `Social Tag Cloud` aparece:

![marca-social](assets/social-tag.png)

## Configuração da Social Tag Cloud {#configuring-social-tag-cloud}

Selecione o componente `Social Tag Cloud` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

Na guia **[!UICONTROL Social Tag Cloud]**, especifique quais tags serão exibidas e, se as tags forem links ativos, o local da página para os resultados da pesquisa:

![nuvem-de-marca-social](assets/social-tag-cloud.png)

* **[!UICONTROL Tags do Social a serem exibidas]**
Identifique quais tags UGC serão exibidas. As opções suspensas são:

   * `From page and child pages`
   * `All tags`

  O padrão é `From page and child pages`, onde &quot;página&quot; se refere à configuração de **Página** abaixo.

* **[!UICONTROL Página]**

  (Obrigatório se não `All tags)` O caminho para o UGC de uma página. O padrão é a página atual, se deixada em branco.

* **[!UICONTROL Nenhum link nas marcas]**

  Se marcadas, as tags serão exibidas na nuvem de tags como texto simples. Se desmarcada, as tags são exibidas como links ativos que pesquisam em todo o conteúdo ao qual essa tag é aplicada. O padrão está desmarcado e requer que o **[!UICONTROL Caminho do Resultado da Pesquisa]** seja definido.

* **[!UICONTROL Caminho do resultado de pesquisa]**

  O caminho para uma página na qual um componente `Search Result` foi colocado, configurado para fazer referência ao UGC que inclui o caminho UGC especificado pela configuração **Página**.

## Alterar exibição da Tags em nuvem do Social {#change-display-of-social-tag-cloud}

Para editar a exibição da **Nuvem da Marca Social**, insira o [Modo de Design](../../help/sites-authoring/default-components-designmode.md) e clique duas vezes no componente `Social Tag Cloud` inserido para abrir uma caixa de diálogo com uma guia adicional.

Usando a guia **[!UICONTROL Social Tag Cloud (Design)]**, especifique como as marcas são exibidas. Uma tag pode ser uma tag simples, uma única palavra no namespace padrão ou uma taxonomia hierárquica:

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Mostrar caminhos completos do título]**

  Se marcado, mostra os títulos das tags principais e o namespace de cada tag aplicada.

  Por exemplo:

   * Verificado: `Geometrixx Media: Gadgets / Cars`
   * Desmarcado: `Cars`

  Não há diferença para uma tag simples.

  O padrão está desmarcado.

* **[!UICONTROL Mostrar apenas marcas de folha]**

  Se marcado, mostra somente as tags aplicadas que não contêm outras tags.

  Por exemplo, considerando a TagID de:

  `Geometrixx Media: Gadgets / Cars`

  Há três tags que podem ser aplicadas:

  `Geometrixx Media (the namespace)`, `Gadgets` e `Cars`

   * Marcado: somente `Cars` são exibidos, se aplicados.
   * Desmarcado: `Geometrixx Media`, `Gadgets` e `Cars` são exibidos, se aplicados.

  Uma tag simples é uma tag folha.

  O padrão está desmarcado.

* **[!UICONTROL Modelo de link]**

  Um modelo, diferente de um padrão, usado para exibir os links em uma nuvem de tags, quando os links são ativados por meio da caixa de diálogo de edição do componente.

* **[!UICONTROL Mesmo tamanho para todas as marcas]**

  Se marcada, todas as palavras na nuvem de tags serão estilizadas da mesma forma. Se desmarcada, as palavras são estilizadas de forma diferente de acordo com seu uso. O padrão está desmarcado.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página do [Tag Essentials](tag.md) para desenvolvedores.

Consulte [Marcando o conteúdo gerado pelo usuário](tag-ugc.md) (UGC) para obter informações sobre como criar e gerenciar tags.

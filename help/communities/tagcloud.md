---
title: Uso da Nuvem de tags sociais
seo-title: Uso da Nuvem de tags sociais
description: Adicionar um componente da Nuvem de tags sociais a uma página
seo-description: Adicionar um componente da Nuvem de tags sociais a uma página
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# Uso da Nuvem de tags sociais {#using-social-tag-cloud}

## Introdução {#introduction}

O `Social Tag Cloud` componente destaca as tags aplicadas pelos membros da comunidade ao publicar conteúdo. É uma forma de identificar os tópicos de tendência e permitir que os visitantes do site localizem rapidamente o conteúdo marcado.

Para obter outro meio de identificar as tendências atuais, visite Tendências [de](trends.md)Atividade.

Esta página documentos as configurações de diálogo do `Social Tag Cloud` componente e descreve a experiência do usuário.

Para obter informações detalhadas para desenvolvedores, consulte [Tag Essentials](tag.md).

See [Administering Tags](../../help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.

## Adicionar uma nuvem de tags sociais {#adding-a-social-tag-cloud}

Para adicionar um `Social Tag Cloud` componente a uma página no modo de autor, use o navegador de componentes para localizá-lo `Communities / Social Tag Cloud` e arrastá-lo para o lugar em uma página onde a nuvem de tags deve aparecer.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](basics.md).

Quando as bibliotecas [do lado do cliente](tag.md#essentials-for-client-side) necessárias forem incluídas, o `Social Tag Cloud` componente aparecerá desta forma:

![chlimage_1-303](assets/chlimage_1-303.png)

## Configuração da nuvem de tags sociais {#configuring-social-tag-cloud}

Selecione o componente inserido a ser acessado e selecione o `Social Tag Cloud` `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-304](assets/chlimage_1-304.png)

Na guia Nuvem **[!UICONTROL de tags do]** Social, especifique quais tags serão exibidas e, se as tags forem links ativos, o local da página para os resultados da pesquisa:

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL Tags sociais para exibir]** Identifique quais tags UGC serão exibidas. As opções de menu suspenso são:

   * `From page and child pages`
   * `All tags`
   O padrão é `From page and child pages`, onde &quot;página&quot; se refere à configuração **Página** abaixo.

* **[!UICONTROL Página]**

   (Obrigatório se não `All tags)` O caminho para o UGC de uma página. O padrão é a página atual se deixado em branco.

* **[!UICONTROL Não há links nas tags]**

   Se marcadas, as tags serão exibidas na nuvem de tags como texto sem formatação. Se desmarcadas, as tags serão exibidas como links ativos que pesquisam todo o conteúdo ao qual essa tag é aplicada. O padrão está desmarcado e requer que o Caminho **[!UICONTROL do resultado da]** pesquisa seja definido.

* **[!UICONTROL Pesquisar caminho de resultados]**

   O caminho para uma página na qual um `Search Result` componente foi colocado, configurado para fazer referência ao UGC que inclui o caminho UGC especificado pela configuração **Página** .

## Alterar exibição da nuvem de tags sociais {#change-display-of-social-tag-cloud}

Para editar a exibição da Tag Cloud **do** Social, insira o Modo [de](../../help/sites-authoring/default-components-designmode.md) design e clique no duplo no `Social Tag Cloud` componente inserido para abrir uma caixa de diálogo com uma guia adicional.

Usando a guia **[!UICONTROL Nuvem de tags sociais (Design)]** , especifique como as tags são exibidas. Uma tag pode ser uma tag simples, uma única palavra na namespace padrão ou uma taxonomia hierárquica:

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL Mostrar caminhos completos do título]**

   Se marcada, mostra os títulos das tags pai e a namespace de cada tag aplicada.

   Por exemplo:

   * Marcado: `Geometrixx Media: Gadgets / Cars`
   * Desmarcado: `Cars`
   Não há diferença para uma tag simples.

   O padrão está desmarcado.

* **[!UICONTROL Mostrar apenas tags de folha]**

   Se marcada, mostra somente as tags aplicadas que não contêm outras tags.

   Por exemplo, considerando a TagID de:

   `Geometrixx Media: Gadgets / Cars`

   Há três tags que podem ser aplicadas:

   `Geometrixx Media (the namespace)`, `Gadgets`e `Cars`

   * Verificado: Somente `Cars` será exibido, se aplicado.
   * Desmarcado: `Geometrixx Media` e `Gadgets`assim como `Cars` será exibido, se aplicado.
   Uma tag simples é uma tag de folha.

   O padrão está desmarcado.

* **[!UICONTROL Modelo do link]**

   Um modelo, diferente de um padrão, usado para exibir os links em uma nuvem de tags, quando os links são ativados pela caixa de diálogo de edição de componentes.

* **[!UICONTROL Mesmo tamanho para todas as tags]**

   Se marcada, todas as palavras na nuvem de tags têm o mesmo estilo. Se não estiver marcada, o estilo das palavras será diferente de acordo com seu uso. O padrão está desmarcado.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Tag Essentials](tag.md) para desenvolvedores.

Consulte [Marcação de conteúdo](tag-ugc.md) gerado pelo usuário (UGC) para obter informações sobre como criar e gerenciar tags.

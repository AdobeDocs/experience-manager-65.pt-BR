---
title: Gerenciar tags inteligentes e pesquisas
description: Atualizar ou remover as tags inteligentes imprecisas para melhorar a relevância das tags
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Gerenciar tags inteligentes e pesquisas {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

É possível preparar tags inteligentes para remover tags imprecisas que possam ter sido atribuídas às imagens da sua marca, de modo que somente as tags mais relevantes sejam exibidas.

A moderação de tags inteligentes também ajuda a refinar pesquisas baseadas em tags para imagens, garantindo que sua imagem apareça nos resultados da pesquisa para obter as tags mais relevantes. Essencialmente, ajuda a eliminar as chances de imagens não relacionadas aparecerem nos resultados da pesquisa.

Também é possível atribuir uma classificação mais alta a uma tag para aumentar sua relevância em relação a uma imagem. A promoção de uma tag para uma imagem aumenta as chances de a imagem aparecer nos resultados da pesquisa quando uma pesquisa é realizada com base na tag específica.

1. Na caixa Omnisearch, procure ativos com base em uma tag.
1. Inspecione os resultados da pesquisa para identificar uma imagem que não seja relevante para a sua pesquisa.
1. Selecione a imagem e clique em **[!UICONTROL Gerenciar tags]** na barra de ferramentas.
1. Na página **[!UICONTROL Gerenciar tags]** , inspecione as tags. Se você não quiser que a imagem seja pesquisada com base em uma tag específica, selecione a tag e clique em **[!UICONTROL Excluir]** na barra de ferramentas. Como alternativa, clique no `X` símbolo que aparece ao lado do rótulo.
1. Para atribuir uma classificação superior a uma tag, selecione-a e clique em **[!UICONTROL Promover]** na barra de ferramentas. A tag promovida é movida para a seção **[!UICONTROL Tags]** .
1. Click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the Success dialog.
1. Navegue até a página de propriedades da imagem. Observe que a tag promovida tem uma relevância alta e, portanto, aparece mais alta nos resultados da pesquisa.

## Compreender os resultados da pesquisa do AEM com tags inteligentes {#understandsearch}

Por padrão, a pesquisa do AEM combina os termos de pesquisa com uma `AND` cláusula. O uso de tags inteligentes não altera esse comportamento padrão. O uso de tags inteligentes adiciona uma `OR` cláusula adicional para localizar qualquer um dos termos de pesquisa nas tags inteligentes aplicadas. For example, consider searching for `woman running`. Por padrão, os ativos com apenas `woman` ou apenas `running` palavras-chave nos metadados não aparecem nos resultados da pesquisa. No entanto, um ativo marcado com tags inteligentes `woman` ou `running` usando tags inteligentes aparece em um query de pesquisa desse tipo. Então os resultados da pesquisa são uma combinação de...

* ativos com `woman` e `running` palavras-chave nos metadados.

* ativos marcados com inteligência com qualquer uma das palavras-chave.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos dos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. corresponde `woman running` aos vários campos de metadados.
1. corresponde a `woman running` em tags inteligentes.
1. correspondências de `woman` ou de `running` em tags inteligentes.

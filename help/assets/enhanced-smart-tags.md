---
title: Tags inteligentes aprimoradas
description: Tags inteligentes aprimoradas
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 5aff321eb52c97e076c225b67c35e9c6d3371154
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 1%

---

# Entender, aplicar e preparar Tags inteligentes {#enhanced-smart-tags}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

As organizações que lidam com ativos digitais usam cada vez mais vocabulário controlado por taxonomia em metadados de ativos. Basicamente, ele inclui uma lista de palavras-chave que funcionários, parceiros e clientes normalmente usam para consultar e pesquisar ativos digitais de uma classe específica. Marcar ativos com um vocabulário controlado por taxonomia garante que eles sejam facilmente identificados e recuperados.

Em comparação aos vocabulários de linguagem natural, marcar ativos digitais com base na taxonomia de negócios ajuda a alinhá-los aos negócios de uma empresa e garante que os ativos mais relevantes apareçam nas pesquisas.

Por exemplo, um fabricante de carros pode marcar imagens de carro com nomes de modelo para que apenas imagens relevantes apareçam quando imagens de vários modelos são pesquisadas para projetar uma campanha promocional.

Para que o Serviço de conteúdo inteligente aplique as tags certas, treine-o para reconhecer sua taxonomia. Para treinar o serviço, primeiro prepare um conjunto de ativos e tags que descreva melhor esses ativos. Para ajudar o serviço a aprender, aplique essas tags nos ativos e execute um fluxo de trabalho de treinamento.

Depois que uma tag é treinada e preparada, o serviço agora pode aplicá-las a ativos por meio de um fluxo de trabalho de marcação.

Em segundo plano, o Serviço de conteúdo inteligente usa a estrutura da IA do Adobe Sensei para treinar o algoritmo de reconhecimento de imagem de acordo com sua estrutura de tags e sua taxonomia comercial. Essa inteligência de conteúdo é usada para aplicar tags relevantes em um conjunto diferente de ativos.

O Serviço de Conteúdo Inteligente é um serviço de nuvem hospedado em [!DNL Adobe Developer Console]. Para usá-lo no [!DNL Adobe Experience Manager], o administrador do sistema deve integrar sua implantação do [!DNL Experience Manager] com o [!DNL Adobe Developer Console].

Em resumo, estas são as principais etapas para usar o Serviço de conteúdo inteligente:

* Integração
* Revisão de ativos e tags (definição de taxonomia)
* Treinando o serviço de conteúdo inteligente
* Marcação automática

![Fluxograma](assets/flowchart.gif)

## Pré-requisitos e formatos compatíveis {#prerequisites}

Antes de usar o Serviço de Conteúdo Inteligente, é necessário criar uma integração no [!DNL Adobe Developer Console].

* Uma conta da Adobe ID com privilégios de administrador para a organização.
* Habilite o serviço de Conteúdo Inteligente para sua organização.
* Para adicionar o Pacote Base do Smart Content Services a uma implantação, licencie o Pacote Base [!DNL Adobe Experience Manager Sites] e o complemento [!DNL Assets].

O serviço aplica Tags inteligentes a ativos dos seguintes tipos MIME:

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

O serviço aplica Tags inteligentes a representações de ativos dos seguintes tipos MIME:

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## Integração {#onboarding}

O Serviço de Conteúdo Inteligente está disponível para compra como um complemento do [!DNL Experience Manager]. Após a compra, um email é enviado ao administrador da sua organização com um link para [!DNL Adobe I/O].

O administrador pode seguir o link para integrar o Serviço de Conteúdo Inteligente ao [!DNL Experience Manager]. Para integrar o serviço com [!DNL Experience Manager Assets], consulte [Configurar Tags Inteligentes](config-smart-tagging.md).

O processo de integração é concluído quando o administrador configura o serviço e adiciona usuários em [!DNL Experience Manager].

## Revisar ativos e tags {#reviewing-assets-and-tags}

Depois de integrar o, a primeira coisa que você deseja fazer é identificar um conjunto de tags que descrevam melhor essas imagens no contexto de seus negócios.

Em seguida, analise as imagens para identificar um conjunto de imagens que melhor representam seu produto para um requisito de negócios específico. Verifique se os ativos do conjunto preparado estão em conformidade com as [diretrizes de treinamento do Serviço de Conteúdo Inteligente](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Adicione os ativos a uma pasta e aplique as tags a cada ativo da página de propriedades. Em seguida, execute o fluxo de trabalho de treinamento nesta pasta. O conjunto preparado de ativos permite que o Serviço de conteúdo inteligente treine mais ativos de maneira eficiente usando suas definições de taxonomia.

>[!NOTE]
>
>1. O treinamento é um processo irrevogável. A Adobe recomenda que você revise as tags no conjunto de ativos preparado bem antes de treinar o Serviço de conteúdo inteligente nas tags.
>1. Antes de treinar uma marca, consulte as [diretrizes de treinamento do Smart Content Service](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Ao treinar o Serviço de conteúdo inteligente pela primeira vez, a Adobe recomenda que você o treine em pelo menos duas tags distintas.

## Compreender os resultados da pesquisa de [!DNL Experience Manager] com marcas inteligentes {#understandsearch}

Por padrão, a pesquisa [!DNL Experience Manager] combina os termos de pesquisa com uma cláusula `AND`. O uso de tags inteligentes não altera esse comportamento padrão. O uso de tags inteligentes adiciona uma cláusula `OR` extra para localizar qualquer termo de pesquisa relacionado às tags inteligentes. Por exemplo, considere pesquisar por `woman running`. Por padrão, o Assets com apenas `woman` ou apenas `running` palavra-chave nos metadados não aparece nos resultados da pesquisa. No entanto, um ativo marcado com `woman` ou `running` usando marcas inteligentes aparece em tal consulta de pesquisa. Então os resultados da busca são uma combinação de,

* Assets com `woman` e `running` palavras-chave nos metadados.

* Assets inteligente marcada com uma das palavras-chave.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa em campos de metadados são exibidos primeiro, seguido pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. Correspondências de `woman running` nos vários campos de metadados.
1. Correspondências de `woman running` em tags inteligentes.
1. Correspondências de `woman` ou de `running` nas marcas inteligentes.

>[!CAUTION]
>
>Se a indexação Lucene for feita de [!DNL Adobe Experience Manager], a pesquisa baseada em tags inteligentes não funcionará conforme esperado.

## Marcar ativos automaticamente {#tagging-assets-automatically}

Depois de treinar o Serviço de conteúdo inteligente, é possível acionar o fluxo de trabalho de marcação para aplicar automaticamente as tags apropriadas a um conjunto diferente de ativos semelhantes.

Você pode executar o fluxo de trabalho de marcação periodicamente ou sempre que necessário.

>[!NOTE]
>
>O fluxo de trabalho de marcação é executado em ativos e pastas.

### Marcação periódica {#periodic-tagging}

Você pode ativar o Serviço de conteúdo inteligente para marcar ativos periodicamente em uma pasta. Abra a página de propriedades da sua pasta de ativos, selecione **[!UICONTROL Habilitar Tags inteligentes]** na guia **[!UICONTROL Detalhes]** e salve as alterações.

Depois que essa opção é selecionada para uma pasta, o Serviço de conteúdo inteligente marca automaticamente os ativos dentro da pasta. Por padrão, o workflow de marcação é executado todos os dias às 12h.

### Marcação sob demanda {#on-demand-tagging}

É possível acionar o fluxo de trabalho de marcação a partir do console do fluxo de trabalho ou da linha do tempo para marcar instantaneamente seus ativos.

>[!NOTE]
>
>Se você executar o fluxo de trabalho de marcação a partir da linha do tempo, poderá aplicar tags em no máximo 15 ativos por vez.

#### Adicionar tags a ativos no console de fluxo de trabalho {#tagging-assets-from-the-workflow-console}

1. Na interface do [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.
1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o fluxo de trabalho **[!UICONTROL Assets de Tags inteligentes do DAM]** e clique em **[!UICONTROL Iniciar fluxo de trabalho]** na barra de ferramentas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Na caixa de diálogo **[!UICONTROL Executar Fluxo de Trabalho]**, navegue até a pasta de carga que contém ativos nos quais você deseja aplicar suas marcas automaticamente.
1. Especifique um título para o fluxo de trabalho e um comentário opcional. Clique em **[!UICONTROL Executar]**.

   ![caixa_de_diálogo_de_marcação](assets/tagging_dialog.png)

   Para verificar se o Serviço de conteúdo inteligente marcou seus ativos corretamente, navegue até a pasta de ativos e revise as tags.

#### Adicionar tags a ativos a partir da linha do tempo {#tagging-assets-from-the-timeline}

1. Na interface do usuário do [!DNL Assets], selecione a pasta que contém ativos ou ativos específicos aos quais deseja aplicar marcas inteligentes.
1. No canto superior esquerdo, abra a **[!UICONTROL Linha do Tempo]**.
1. Abra as ações na parte inferior da barra lateral esquerda e clique em **[!UICONTROL Iniciar Fluxo de Trabalho]**.

   ![start_workflow](assets/start_workflow.png)

1. Selecione o fluxo de trabalho **[!UICONTROL Assets de Marca Inteligente do DAM]** e especifique um título para o fluxo de trabalho.
1. Clique em **[!UICONTROL Iniciar]**. O fluxo de trabalho aplica tags aos ativos. para verificar se o Serviço de conteúdo inteligente marcou seus ativos corretamente, navegue até a pasta de ativos e revise as tags.

>[!NOTE]
>
>Nos ciclos de marcação subsequentes, somente os ativos modificados serão marcados novamente com tags recém-treinadas. No entanto, até mesmo os ativos inalterados são marcados se a lacuna entre o último e o atual ciclos de marcação para o fluxo de trabalho de marcação exceder 24 horas. Para workflows de marcação periódica, os ativos inalterados são marcados quando o intervalo de tempo excede seis meses.

## Preparar ou moderar as tags inteligentes aplicadas {#manage-smart-tags}

É possível preparar tags inteligentes para remover tags imprecisas atribuídas às imagens da sua marca, de modo que somente as tags mais relevantes sejam exibidas.

A moderação de tags inteligentes também ajuda a refinar as pesquisas de imagens baseadas em tags, garantindo que a imagem seja exibida nos resultados da pesquisa para as tags mais relevantes. Basicamente, ajuda a eliminar as chances de imagens não relacionadas serem exibidas nos resultados da pesquisa.

Também é possível atribuir uma classificação mais alta a uma tag para aumentar sua relevância para uma imagem. Promover uma tag para uma imagem aumenta as chances da imagem aparecer nos resultados da pesquisa quando a tag específica for pesquisada.

1. Na caixa de pesquisa, pesquise por ativos com base no uso de uma tag como palavra-chave.
1. Para identificar uma imagem que não seja relevante para sua pesquisa, analise os resultados da pesquisa.
1. Selecione a imagem e clique em **[!UICONTROL Gerenciar marcas]** na barra de ferramentas.
1. Na página **[!UICONTROL Gerenciar marcas]**, examine as marcas. Se não quiser que a imagem seja pesquisada com base em uma marca específica, selecione a marca e clique em **[!UICONTROL Excluir]** na barra de ferramentas. Como alternativa, clique no símbolo `x` que aparece ao lado de uma marca.
1. Como opção, para atribuir uma classificação mais alta a uma marca, selecione a marca e clique em **[!UICONTROL Promover]** na barra de ferramentas. A marca promovida foi movida para a seção **[!UICONTROL Marcas]**.
1. Clique em **[!UICONTROL Salvar]** e em **[!UICONTROL OK]**
1. Navegue até a página **[!UICONTROL Propriedades]** da imagem. Observe que a tag promovida recebe mais relevância e aparece anteriormente nos resultados da pesquisa.

## Dicas e limitações {#tips-best-practices-limitations}

* Para treinar o modelo, use as imagens mais apropriadas. O treinamento não pode ser revertido ou o modelo de treinamento não pode ser removido. A precisão da marcação depende do treinamento atual, portanto, faça isso com cuidado.
* O uso dos Serviços de conteúdo inteligente é limitado a até 2 milhões de imagens marcadas por ano. Todas as imagens duplicadas processadas e marcadas são contadas como imagens marcadas.
* Se você executar o fluxo de trabalho de marcação a partir da linha do tempo, poderá aplicar tags em no máximo 15 ativos por vez.
* As Tags inteligentes funcionam somente para formatos de imagem PNG e JPG. Portanto, os ativos compatíveis que têm representações criadas nesses dois formatos são marcados com Tags inteligentes.

>[!MORELIKETHIS]
>
>* [Visão geral e como treinar Tags Inteligentes](enhanced-smart-tags.md)
>* [Configurar marcação inteligente](config-smart-tagging.md)
>* [Solução de problemas de marcas inteligentes para credenciais do OAuth](config-oauth.md)
>* [Tutorial em vídeo sobre marcas inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html?lang=pt-BR)

---
title: Tags inteligentes aprimoradas
description: Tags inteligentes aprimoradas
contentOwner: AG
feature: Smart Tags, Search
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 1%

---


# Entender, aplicar e preparar Tags inteligentes {#enhanced-smart-tags}

As organizações que lidam com ativos digitais cada vez mais usam um vocabulário controlado por taxonomia em metadados de ativos. Basicamente, inclui uma lista de palavras-chave que funcionários, parceiros e clientes costumam usar para consultar e pesquisar ativos digitais de uma classe específica. Marcar ativos com um vocabulário controlado por taxonomia garante que os ativos sejam facilmente identificados e recuperados.

Comparado aos vocabulários de linguagem natural, a marcação de ativos digitais com base na taxonomia comercial ajuda a alinhá-los aos negócios de uma empresa e garante que os ativos mais relevantes apareçam em pesquisas.

Por exemplo, um fabricante de carros pode marcar imagens de carros com nomes de modelos para que somente imagens relevantes sejam exibidas quando imagens de vários modelos forem pesquisadas para projetar uma campanha promocional.

Para que o Serviço de conteúdo inteligente aplique as tags certas, treine-o para reconhecer sua taxonomia. Para treinar o serviço, primeiro prepare um conjunto de ativos e tags que descrevam melhor esses ativos. Para ajudar o serviço a aprender, aplique essas tags nos ativos e execute um fluxo de trabalho de treinamento.

Depois que uma tag é treinada e pronta, o serviço agora pode aplicar essas tags em ativos por meio de um fluxo de trabalho de marcação.

Em segundo plano, o Serviço de conteúdo inteligente usa a estrutura da Adobe Sensei AI para treinar o algoritmo de reconhecimento de imagem de acordo com sua estrutura de tags e sua taxonomia comercial. Essa inteligência de conteúdo é então usada para aplicar tags relevantes em um conjunto diferente de ativos.

O Serviço de conteúdo inteligente é um serviço em nuvem hospedado em [!DNL Adobe Developer Console]. Para usá-lo em [!DNL Adobe Experience Manager], o administrador do sistema deve integrar sua implantação [!DNL Experience Manager] com [!DNL Adobe Developer Console].

Em resumo, estas são as principais etapas para usar o Serviço de conteúdo inteligente:

* Integração
* Revisão de ativos e tags (definição de taxonomia)
* Treinamento do Serviço de conteúdo inteligente
* Marcação automática

![Fluxograma](assets/flowchart.gif)

## Pré-requisitos e formatos compatíveis {#prerequisites}

Antes de usar o Serviço de conteúdo inteligente, verifique o seguinte para criar uma integração em [!DNL Adobe Developer Console]:

* Uma conta da Adobe ID com privilégios de administrador para a organização.
* Ative o serviço de Conteúdo Inteligente para sua organização.
* Para adicionar o Pacote Base dos Serviços de Conteúdo Inteligente a uma implantação, licencie o [!DNL Adobe Experience Manager Sites] Pacote Base e o [!DNL Assets] complemento.

O serviço aplica Tags inteligentes a ativos dos seguintes tipos MIME:

* image/jpeg
* image/tiff
* image/png
* image/bmp
* image/gif
* image/pjpeg
* image/x-portable-anymap
* image/x-portable-bitmap
* image/x-portable-graymap
* imagem/x-portable-pixmap
* image/x-rgb
* image/x-xbitmap
* image/x-xpixmap
* image/x-icon
* imagem/photoshop
* image/x-photoshop
* image/psd
* image/vnd.adobe.photoshop

O serviço aplica Tags inteligentes a representações de ativos dos seguintes tipos MIME:

* image/jpeg
* image/pjpeg
* image/png

## Integração {#onboarding}

O Serviço de conteúdo inteligente está disponível para compra como um complemento para [!DNL Experience Manager]. Após a compra, um email é enviado ao administrador da organização com um link para [!DNL Adobe I/O].

O administrador pode seguir o link para integrar o Serviço de conteúdo inteligente com [!DNL Experience Manager]. Para integrar o serviço a [!DNL Experience Manager Assets], consulte [Configurar tags inteligentes](config-smart-tagging.md).

O processo de integração é concluído quando o administrador configura o serviço e adiciona usuários em [!DNL Experience Manager].

>[!NOTE]
>
>Se estiver usando [!DNL Experience Manager] 6.3 ou versão anterior e exigir o serviço de marcação para seus ativos, consulte [Tags inteligentes](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). As Tags inteligentes não usam os recursos de IA mais recentes e, portanto, são menos precisas do que o serviço de marcação inteligente aprimorado.

## Revisar ativos e tags {#reviewing-assets-and-tags}

Depois que estiver integrado, a primeira coisa que você deseja fazer é identificar um conjunto de tags que descreva melhor essas imagens no contexto de sua empresa.

Em seguida, revise as imagens para identificar um conjunto de imagens que melhor representam seu produto para um requisito específico de negócios. Certifique-se de que os ativos em seu conjunto preparado estejam em conformidade com [Diretrizes de treinamento do Serviço de conteúdo inteligente](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Adicione os ativos a uma pasta e aplique as tags a cada ativo da página de propriedades. Em seguida, execute o workflow de treinamento nesta pasta. O conjunto preparado de ativos permite que o Serviço de conteúdo inteligente treine efetivamente mais ativos usando suas definições de taxonomia.

>[!NOTE]
>
>1. A formação é um processo irrevogável. O Adobe recomenda que você analise as tags no conjunto de ativos preparado bem antes de treinar o Serviço de conteúdo inteligente nas tags.
>1. Antes de treinar uma tag, consulte [Diretrizes de treinamento do Serviço de conteúdo inteligente](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Ao treinar o Serviço de conteúdo inteligente pela primeira vez, o Adobe recomenda treiná-lo em pelo menos duas tags distintas.


## Entender os resultados da pesquisa [!DNL Experience Manager] com tags inteligentes {#understandsearch}

Por padrão, a pesquisa [!DNL Experience Manager] combina os termos de pesquisa com uma cláusula `AND`. O uso de tags inteligentes não altera esse comportamento padrão. O uso de tags inteligentes adiciona uma cláusula `OR` extra para localizar qualquer um dos termos de pesquisa relacionados às tags inteligentes. Por exemplo, considere pesquisar por `woman running`. Os ativos com apenas `woman` ou apenas `running` palavra-chave nos metadados não aparecem nos resultados da pesquisa por padrão. No entanto, um ativo marcado com `woman` ou `running` usando tags inteligentes aparece em tal query de pesquisa. Então os resultados da pesquisa são uma combinação de...

* Ativos com palavras-chave `woman` e `running` nos metadados.

* Ativos marcados com tags inteligentes com qualquer uma das palavras-chave.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. Corresponde a `woman running` nos vários campos de metadados.
1. Corresponde a `woman running` em tags inteligentes.
1. Corresponde a `woman` ou de `running` em tags inteligentes.

>[!CAUTION]
>
>Se a indexação do Lucene for feita a partir de [!DNL Adobe Experience Manager], a pesquisa baseada em tags inteligentes não funcionará conforme esperado.

## Marcar ativos automaticamente {#tagging-assets-automatically}

Depois de ter treinado o Serviço de conteúdo inteligente, você pode acionar o fluxo de trabalho de marcação para aplicar automaticamente as tags apropriadas em um conjunto diferente de ativos semelhantes.

Você pode executar o fluxo de trabalho de marcação periodicamente ou sempre que necessário.

>[!NOTE]
>
>O fluxo de trabalho de marcação é executado em ativos e pastas.

### Marcação periódica {#periodic-tagging}

Você pode permitir que o Serviço de conteúdo inteligente marque periodicamente ativos em uma pasta. Abra a página de propriedades da pasta de ativos, selecione **[!UICONTROL Ativar tags inteligentes]** na guia **[!UICONTROL Detalhes]** e salve as alterações.

Quando essa opção é selecionada para uma pasta, o Serviço de conteúdo inteligente insere tags automaticamente nos ativos da pasta. Por padrão, o fluxo de trabalho de marcação é executado todos os dias às 12:00 AM.

### Marcação sob demanda {#on-demand-tagging}

Você pode acionar o fluxo de trabalho de marcação no console do fluxo de trabalho ou na linha do tempo para marcar instantaneamente seus ativos.

>[!NOTE]
>
>Se você executar o fluxo de trabalho de marcação na linha do tempo, poderá aplicar tags em no máximo 15 ativos de cada vez.

#### Marque ativos no console do fluxo de trabalho {#tagging-assets-from-the-workflow-console}

1. Na interface [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o fluxo de trabalho **[!UICONTROL Ativos de tags inteligentes do DAM]** e clique em **[!UICONTROL Iniciar fluxo de trabalho]** na barra de ferramentas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Na caixa de diálogo **[!UICONTROL Executar fluxo de trabalho]**, navegue até a pasta de carga que contém ativos nos quais você deseja aplicar suas tags automaticamente.
1. Especifique um título para o fluxo de trabalho e um comentário opcional. Clique em **[!UICONTROL Executar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Para verificar se o Serviço de conteúdo inteligente marcou seus ativos corretamente, navegue até a pasta de ativos e revise as tags.

#### Marque ativos na linha do tempo {#tagging-assets-from-the-timeline}

1. Na interface do usuário [!DNL Assets], selecione a pasta que contém ativos ou ativos específicos aos quais deseja aplicar tags inteligentes.
1. No canto superior esquerdo, abra a **[!UICONTROL Linha do tempo]**.
1. Abra as ações na parte inferior da barra lateral esquerda e clique em **[!UICONTROL Iniciar fluxo de trabalho]**.

   ![start_workflow](assets/start_workflow.png)

1. Selecione o fluxo de trabalho **[!UICONTROL Ativos de tags inteligentes do DAM]** e especifique um título para o fluxo de trabalho.
1. Clique em **[!UICONTROL Iniciar]**. O fluxo de trabalho aplica tags nos ativos. para verificar se o Serviço de conteúdo inteligente marcou seus ativos corretamente, navegue até a pasta de ativos e revise as tags.

>[!NOTE]
>
>Nos ciclos de marcação subsequentes, somente os ativos modificados são marcados novamente com tags recém-treinadas. No entanto, mesmo ativos inalterados são marcados se a diferença entre os últimos e os atuais ciclos de marcação do fluxo de trabalho de marcação exceder 24 horas. Para workflows de marcação periódica, os ativos inalterados são marcados quando o intervalo de tempo excede seis meses.

## Preparar ou moderar as tags inteligentes aplicadas {#manage-smart-tags}

Você pode preparar tags inteligentes para remover qualquer tag imprecisa atribuída às imagens da sua marca, de modo que somente as tags mais relevantes sejam exibidas.

A moderação de tags inteligentes também ajuda a refinar as pesquisas de imagens baseadas em tags, garantindo que sua imagem apareça nos resultados da pesquisa para as tags mais relevantes. Essencialmente, ajuda a eliminar as chances de imagens não relacionadas serem exibidas nos resultados da pesquisa.

Também é possível atribuir uma classificação mais alta a uma tag para aumentar sua relevância para uma imagem. Promover uma tag para uma imagem aumenta a probabilidade da imagem aparecer nos resultados da pesquisa quando a tag específica for pesquisada.

1. Na caixa de pesquisa, procure ativos com base em uma tag como palavra-chave.
1. Para identificar uma imagem que não seja relevante para sua pesquisa, analise os resultados da pesquisa.
1. Selecione a imagem e clique em **[!UICONTROL Gerenciar tags]** na barra de ferramentas.
1. Na página **[!UICONTROL Gerenciar tags]**, revise as tags. Se não quiser que a imagem seja pesquisada com base em uma tag específica, selecione a tag e clique em **[!UICONTROL Delete]** na barra de ferramentas. Como alternativa, clique no símbolo `x` que aparece ao lado de uma tag.
1. Como opção, para atribuir uma classificação mais alta a uma tag, selecione a tag e clique em **[!UICONTROL Promover]** na barra de ferramentas. A tag promovida é movida para a seção **[!UICONTROL Tags]**.
1. Clique em **[!UICONTROL Salvar]** e clique em **[!UICONTROL OK]**
1. Navegue até a página **[!UICONTROL Propriedades]** da imagem. Observe que a tag promovida tem mais relevância e é exibida anteriormente nos resultados da pesquisa.

## Dicas e limitações {#tips-best-practices-limitations}

* O uso dos Serviços de conteúdo inteligente é limitado a até 2 milhões de imagens marcadas por ano. Todas as imagens duplicadas que são processadas e marcadas são contadas como uma imagem marcada.
* Se você executar o fluxo de trabalho de marcação na linha do tempo, poderá aplicar tags em no máximo 15 ativos de cada vez.
* As Tags inteligentes funcionam somente para formatos de imagem PNG e JPG. Assim, os ativos compatíveis que têm representações criadas nesses dois formatos são marcados com Tags inteligentes.

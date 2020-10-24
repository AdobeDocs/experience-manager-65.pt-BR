---
title: Tags inteligentes aprimoradas
description: Tags inteligentes aprimoradas
contentOwner: AG
translation-type: tm+mt
source-git-commit: e124025295f29d6f3999dc52467301d48bceee75
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 1%

---


# Compreender, aplicar e preparar tags inteligentes {#enhanced-smart-tags}

As organizações que lidam com ativos digitais cada vez mais usam vocabulário controlado por taxonomia em metadados de ativos. Basicamente, inclui uma lista de palavras-chave que os funcionários, parceiros e clientes normalmente usam para consultar e procurar ativos digitais de uma classe específica. Marcar ativos com um vocabulário controlado por taxonomia garante que eles possam ser facilmente identificados e recuperados por pesquisas baseadas em tags.

Comparado aos vocabulários de linguagem natural, a marcação de ativos digitais com base na taxonomia comercial ajuda a alinhá-los a uma empresa empresa e garante que os ativos mais relevantes sejam exibidos nas pesquisas.

Por exemplo, um fabricante de carros pode marcar imagens de carros com nomes de modelos para que somente imagens relevantes sejam exibidas quando imagens de vários modelos forem pesquisadas para projetar uma campanha promocional.

Para que o Serviço de conteúdo inteligente aplique as tags certas, você deve treiná-lo para reconhecer sua taxonomia. Para treinar o serviço, primeiro prepare um conjunto de ativos e tags que melhor descrevam esses ativos. Aplique essas tags nos ativos e execute um fluxo de trabalho de treinamento para ajudar o serviço a aprender.

Depois que uma tag é treinada e pronta, o serviço pode aplicar essas tags em ativos por meio de um fluxo de trabalho de marcação.

Em segundo plano, o Serviço de conteúdo inteligente usa a estrutura do Adobe Sensei AI para treinar seu algoritmo de reconhecimento de imagem na estrutura de tags e na taxonomia comercial. Essa inteligência de conteúdo é então usada para aplicar tags relevantes em um conjunto diferente de ativos.

O Serviço de conteúdo inteligente é um serviço em nuvem hospedado em E/S de Adobe. Para usá-lo no [!DNL Adobe Experience Manager], o administrador do sistema deve integrar sua [!DNL Experience Manager] implantação com E/S de Adobe.

Em resumo, veja as principais etapas para usar o Serviço de conteúdo inteligente:

* Integração
* Revisão de ativos e tags (definição de taxonomia)
* Treinamento do Serviço de conteúdo inteligente
* Marcação automática

![fluxograma](assets/flowchart.gif)

## Pré-requisitos {#prerequisites}

Antes de usar o Serviço de conteúdo inteligente, verifique o seguinte para criar uma integração na E/S do Adobe:

* Existência de uma Adobe ID com privilégios de administrador para a organização.
* O serviço Smart Content Service está habilitado para sua organização.
* O Pacote básico do Smart Content Services só pode ser adicionado a uma implantação na qual um Pacote [!DNL Sites] básico e um complemento [!DNL Assets] foram licenciados.

## Integração {#onboarding}

The Smart Content Service is available for purchase as an add-on to [!DNL Experience Manager]. Após a compra, um email é enviado ao administrador da sua organização com um link para E/S de Adobe.

O administrador pode seguir o link para integrar o Serviço de conteúdo inteligente ao [!DNL Experience Manager]. Para integrar o serviço com [!DNL Experience Manager Assets], consulte [Configurar tags](config-smart-tagging.md)inteligentes.

O processo de integração é concluído quando o administrador configura o serviço e adiciona usuários ao [!DNL Experience Manager].

>[!NOTE]
>
>Se você estiver usando a versão [!DNL Experience Manager] 6.3 ou anterior e precisar de um serviço de marcação para seus ativos, consulte Tags [inteligentes](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). As Tags inteligentes não usam os mais recentes recursos de AI e, portanto, são menos precisas do que o serviço de tags inteligentes aprimorado.

## Revisar ativos e tags {#reviewing-assets-and-tags}

Depois que você estiver integrado, a primeira coisa que deseja fazer é identificar um conjunto de tags que descrevam melhor essas imagens no contexto de sua empresa.

Em seguida, analise as imagens para identificar um conjunto de imagens que melhor representem seu produto para um requisito comercial específico. Certifique-se de que os ativos no conjunto preparado estejam em conformidade com as diretrizes [de treinamento do Serviço de conteúdo](/help/assets/config-smart-tagging.md#training-the-smart-content-service)inteligente.

Adicione os ativos a uma pasta e aplique as tags a cada ativo da página de propriedades. Em seguida, execute o fluxo de trabalho de treinamento nesta pasta. O conjunto preparado de ativos permite que o Serviço de conteúdo inteligente treine com eficácia mais ativos usando suas definições de taxonomia.

>[!NOTE]
>
>1. A formação é um processo irrevogável. A Adobe recomenda que você revise as tags no conjunto de ativos preparado bem antes de treinar o Serviço de conteúdo inteligente nas tags.
>1. Antes de treinar para uma tag, consulte as diretrizes [de treinamento do Serviço de conteúdo](/help/assets/config-smart-tagging.md#training-the-smart-content-service)inteligente.
>1. Quando você treina o Serviço de conteúdo inteligente pela primeira vez, o Adobe recomenda que você o treine em pelo menos duas tags distintas.


## Compreender os resultados da [!DNL Experience Manager] pesquisa com tags inteligentes {#understandsearch}

Por padrão, [!DNL Experience Manager] a pesquisa combina os termos de pesquisa com uma `AND` cláusula. O uso de tags inteligentes não altera esse comportamento padrão. O uso de tags inteligentes adiciona uma `OR` cláusula adicional para localizar qualquer um dos termos de pesquisa nas tags inteligentes aplicadas. For example, consider searching for `woman running`. Por padrão, os ativos com apenas `woman` ou apenas `running` palavras-chave nos metadados não aparecem nos resultados da pesquisa. No entanto, um ativo marcado com tags inteligentes `woman` ou `running` usando tags inteligentes aparece em um query de pesquisa desse tipo. Então os resultados da pesquisa são uma combinação de...

* ativos com `woman` e `running` palavras-chave nos metadados.

* ativos marcados com inteligência com qualquer uma das palavras-chave.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos dos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. corresponde `woman running` aos vários campos de metadados.
1. corresponde a `woman running` em tags inteligentes.
1. correspondências de `woman` ou de `running` em tags inteligentes.

>[!CAUTION]
>
>Se a indexação do Lucene for feita fora [!DNL Adobe Experience Manager] , a pesquisa com base em tags inteligentes não funcionará como esperado.

## Marcar ativos automaticamente {#tagging-assets-automatically}

Depois de ter treinado o Serviço de conteúdo inteligente, é possível acionar o fluxo de trabalho de marcação para aplicar automaticamente as tags apropriadas em um conjunto diferente de ativos semelhantes.

Você pode executar o fluxo de trabalho de marcação periodicamente ou sempre que necessário.

>[!NOTE]
>
>O fluxo de trabalho de marcação é executado em ativos e pastas.

### Marcação periódica {#periodic-tagging}

Você pode ativar o Serviço de conteúdo inteligente para marcar periodicamente os ativos em uma pasta. Abra a página de propriedades da pasta de ativos, selecione **[!UICONTROL Ativar tags]** inteligentes na guia **[!UICONTROL Detalhes]** e salve as alterações.

Depois que essa opção é selecionada para uma pasta, o Serviço de conteúdo inteligente insere automaticamente tags nos ativos dentro da pasta. Por padrão, o fluxo de trabalho de marcação é executado todos os dias às 12h00.

### Marcação sob demanda {#on-demand-tagging}

Você pode acionar o fluxo de trabalho de marcação do console do fluxo de trabalho ou da linha do tempo para marcar instantaneamente seus ativos.

>[!NOTE]
>
>Se você executar o fluxo de trabalho de marcação a partir da linha do tempo, poderá aplicar tags em no máximo 15 ativos de cada vez.

#### Marcar ativos do console de fluxo de trabalho {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Na caixa de diálogo **[!UICONTROL Executar fluxo de trabalho]** , navegue até a pasta de carga que contém os ativos nos quais você deseja aplicar suas tags automaticamente.
1. Especifique um título para o fluxo de trabalho e um comentário opcional. Clique em **[!UICONTROL Executar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Navegue até a pasta de ativos e reveja as tags para verificar se o Smart Content Service marcou seus ativos corretamente.

#### Marcar ativos da linha do tempo {#tagging-assets-from-the-timeline}

1. Na interface do [!DNL Assets] usuário, selecione a pasta que contém ativos ou ativos específicos aos quais você deseja aplicar tags inteligentes.
1. No canto superior esquerdo, abra a **[!UICONTROL Linha do tempo]**.
1. Abra as ações na parte inferior da barra lateral esquerda e clique em Fluxo de trabalho do **[!UICONTROL Start]**.

   ![start_workflow](assets/start_workflow.png)

1. Selecione o fluxo de trabalho dos Ativos **[!UICONTROL de tags inteligentes do]** DAM e especifique um título para o fluxo de trabalho.
1. Clique em **[!UICONTROL Start]**. O fluxo de trabalho aplica suas tags em ativos. Navegue até a pasta de ativos e reveja as tags para verificar se o Smart Content Service marcou seus ativos corretamente.

>[!NOTE]
>
>Nos ciclos de marcação subsequentes, somente os ativos modificados são marcados novamente com tags treinadas recentemente.No entanto, mesmo ativos inalterados são marcados se a diferença entre os últimos e os atuais ciclos de marcação do fluxo de trabalho de marcação exceder 24 horas. Para workflows de marcação periódica, os ativos inalterados são marcados quando o intervalo de tempo excede 6 meses.

## Preparar ou moderar as tags inteligentes aplicadas {#manage-smart-tags}

É possível preparar tags inteligentes para remover tags imprecisas que possam ter sido atribuídas às imagens da sua marca, de modo que somente as tags mais relevantes sejam exibidas.

A moderação de tags inteligentes também ajuda a refinar pesquisas baseadas em tags para imagens, garantindo que sua imagem apareça nos resultados da pesquisa para obter as tags mais relevantes. Essencialmente, ajuda a eliminar as chances de imagens não relacionadas aparecerem nos resultados da pesquisa.

Também é possível atribuir uma classificação mais alta a uma tag para aumentar sua relevância em relação a uma imagem. A promoção de uma tag para uma imagem aumenta as chances de a imagem aparecer nos resultados da pesquisa quando uma pesquisa é realizada com base na tag específica.

1. Na caixa Omnisearch, procure ativos com base em uma tag.
1. Inspect os resultados da pesquisa para identificar uma imagem que você não acha relevante para sua pesquisa.
1. Selecione a imagem e clique em **[!UICONTROL Gerenciar tags]** na barra de ferramentas.
1. Na página **[!UICONTROL Gerenciar tags]** , inspecione as tags. Se você não quiser que a imagem seja pesquisada com base em uma tag específica, selecione a tag e clique em **[!UICONTROL Excluir]** na barra de ferramentas. Como alternativa, clique no `x` símbolo que aparece ao lado de uma tag.
1. Como opção, para atribuir uma classificação mais alta a uma tag, selecione a tag e clique em **[!UICONTROL Promover]** na barra de ferramentas. A tag promovida é movida para a seção **[!UICONTROL Tags]** .
1. Click **[!UICONTROL Save]** and then click **[!UICONTROL OK]**
1. Navegue até a página **[!UICONTROL Propriedades]** da imagem. Observe que a tag promovida tem mais relevância e aparece mais cedo nos resultados da pesquisa.

## Dicas e limitações {#tips-best-practices-limitations}

* O uso do Smart Content Services é limitado a até 2 milhões de imagens marcadas por ano. Todas as imagens de duplicado que são processadas e marcadas são contadas como imagens marcadas.
* Se você executar o fluxo de trabalho de marcação a partir da linha do tempo, poderá aplicar tags em no máximo 15 ativos de cada vez.

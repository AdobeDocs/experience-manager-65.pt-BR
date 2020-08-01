---
title: Tags inteligentes aprimoradas
description: Tags inteligentes aprimoradas
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 8%

---


# Tags inteligentes aprimoradas {#enhanced-smart-tags}

## Visão geral de tags inteligentes aprimoradas {#overview-of-enhanced-smart-tags}

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

## Integração {#onboarding}

The Smart Content Service is available for purchase as an add-on to [!DNL Experience Manager]. Após a compra, um email é enviado ao administrador da sua organização com um link para E/S de Adobe.

O administrador pode seguir o link para integrar o Serviço de conteúdo inteligente ao [!DNL Experience Manager]. Para integrar o serviço com [!DNL Experience Manager Assets], consulte [Configurar tags](config-smart-tagging.md)inteligentes.

O processo de integração é concluído quando o administrador configura o serviço e adiciona usuários ao [!DNL Experience Manager].

>[!NOTE]
>
>Se você estiver usando a versão [!DNL Experience Manager] 6.3 ou anterior e precisar de um serviço de marcação para seus ativos, consulte Tags [inteligentes](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). As Tags inteligentes não usam os mais recentes recursos de AI e, portanto, são menos precisas do que o serviço de tags inteligentes aprimorado.

## Revisar ativos e tags {#reviewing-assets-and-tags}

Depois que você estiver integrado, a primeira coisa que deseja fazer é identificar um conjunto de tags que melhor descrevem essas imagens no contexto de sua empresa.

Em seguida, analise as imagens para identificar um conjunto de imagens que melhor representem seu produto para um requisito comercial específico. Certifique-se de que os ativos no conjunto preparado estejam em conformidade com as diretrizes [de treinamento do Serviço de conteúdo](smart-tags-training-guidelines.md)inteligente.

Adicione os ativos a uma pasta e aplique as tags a cada ativo da página de propriedades. Em seguida, execute o fluxo de trabalho de treinamento nesta pasta. O conjunto preparado de ativos permite que o Serviço de conteúdo inteligente treine com eficácia mais ativos usando suas definições de taxonomia.

>[!NOTE]
>
>1. A formação é um processo irrevogável. A Adobe recomenda que você revise as tags no conjunto de ativos preparado bem antes de treinar o Serviço de conteúdo inteligente nas tags.
>1. Leia as diretrizes [de treinamento do Serviço de conteúdo](smart-tags-training-guidelines.md) inteligente antes de iniciar o treinamento de qualquer tag.
>1. Quando você treina o Serviço de conteúdo inteligente pela primeira vez, o Adobe recomenda que você o treine em pelo menos duas tags distintas.


## Treinar o Serviço de conteúdo inteligente {#training-the-smart-content-service}

Para que o Serviço de conteúdo inteligente reconheça a taxonomia de sua empresa, execute-a em um conjunto de ativos que já incluem tags relevantes para sua empresa. Após o treinamento, o serviço pode aplicar a mesma taxonomia em um conjunto de ativos semelhante.

Você pode treinar o serviço várias vezes para melhorar sua capacidade de aplicar tags relevantes. Após cada ciclo de treinamento, execute um fluxo de trabalho de marcação e verifique se seus ativos estão marcados corretamente.

Você pode treinar o Serviço de conteúdo inteligente periodicamente ou com base em requisitos.

>[!NOTE]
>
>O fluxo de trabalho de treinamento é executado somente em pastas.

### Formação contínua {#periodic-training}

Você pode ativar o Serviço de conteúdo inteligente para treinar periodicamente nos ativos e tags associadas em uma pasta. Abra a página [!UICONTROL Propriedades] da sua pasta de ativos, selecione **[!UICONTROL Ativar tags]** inteligentes na guia **[!UICONTROL Detalhes]** e salve as alterações.

![enable_smart_tags](assets/enable_smart_tags.png)

Quando essa opção for selecionada para uma pasta, [!DNL Experience Manager] executará um fluxo de trabalho de treinamento automaticamente para treinar o Serviço de conteúdo inteligente nos ativos da pasta e em suas tags. Por padrão, o fluxo de trabalho de treinamento é executado semanalmente às 12h30 do sábado.

### Treinamento sob demanda {#on-demand-training}

Você pode treinar o Serviço de conteúdo inteligente sempre que necessário no console Fluxo de trabalho.

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL Smart Tags Training]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.
1. Na caixa de diálogo **[!UICONTROL Executar fluxo de trabalho]** , navegue até a pasta de carga que inclui os ativos marcados para treinar o serviço.
1. Especifique um título para o fluxo de trabalho e adicione um comentário. Em seguida, clique em **[!UICONTROL Executar]**. Os ativos e as tags são enviados para treinamento.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Depois que os ativos em uma pasta são processados para treinamento, somente os ativos modificados são processados em ciclos de treinamento subsequentes.

### Relatórios de treinamento de Visualização {#viewing-training-reports}

Para verificar se o Serviço de conteúdo inteligente é treinado em suas tags no conjunto de ativos de treinamento, reveja o relatório de fluxo de trabalho de treinamento no console Relatórios.

1. Na [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Then, click **[!UICONTROL Create]** from the toolbar.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. To view the report, click **[!UICONTROL View]** from the toolbar.
1. Revise os detalhes do relatório.

   O relatório exibe o status do treinamento das tags que você treinou. A cor verde na coluna **[!UICONTROL Status de treinamento]** indica que o Serviço de conteúdo inteligente foi treinado para a tag. A cor amarela indica que o serviço não é completamente treinado para uma tag específica. Nesse caso, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento para treinar o serviço completamente na tag.

   Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para essas tags.

1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Download]** na barra de ferramentas. O relatório é baixado como uma planilha do Microsoft Excel.

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

Você pode acionar o fluxo de trabalho de marcação do seguinte para marcar instantaneamente seus ativos:

* Console de fluxo de trabalho
* Linha do tempo

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

   Navegue até a pasta de ativos e reveja as tags para verificar se o Smart Content Service marcou seus ativos corretamente. Para obter detalhes, consulte [Gerenciamento de tags](managing-smart-tags.md)inteligentes.

#### Marcar ativos da linha do tempo {#tagging-assets-from-the-timeline}

1. Na interface do [!DNL Assets] usuário, selecione a pasta que contém ativos ou ativos específicos aos quais você deseja aplicar tags inteligentes.
1. No canto superior esquerdo, abra a **[!UICONTROL Linha do tempo]**.
1. Abra as ações na parte inferior da barra lateral esquerda e clique em Fluxo de trabalho do **[!UICONTROL Start]**.

   ![start_workflow](assets/start_workflow.png)

1. Selecione o fluxo de trabalho dos Ativos **[!UICONTROL de tags inteligentes do]** DAM e especifique um título para o fluxo de trabalho.
1. Clique em **[!UICONTROL Start]**. O fluxo de trabalho aplica suas tags em ativos. Navegue até a pasta de ativos e reveja as tags para verificar se o Smart Content Service marcou seus ativos corretamente. Para obter detalhes, consulte [Gerenciamento de tags](managing-smart-tags.md)inteligentes.

>[!NOTE]
>
>Nos ciclos de marcação subsequentes, somente os ativos modificados são marcados novamente com tags treinadas recentemente.No entanto, mesmo ativos inalterados são marcados se a diferença entre os últimos e os atuais ciclos de marcação do fluxo de trabalho de marcação exceder 24 horas. Para workflows de marcação periódica, os ativos inalterados são marcados quando o intervalo de tempo excede 6 meses.

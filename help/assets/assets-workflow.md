---
title: Processar ativos usando workflows
description: Processamento de ativos para converter formatos, criar execuções, gerenciar ativos, validar ativos e executar workflows.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d5a48be283484005013ef3ed7ad015b43f6398b
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---


# Processar ativos digitais {#process-assets}

[!DNL Adobe Experience Manager Assets] permite que você trabalhe com seus ativos digitais de várias maneiras para permitir um processamento robusto de ativos. Você pode usar os métodos de processamento padrão ou personalizado para garantir a conclusão completa dos processos de negócios, as auditorias e a conformidade, a descoberta e distribuição e a sanidade básica dos ativos digitais. Você pode fazer as tarefas de gerenciamento de ativos e, ao mesmo tempo, atingir a escala e a personalização necessárias.

## Entender workflows {#understand-workflows}

Para processamento de ativos, [!DNL Experience Manager] usa workflows. Os workflows ajudam a automatizar a lógica comercial ou as atividades. As etapas granulares para realizar tarefas específicas são fornecidas por padrão e os desenvolvedores podem criar suas próprias etapas personalizadas. Essas etapas podem ser combinadas em uma ordem lógica para criar workflows. Por exemplo, um fluxo de trabalho pode aplicar uma marca d&#39;água em imagens carregadas com base em critérios específicos, como pasta para a qual é carregado, resolução da imagem e assim por diante. Outro exemplo é um fluxo de trabalho configurado para marca d&#39;água e, simultaneamente, adicionar metadados, criar execuções, adicionar tags inteligentes e publicar em um armazenamento de dados.

## Workflows padrão disponíveis em [!DNL Experience Manager] {#default-workflows}

Por padrão, todos os ativos carregados são processados usando o fluxo de trabalho [!UICONTROL DAM Update Asset]. O fluxo de trabalho é executado para cada ativo carregado e realiza tarefas básicas de gerenciamento de ativos, como geração de representação, gravação de metadados, extração da página, extração de mídia e transcodificação.

Para ver os vários modelos de fluxo de trabalho disponíveis por padrão, consulte **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]** em [!DNL Experience Manager].

![Alguns dos fluxos de trabalho padrão](assets/aem-default-workflows.png)

*Figura: Alguns dos workflows padrão disponíveis em  [!DNL Experience Manager].*

## Aplicar workflows para processar ativos {#applying-workflows-to-assets}

Aplicar workflows a ativos digitais é o mesmo que aplicar a páginas do site. Para obter um guia completo sobre como criar e usar workflows, consulte [workflows de start](/help/sites-authoring/workflows-participating.md).

Use workflows em ativos digitais para ativar o ativo ou criar marcas d&#39;água. Muitos dos workflows dos ativos são ativados automaticamente. Por exemplo, o fluxo de trabalho que cria automaticamente uma representação depois que uma imagem é editada é ativado automaticamente.

>[!NOTE]
>
>Se um fluxo de trabalho disponível na interface clássica não estiver disponível na interface habilitada para toque, como [!UICONTROL Solicitar para ativar] e [!UICONTROL Solicitar para desativar], consulte [criar modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md#classic2touchui).

## Aplicar um fluxo de trabalho a um ativo {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Para aplicar um fluxo de trabalho a um ativo, siga estas etapas:

1. Navegue até o local do ativo para o qual você deseja start um fluxo de trabalho e clique no ativo para abrir a página do ativo. Selecione **[!UICONTROL Linha do tempo]** no menu para exibir a linha do tempo.

   ![linha do tempo 1](assets/timeline.png)

1. Clique em **[!UICONTROL Ações]** na parte inferior para abrir a lista de ações disponíveis para o ativo.

1. Clique em **[!UICONTROL Fluxo de trabalho do Start]** na lista.

1. Na caixa de diálogo **[!UICONTROL Fluxo de trabalho do Start]**, selecione um modelo de fluxo de trabalho na lista.

1. (Opcional) Especifique um título para o fluxo de trabalho que pode ser usado para fazer referência à instância do fluxo de trabalho.

   ![selecione o fluxo de trabalho, forneça um título e clique em start](assets/start-workflow.png)

1. Clique em **[!UICONTROL Start]** e, em seguida, clique em **[!UICONTROL Prosseguir]**. Cada etapa do fluxo de trabalho é exibida na linha do tempo como um evento.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Aplicar um fluxo de trabalho a vários ativos {#applying-a-workflow-to-multiple-assets}

1. No console [!DNL Assets], navegue até o local dos ativos para os quais deseja start um fluxo de trabalho e selecione os ativos. Selecione **[!UICONTROL Linha do tempo]** no menu para exibir a linha do tempo.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Clique em **[!UICONTROL Ações]** ![divisa para cima](assets/do-not-localize/chevron-up-icon.png) na parte inferior.
1. Clique em **[!UICONTROL Fluxo de trabalho do Start]**. Na caixa de diálogo **[!UICONTROL Fluxo de trabalho do Start]**, selecione um modelo de fluxo de trabalho na lista.

   ![Fluxo de trabalho do start](assets/start-workflow.png)

1. (Opcional) Especifique um título para o fluxo de trabalho, que pode ser usado para fazer referência à instância do fluxo de trabalho.
1. Clique em **[!UICONTROL Iniciar]** e em **[!UICONTROL Confirmar]** na caixa de diálogo. O fluxo de trabalho é executado em todos os ativos selecionados.

## Aplicar um fluxo de trabalho a várias pastas {#applying-a-workflow-to-multiple-folders}

O procedimento para aplicar um fluxo de trabalho a várias pastas é semelhante ao procedimento para aplicar um fluxo de trabalho a vários ativos. Selecione as pastas na interface [!DNL Assets] e execute as etapas de 2 a 7 do procedimento [aplique um fluxo de trabalho a vários ativos](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Aplicar um fluxo de trabalho a uma coleção {#applying-a-workflow-to-a-collection}

Consulte [aplicar um fluxo de trabalho em uma coleção](/help/assets/manage-collections.md#running-a-workflow-on-a-collection).

## Start automático de um fluxo de trabalho para processar ativos condicionalmente {#auto-execute-workflow-on-some-assets}

Os administradores podem configurar o fluxo de trabalho para executar e processar automaticamente ativos com base em condições predefinidas. A funcionalidade é útil para usuários de linha de negócios e comerciantes, por exemplo, para criar fluxo de trabalho personalizado em pastas específicas. Diga que todos os ativos da fotografia de uma agência podem ter marca d&#39;água ou que todos os ativos carregados por um freelancer podem ser processados para criar representações específicas.

Para um modelo de fluxo de trabalho, os usuários podem criar um inicializador de fluxo de trabalho que o execute. Um iniciador de fluxo de trabalho monitora as alterações no repositório de conteúdo e executa o fluxo de trabalho quando as condições predefinidas são cumpridas. Os administradores podem fornecer acesso aos comerciantes para criar os workflows e configurar o iniciador. Os usuários podem modificar o fluxo de trabalho padrão [!UICONTROL DAM Update Asset] para adicionar as etapas adicionais necessárias para processar ativos específicos. O fluxo de trabalho é executado em todos os ativos carregados recentemente. Use uma das seguintes abordagens para limitar a execução das etapas extras em ativos específicos:

* Faça uma cópia do fluxo de trabalho [!UICONTROL DAM Update Asset] e modifique-o para ser executado em uma hierarquia de pastas específica. Essa abordagem é útil para algumas pastas.
* As etapas de processamento adicionais podem ser adicionadas usando um [OU split](/help/sites-developing/workflows-step-ref.md#or-split) como condicionalmente aplicável a quantas pastas forem necessárias.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* Considere suas necessidades para todos os tipos de execuções ao projetar workflows. Se você não prever a necessidade de uma representação no futuro, remova a etapa de criação do fluxo de trabalho. As execuções não podem ser excluídas em massa depois. As representações indesejadas podem ocupar muito espaço no armazenamento após o uso prolongado de [!DNL Experience Manager]. Para ativos individuais, você pode remover execuções manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e carregá-los novamente.
* Por padrão, o fluxo de trabalho [!UICONTROL DAM Update Asset] inclui algumas etapas para criar miniaturas e representações da Web. Se qualquer renderização padrão for removida do fluxo de trabalho, a interface do usuário de [!DNL Assets] não será renderizada corretamente.

>[!MORELIKETHIS]
>
>* [Aplicar e participar de workflows](/help/sites-authoring/workflows.md)
>* [Criar modelos de fluxo de trabalho e ampliar a funcionalidade do fluxo de trabalho](/help/sites-developing/workflows.md)
>* [Métodos para executar workflows](/help/sites-administering/workflows-starting.md)
>* [Práticas recomendadas de fluxo de trabalho](/help/sites-developing/workflows-best-practices.md)
>* [Artigo da comunidade sobre a modificação de ativos usando o fluxo de trabalho](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)


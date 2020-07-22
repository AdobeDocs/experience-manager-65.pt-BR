---
title: Processar ativos para realizar processos de negócios, realizar auditorias, atingir a conformidade e manter a sanidade básica
description: Processamento de ativos para converter formatos, criar execuções, gerenciar ativos, validar ativos e executar workflows.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 3%

---


# Processar ativos digitais {#process-assets}

[!DNL Adobe Experience Manager Assets] permite que você trabalhe com seus ativos digitais de várias maneiras para permitir um processamento robusto de ativos. Você pode usar os métodos de processamento padrão ou personalizado para garantir a conclusão completa dos processos de negócios, as auditorias e a conformidade, a descoberta e distribuição e a sanidade básica dos ativos digitais. Você pode fazer as tarefas de gerenciamento de ativos e, ao mesmo tempo, atingir a escala e a personalização necessárias.

## Entender workflows {#understand-workflows}

Para processamento de ativos, [!DNL Experience Manager] usa workflows. Os Workflows ajudam a automatizar a lógica comercial ou as atividades. As etapas granulares para realizar tarefas específicas são fornecidas por padrão e os desenvolvedores podem criar suas próprias etapas personalizadas. Essas etapas podem ser combinadas em uma ordem lógica para criar workflows. Por exemplo, um fluxo de trabalho pode aplicar uma marca d&#39;água em imagens carregadas com base em critérios específicos, como pasta para a qual é carregado, resolução da imagem e assim por diante. Outro exemplo é um fluxo de trabalho configurado para marca d&#39;água e, simultaneamente, adicionar metadados, criar execuções, adicionar tags inteligentes e publicar em um armazenamento de dados.

## workflows padrão disponíveis em [!DNL Experience Manager] {#default-workflows}

Por padrão, todos os ativos carregados são processados usando o fluxo de trabalho Atualizar ativo [!UICONTROL do] DAM. O fluxo de trabalho é executado para cada ativo carregado e realiza tarefas básicas de gerenciamento de ativos, como geração de representação, gravação de metadados, extração da página, extração de mídia e transcodificação.

Para ver os vários modelos de fluxo de trabalho disponíveis por padrão, consulte **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]** em [!DNL Experience Manager].

![Alguns dos fluxos de trabalho padrão](assets/aem-default-workflows.png)

*Figura: Alguns dos workflows padrão disponíveis em[!DNL Experience Manager].*

## Aplicar workflows para processar ativos {#applying-workflows-to-assets}

Aplicar workflows a ativos digitais é o mesmo que aplicar a páginas do site. Para obter um guia completo sobre como criar e usar workflows, consulte workflows [de](/help/sites-authoring/workflows-participating.md)start.

Use workflows em ativos digitais para ativar o ativo ou criar marcas d&#39;água. Muitos dos workflows dos ativos são ativados automaticamente. Por exemplo, o fluxo de trabalho que cria automaticamente uma representação depois que uma imagem é editada é ativado automaticamente.

>[!NOTE]
>
>Se um fluxo de trabalho disponível na interface clássica não estiver disponível na interface habilitada para toque, como [!UICONTROL Solicitar a ativação] e [!UICONTROL Solicitar a desativação], consulte [Criar modelos](/help/sites-developing/workflows-models.md#classic2touchui)de fluxo de trabalho.

## Aplicar um fluxo de trabalho a um ativo {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Para aplicar um fluxo de trabalho a um ativo, siga estas etapas:

1. Navegue até o local do ativo para o qual você deseja start um fluxo de trabalho e clique no ativo para abrir a página do ativo. Selecione **[!UICONTROL Linha]** do tempo no menu para exibir a linha do tempo.

   ![linha do tempo 1](assets/timeline.png)

1. Clique em **[!UICONTROL Ações]** na parte inferior para abrir a lista de ações disponíveis para o ativo.

1. Clique em Fluxo de trabalho **[!UICONTROL do]** Start na lista.

1. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-254](assets/chlimage_1-50.png)

1. (Opcional) Especifique um título para o fluxo de trabalho que pode ser usado para fazer referência à instância do fluxo de trabalho.

   ![chlimage_1-255](assets/chlimage_1-51.png)

1. Clique em **[!UICONTROL Start]** e em **[!UICONTROL Prosseguir]**. Cada etapa do fluxo de trabalho é exibida na linha do tempo como um evento.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Aplicar um fluxo de trabalho a vários ativos {#applying-a-workflow-to-multiple-assets}

1. No console Ativos, navegue até o local dos ativos para os quais deseja start um fluxo de trabalho e selecione os ativos. Selecione **[!UICONTROL Linha]** do tempo no menu para exibir a linha do tempo.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Clique em **[!UICONTROL Ações]** ![difundir](assets/do-not-localize/chevron-up-icon.png) na parte inferior.
1. Clique em Fluxo de trabalho do **[!UICONTROL Start]**. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-31](assets/chlimage_1-138.png)

1. (Opcional) Especifique um título para o fluxo de trabalho, que pode ser usado para fazer referência à instância do fluxo de trabalho.
1. Clique em **[!UICONTROL Iniciar]** e em **[!UICONTROL Confirmar]** na caixa de diálogo. O fluxo de trabalho é executado em todos os ativos selecionados.

## Aplicar um fluxo de trabalho a várias pastas {#applying-a-workflow-to-multiple-folders}

O procedimento para aplicar um fluxo de trabalho a várias pastas é semelhante ao procedimento para aplicar um fluxo de trabalho a vários ativos. Selecione as pastas na [!DNL Assets] interface e execute as etapas 2 a 7 do procedimento para [aplicar um fluxo de trabalho a vários ativos](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Aplicar um fluxo de trabalho a uma coleção {#applying-a-workflow-to-a-collection}

Consulte [aplicar um fluxo de trabalho em uma coleção](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection).

## start automático de um fluxo de trabalho para processar ativos condicionalmente {#auto-execute-workflow-on-some-assets}

Os administradores podem configurar o fluxo de trabalho para executar e processar automaticamente ativos com base em condições predefinidas. A funcionalidade é útil para usuários de linha de negócios e comerciantes, por exemplo, para criar fluxo de trabalho personalizado em pastas específicas. Diga que todos os ativos da fotografia de uma agência podem ter marca d&#39;água ou que todos os ativos carregados por um freelancer podem ser processados para criar representações específicas.

Para um modelo de fluxo de trabalho, os usuários podem criar um inicializador de fluxo de trabalho que o execute. Um iniciador de fluxo de trabalho monitora as alterações no repositório de conteúdo e executa o fluxo de trabalho quando as condições predefinidas são cumpridas. Os administradores podem fornecer acesso aos comerciantes para criar os workflows e configurar o iniciador. Os usuários podem modificar o fluxo de trabalho padrão do Ativo [!UICONTROL de atualização do] DAM para adicionar as etapas adicionais necessárias para processar ativos específicos. O fluxo de trabalho é executado em todos os ativos carregados recentemente. Use uma das seguintes abordagens para limitar a execução das etapas extras em ativos específicos:

* Faça uma cópia do fluxo de trabalho Atualizar ativo [!UICONTROL do] DAM e modifique-o para ser executado em uma hierarquia de pastas específica. Essa abordagem é útil para algumas pastas.
* As etapas de processamento adicionais podem ser adicionadas usando uma divisão [OU](/help/sites-developing/workflows-step-ref.md#or-split) , como aplicável condicionalmente a quantas pastas forem necessárias.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* Considere suas necessidades para todos os tipos de execuções ao projetar workflows. Se você não prever a necessidade de uma representação no futuro, remova a etapa de criação do fluxo de trabalho. As execuções não podem ser excluídas em massa depois. As representações indesejadas podem ocupar muito espaço no armazenamento após uso prolongado de [!DNL Experience Manager]. Para ativos individuais, você pode remover execuções manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e carregá-los novamente.
* Por padrão, o fluxo de trabalho Atualizar ativo [!UICONTROL do] DAM inclui algumas etapas para criar miniaturas e representações da Web. Se qualquer renderização padrão for removida do fluxo de trabalho, a interface do usuário do não [!DNL Assets] será renderizada corretamente.

>[!MORELIKETHIS]
>
>* [Aplicar e participar de workflows](/help/sites-authoring/workflows.md)
>* [Criar modelos de fluxo de trabalho e ampliar a funcionalidade do fluxo de trabalho](/help/sites-developing/workflows.md)
>* [Métodos para executar workflows](/help/sites-administering/workflows-starting.md)
>* [Práticas recomendadas de fluxo de trabalho](/help/sites-developing/workflows-best-practices.md)
>* [Artigo da comunidade sobre a modificação de ativos usando o fluxo de trabalho](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)


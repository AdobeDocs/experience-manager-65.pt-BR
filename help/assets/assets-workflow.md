---
title: Processar ativos usando fluxos de trabalho
description: Processamento de ativos para converter formatos, criar representações, gerenciar ativos, validar ativos e executar fluxos de trabalho.
contentOwner: AG
feature: Workflow, Renditions
role: User, Admin
exl-id: e7c84385-efb3-4997-83ff-7a7f31582469
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# Processar ativos digitais {#process-assets}

O [!DNL Adobe Experience Manager Assets] permite que você trabalhe com seus ativos digitais de várias maneiras para permitir um processamento de ativos robusto. Você pode usar os métodos de processamento padrão ou personalizados para garantir a conclusão completa do processo de negócios, auditorias e conformidade, detecção e distribuição, e a sanidade básica de seus ativos digitais. Você pode realizar as tarefas de gerenciamento de ativos enquanto atinge a escala e a personalização necessárias.

## Entender os fluxos de trabalho {#understand-workflows}

Para processamento de ativos, [!DNL Experience Manager] usa fluxos de trabalho. Os workflows ajudam a automatizar a lógica ou as atividades de negócios. Etapas granulares para realizar tarefas específicas são fornecidas por padrão e os desenvolvedores podem criar suas próprias etapas personalizadas. Essas etapas podem ser combinadas em uma ordem lógica para criar workflows. Por exemplo, um fluxo de trabalho pode aplicar uma marca d&#39;água às imagens carregadas com base em um critério específico, como pasta na qual é carregado, resolução da imagem e assim por diante. Outro exemplo é um fluxo de trabalho configurado para criar uma marca d&#39;água e adicionar metadados simultaneamente, criar representações, adicionar tags inteligentes e publicar em um armazenamento de dados.

## Fluxos de trabalho padrão disponíveis em [!DNL Experience Manager] {#default-workflows}

Por padrão, todos os ativos carregados são processados usando o fluxo de trabalho [!UICONTROL Ativo de atualização DAM]. O fluxo de trabalho é executado para cada ativo carregado e realiza tarefas básicas de gerenciamento de ativos, como geração de representação, write-back de metadados, extração de página, extração de mídia e transcodificação.

Para ver os vários modelos de fluxo de trabalho disponíveis por padrão, consulte **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]** em [!DNL Experience Manager].

![Algum do fluxo de trabalho padrão](assets/aem-default-workflows.png)

*Figura: alguns dos fluxos de trabalho padrão disponíveis em [!DNL Experience Manager].*

## Aplicar fluxos de trabalho para processar ativos {#applying-workflows-to-assets}

A aplicação de fluxos de trabalho a ativos digitais é a mesma para páginas do site. Para obter um guia completo sobre como criar e usar workflows, consulte [iniciar workflows](/help/sites-authoring/workflows-participating.md).

Use fluxos de trabalho em ativos digitais para ativar o ativo ou criar marcas d&#39;água. Muitos dos fluxos de trabalho de ativos são ativados automaticamente. Por exemplo, o fluxo de trabalho que cria automaticamente uma representação depois que uma imagem é editada é ativado automaticamente.

>[!NOTE]
>
>Se um fluxo de trabalho disponível na interface clássica não estiver disponível na interface habilitada para toque, como [!UICONTROL Solicitar Ativação] e [!UICONTROL Solicitar Desativação], consulte [criar modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md#classic2touchui).

## Aplicar um fluxo de trabalho a um ativo {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Para aplicar um fluxo de trabalho a um ativo, siga estas etapas:

1. Navegue até o local do ativo para o qual deseja iniciar um fluxo de trabalho e clique no ativo para abrir a página do ativo. Selecione **[!UICONTROL Linha do tempo]** no menu para exibir a linha do tempo.

   ![linha do tempo-1](assets/timeline.png)

1. Clique em **[!UICONTROL Ações]** na parte inferior para abrir a lista de ações disponíveis para o ativo.

1. Clique em **[!UICONTROL Iniciar Fluxo de Trabalho]** na lista.

1. Na caixa de diálogo **[!UICONTROL Iniciar Fluxo de Trabalho]**, selecione um modelo de fluxo de trabalho da lista.

1. (Opcional) Especifique um título para o workflow que possa ser usado para fazer referência à instância do workflow.

   ![selecione o fluxo de trabalho, forneça um título e clique em iniciar](assets/start-workflow.png)

1. Clique em **[!UICONTROL Iniciar]** e em **[!UICONTROL Continuar]**. Cada etapa do fluxo de trabalho é exibida na linha do tempo como um evento.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Aplicar um fluxo de trabalho a vários ativos {#applying-a-workflow-to-multiple-assets}

1. No console [!DNL Assets], navegue até o local dos ativos para os quais deseja iniciar um fluxo de trabalho e selecione os ativos. Selecione **[!UICONTROL Linha do tempo]** no menu para exibir a linha do tempo.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Clique em **[!UICONTROL Ações]** ![divisa para cima](assets/do-not-localize/chevron-up-icon.png) na parte inferior.
1. Clique em **[!UICONTROL Iniciar Fluxo de Trabalho]**. Na caixa de diálogo **[!UICONTROL Iniciar Fluxo de Trabalho]**, selecione um modelo de fluxo de trabalho da lista.

   ![iniciar fluxo de trabalho](assets/start-workflow.png)

1. (Opcional) Especifique um título para o workflow, que pode ser usado para fazer referência à instância do workflow.
1. Clique em **[!UICONTROL Iniciar]** e em **[!UICONTROL Confirmar]** na caixa de diálogo. O fluxo de trabalho é executado em todos os ativos selecionados.

## Aplicar um fluxo de trabalho a várias pastas {#applying-a-workflow-to-multiple-folders}

O procedimento para aplicar um fluxo de trabalho a várias pastas é semelhante ao procedimento para aplicar um fluxo de trabalho a vários ativos. Selecione as pastas na interface [!DNL Assets] e execute as etapas 2 a 7 do procedimento [aplicar um fluxo de trabalho a vários ativos](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Aplicar um fluxo de trabalho a uma coleção {#applying-a-workflow-to-a-collection}

Consulte [aplicar um fluxo de trabalho a uma coleção](/help/assets/manage-collections.md#running-a-workflow-on-a-collection).

## Iniciar automaticamente um fluxo de trabalho para processar ativos condicionalmente {#auto-execute-workflow-on-some-assets}

Os administradores podem configurar o fluxo de trabalho para executar e processar ativos automaticamente com base em condições predefinidas. A funcionalidade é útil para usuários e profissionais de marketing da linha de negócios, por exemplo, para criar um fluxo de trabalho personalizado em pastas específicas. Digamos que todos os ativos da sessão de fotos de uma agência possam ter uma marca d&#39;água ou que todos os ativos carregados por um freelancer possam ser processados para criar representações específicas.

Para um modelo de fluxo de trabalho, os usuários podem criar um iniciador de fluxo de trabalho que o execute. Um iniciador de fluxo de trabalho monitora alterações no repositório de conteúdo e executa o fluxo de trabalho quando as condições predefinidas são atendidas. Os administradores podem fornecer acesso aos profissionais de marketing para criar os fluxos de trabalho e configurar o Launch. Os usuários podem modificar o fluxo de trabalho padrão [!UICONTROL Ativo de atualização do DAM] para adicionar as etapas extras necessárias para processar ativos específicos. O fluxo de trabalho é executado em todos os ativos carregados recentemente. Use uma das seguintes abordagens para limitar a execução das etapas adicionais em ativos específicos:

* Faça uma cópia do fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] e modifique-o para ser executado em uma hierarquia de pastas específica. Essa abordagem é útil para algumas pastas.
* As etapas de processamento adicionais podem ser adicionadas usando uma [OU divisão](/help/sites-developing/workflows-step-ref.md#or-split) conforme condicionalmente aplicável a quantas pastas forem necessárias.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* Considere suas necessidades para todos os tipos de representações ao criar workflows. Se você não prever a necessidade de uma representação no futuro, remova a etapa de criação do fluxo de trabalho. As representações não podem ser excluídas em massa posteriormente. As representações indesejadas podem ocupar espaço de armazenamento após o uso prolongado de [!DNL Experience Manager]. Para ativos individuais, é possível remover representações manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e carregá-los novamente.
* Por padrão, o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] inclui algumas etapas para criar miniaturas e representações da Web. Se qualquer representação padrão for removida do fluxo de trabalho, a interface de usuário do [!DNL Assets] não será renderizada corretamente.

>[!MORELIKETHIS]
>
>* [Aplicar e participar de fluxos de trabalho](/help/sites-authoring/workflows.md)
>* [Criar modelos de fluxo de trabalho e estender a funcionalidade do fluxo de trabalho](/help/sites-developing/workflows.md)
>* [Métodos para executar fluxos de trabalho](/help/sites-administering/workflows-starting.md)
>* [Práticas recomendadas de fluxo de trabalho](/help/sites-developing/workflows-best-practices.md)

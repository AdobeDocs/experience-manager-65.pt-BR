---
title: Ativos relacionados
description: Saiba como relacionar ativos digitais que compartilham alguns atributos comuns. Além disso, crie relacionamentos derivados da origem entre ativos digitais.
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Ativos relacionados {#related-assets}

[!DNL Adobe Experience Manager Assets] permite relacionar ativos manualmente com base nas necessidades da organização usando o recurso de ativos relacionados. Por exemplo, você pode relacionar um arquivo de licença com um ativo ou uma imagem/vídeo em um tópico semelhante. Você pode relacionar ativos que compartilham determinados atributos comuns. Também é possível usar o recurso para criar relacionamentos de origem/derivados entre ativos. Por exemplo, se você tiver um arquivo PDF gerado a partir de um arquivo INDD, poderá relacionar o arquivo PDF ao seu arquivo INDD de origem.

Com esse recurso, você tem a flexibilidade de compartilhar um arquivo PDF ou JPG de baixa resolução com fornecedores ou agências e disponibilizar o arquivo INDD de alta resolução somente mediante solicitação.

>[!NOTE]
>
>Somente os usuários com permissões de edição em ativos podem relacionar e desvincular os ativos.

## Relacionar ativos {#relating-assets}

1. No [!DNL Experience Manager] , abra o **[!UICONTROL Propriedades]** página de um ativo que você deseja relacionar.

   ![abra a página Propriedades de um ativo para relacionar o ativo](assets/asset-properties-relate-assets.png)

   *Figura: [!DNL Assets] [!UICONTROL Propriedades] página para relacionar ativos.*

   Como alternativa, selecione o ativo na exibição em lista.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Você também pode selecionar o ativo de uma coleção.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Para relacionar outro ativo com o ativo selecionado, clique em **[!UICONTROL Relacionar]** ![ativos relacionados](assets/do-not-localize/link-relate.png) na barra de ferramentas.
1. Siga uma das seguintes opções:

   * Para relacionar o arquivo de origem do ativo, selecione **[!UICONTROL Origem]** na lista.
   * Para relacionar um arquivo derivado, selecione **[!UICONTROL Derivado]** na lista.
   * Para criar um relacionamento bidirecional entre os ativos, selecione **[!UICONTROL Outros]** na lista.

1. No **[!UICONTROL Selecionar ativo]** , navegue até o local do ativo que deseja relacionar e selecione-o.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Clique em **[!UICONTROL Confirmar]**.
1. Clique em **[!UICONTROL OK]** para fechar a caixa de diálogo. Dependendo da escolha do relacionamento na etapa 3, o ativo relacionado é listado em uma categoria apropriada na **[!UICONTROL Relacionado]** seção. Por exemplo, se o ativo relacionado for o arquivo de origem do ativo atual, ele será listado em **[!UICONTROL Origem]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Para desrelacionar um ativo, clique em **[!UICONTROL Não relacionado]** ![ativos não relacionados](assets/do-not-localize/link-unrelate-icon.png) na barra de ferramentas.

1. Selecione o(s) ativo(s) que deseja desrelacionar da variável **[!UICONTROL Remover Relações]** e clique em **[!UICONTROL Não relacionado]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Clique em **[!UICONTROL OK]** para fechar a caixa de diálogo. Os ativos para os quais você removeu relações são excluídos da lista de ativos relacionados na **[!UICONTROL Relacionado]** seção.

## Traduzir ativos relacionados {#translating-related-assets}

Criar relacionamentos de origem/derivados entre ativos usando o recurso de ativos relacionados também é útil em fluxos de trabalho de tradução. Ao executar um fluxo de trabalho de tradução em um ativo derivado, [!DNL Experience Manager Assets] O busca automaticamente qualquer ativo que o arquivo de origem faça referência e o inclui para tradução. Dessa forma, o ativo referenciado pelo ativo de origem é convertido junto com a fonte e os ativos derivados. Por exemplo, considere um cenário em que a cópia em inglês inclua um ativo derivado e o arquivo de origem, como mostrado.

![chlimage_1-281](assets/chlimage_1-281.png)

Se o arquivo de origem estiver relacionado a outro ativo, [!DNL Experience Manager Assets] busca o ativo referenciado e o inclui para tradução.

![a página Propriedades do ativo mostra o arquivo de origem do ativo relacionado a ser incluído para tradução](assets/asset-properties-source-asset.png)

*Figura: Ativo de origem dos ativos relacionados a serem incluídos para tradução.*

1. Traduza os ativos na pasta de origem para um idioma de destino seguindo as etapas em [Criar um novo projeto de tradução](translation-projects.md#create-a-new-translation-project). Por exemplo, nesse caso, traduza os ativos para francês.

1. No [!UICONTROL Projetos] abra a pasta de tradução.

1. Clique no bloco do projeto para abrir a página de detalhes.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Clique nas reticências abaixo do cartão Tarefa de tradução para visualizar o status da tradução.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Selecione o ativo e clique em **[!UICONTROL Receita em ativos]** na barra de ferramentas para exibir o status de tradução do ativo.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Para verificar se os ativos relacionados à origem foram traduzidos, clique no ativo de origem.

1. Selecione o ativo que está relacionado à origem e clique em **[!UICONTROL Receita em ativos]**. O ativo relacionado convertido é exibido.

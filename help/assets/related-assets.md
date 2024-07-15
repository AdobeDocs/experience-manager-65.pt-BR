---
title: Ativos relacionados
description: Saiba como relacionar ativos digitais que compartilham alguns atributos comuns. Além disso, crie relacionamentos derivados da origem entre ativos digitais.
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Ativos relacionados {#related-assets}

O [!DNL Adobe Experience Manager Assets] permite relacionar ativos manualmente com base nas necessidades da sua organização usando o recurso de ativos relacionados. Por exemplo, você pode relacionar um arquivo de licença a um ativo ou uma imagem/vídeo em um tópico semelhante. Você pode relacionar ativos que compartilham determinados atributos comuns. Você também pode usar o recurso para criar relacionamentos de origem/derivados entre ativos. Por exemplo, se você tiver um arquivo PDF gerado a partir de um arquivo INDD, poderá relacionar o arquivo PDF ao seu arquivo INDD de origem.

Usando esse recurso, você tem a flexibilidade de compartilhar um arquivo PDF ou JPG de baixa resolução com fornecedores ou agências e disponibilizar o arquivo INDD de alta resolução somente mediante solicitação.

>[!NOTE]
>
>Somente os usuários com permissões de edição em ativos podem relacionar e não relacionar os ativos.

## Relacionar ativos {#relating-assets}

1. Na interface [!DNL Experience Manager], abra a página **[!UICONTROL Propriedades]** de um ativo que você deseja relacionar.

   ![abra a página Propriedades de um ativo para relacionar o ativo](assets/asset-properties-relate-assets.png)

   *Figura: página [!DNL Assets] [!UICONTROL Propriedades] para relacionar ativos.*

   Como alternativa, selecione o ativo na exibição em lista.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Você também pode selecionar o ativo de uma coleção.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Para relacionar outro ativo ao ativo selecionado, clique em **[!UICONTROL Relacionar]** ![relacionar ativos](assets/do-not-localize/link-relate.png) na barra de ferramentas.
1. Siga uma das seguintes opções:

   * Para relacionar o arquivo de origem do ativo, selecione **[!UICONTROL Source]** na lista.
   * Para relacionar um arquivo derivado, selecione **[!UICONTROL Derivado]** na lista.
   * Para criar uma relação bidirecional entre os ativos, selecione **[!UICONTROL Outros]** na lista.

1. Na tela **[!UICONTROL Selecionar ativo]**, navegue até o local do ativo que deseja relacionar e selecione-o.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Clique em **[!UICONTROL Confirmar]**.
1. Clique em **[!UICONTROL OK]** para fechar a caixa de diálogo. Dependendo da sua escolha de relação na etapa 3, o ativo relacionado é listado em uma categoria apropriada na seção **[!UICONTROL Relacionado]**. Por exemplo, se o ativo relacionado for o arquivo de origem do ativo atual, ele será listado em **[!UICONTROL Source]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Para desrelacionar um ativo, clique em **[!UICONTROL Desrelacionar]** ![desrelacionar ativos](assets/do-not-localize/link-unrelate-icon.png) da barra de ferramentas.

1. Selecione os ativos que deseja cancelar a relação na caixa de diálogo **[!UICONTROL Remover Relações]** e clique em **[!UICONTROL Cancelar Relação]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Clique em **[!UICONTROL OK]** para fechar a caixa de diálogo. Os ativos cujas relações você removeu são excluídos da lista de ativos relacionados na seção **[!UICONTROL Relacionados]**.

## Traduzir ativos relacionados {#translating-related-assets}

Criar relacionamentos de origem/derivados entre ativos usando o recurso de ativos relacionados também é útil em fluxos de trabalho de tradução. Quando você executa um fluxo de trabalho de tradução em um ativo derivado, o [!DNL Experience Manager Assets] busca automaticamente qualquer ativo ao qual o arquivo de origem faça referência e o inclui para tradução. Dessa forma, o ativo referenciado pelo ativo de origem é traduzido junto com os ativos de origem e derivados. Por exemplo, considere um cenário em que sua cópia em inglês inclua um ativo derivado e seu arquivo de origem, como mostrado.

![chlimage_1-281](assets/chlimage_1-281.png)

Se o arquivo de origem estiver relacionado a outro ativo, [!DNL Experience Manager Assets] buscará o ativo referenciado e o incluirá para tradução.

A página ![Propriedades do ativo mostra o arquivo de origem do ativo relacionado a ser incluído para tradução](assets/asset-properties-source-asset.png)

*Figura: ativo Source dos ativos relacionados a serem incluídos para tradução.*

1. Traduza os ativos na pasta de origem para um idioma de destino seguindo as etapas em [Criar um projeto de tradução](translation-projects.md#create-a-new-translation-project). Por exemplo, neste caso, traduza seus ativos para francês.

1. Na página [!UICONTROL Projetos], abra a pasta de tradução.

1. Clique no bloco do projeto para abrir a página de detalhes.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Clique nas reticências abaixo do cartão Tarefa de tradução para exibir o status da tradução.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Selecione o ativo e clique em **[!UICONTROL Revelar no Assets]** na barra de ferramentas para exibir o status de tradução do ativo.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Para verificar se os ativos relacionados à origem foram traduzidos, clique no ativo de origem.

1. Selecione o ativo relacionado à origem e clique em **[!UICONTROL Revelar no Assets]**. O ativo relacionado traduzido é exibido.

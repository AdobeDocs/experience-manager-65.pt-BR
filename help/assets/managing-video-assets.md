---
title: Gerenciar ativos de vídeo
description: Fazer upload, visualizar, anotar e publicar ativos de vídeo em [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 8%

---

# Gerenciar ativos de vídeo {#manage-video-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/managing-video-assets.html?lang=en) |

O formato de vídeo é uma parte essencial dos ativos digitais de uma organização. [!DNL Adobe Experience Manager] O oferece ofertas e recursos maduros para gerenciar todo o ciclo de vida dos ativos de vídeo após sua criação.

Saiba como gerenciar e editar os ativos de vídeo em [!DNL Adobe Experience Manager Assets]. A codificação e a transcodificação de vídeo, por exemplo, a transcodificação FFmpeg, é possível usando [!DNL Dynamic Media] integração.

## Fazer upload e visualizar ativos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] gera visualizações para ativos de vídeo com a extensão MP4. Se o formato do ativo não for MP4, instale o FFmpeg pack para gerar uma pré-visualização. FFmpeg cria representações de vídeo do tipo OGG e MP4. Você pode visualizar as representações no [!DNL Assets] interface do usuário.

1. Na pasta ou nas subpastas de ativos digitais, navegue até o local onde deseja adicionar ativos digitais.
1. Para fazer upload do ativo, clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Arquivos]**. Como alternativa, arraste um arquivo na interface do usuário do . Consulte [fazer upload de ativos](manage-assets.md#uploading-assets) para obter detalhes.
1. Para visualizar um vídeo na exibição de Cartão, clique no botão **[!UICONTROL Reproduzir]** ![opção de reprodução](assets/do-not-localize/play.png) no ativo de vídeo. Você pode pausar ou reproduzir vídeo somente na exibição de cartão. O [!UICONTROL Reproduzir] e [!UICONTROL Pausar] não estão disponíveis na exibição de lista.

1. Para visualizar o vídeo na página de detalhes do ativo, clique em **[!UICONTROL Editar]** no cartão. O vídeo é reproduzido no player de vídeo nativo do navegador. Você pode reproduzir, pausar, controlar o volume e aplicar zoom ao vídeo em tela cheia.

   ![Controles de reprodução de vídeo](assets/video-playback-controls.png)

## Configuração para fazer upload de ativos com mais de 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Por padrão, [!DNL Assets] O não permite fazer upload de ativos com mais de 2 GB por causa de um limite de tamanho de arquivo. No entanto, é possível substituir esse limite indo até o CRXDE Lite e criando um nó sob o `/apps` diretório. O nó deve ter o mesmo nome de nó, estrutura de diretório e propriedades de nó comparáveis da ordem.

Além de [!DNL Assets] altere as seguintes configurações para fazer upload de ativos grandes:

* Aumente o tempo de expiração do token. Consulte [!UICONTROL Servlet CSRF do Adobe Granite] no Console da Web em `https://[aem_server]:[port]/system/console/configMgr`. Para obter mais informações, consulte [Proteção CSRF](/help/sites-developing/csrf-protection.md).
* Aumente o `receiveTimeout` na configuração do Dispatcher. Para obter mais informações, consulte [Configuração do Dispatcher do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>O [!DNL Experience Manager] A interface de usuário clássica não tem uma restrição de limite de tamanho de arquivo de 2 GB. Além disso, o fluxo de trabalho completo para vídeo grande não é totalmente compatível.

Para configurar um limite de tamanho de arquivo mais alto, execute as seguintes etapas no `/apps` diretório.

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. No CRXDE Lite, navegue até `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Para ver a janela do diretório, clique no botão `>>`.
1. Na barra de ferramentas, clique no botão **[!UICONTROL Nó de sobreposição]**. Como alternativa, selecione **[!UICONTROL Sobrepor nó]** no menu de contexto.
1. No **[!UICONTROL Nó de sobreposição]** , clique em **[!UICONTROL OK]**.

   ![Nó de sobreposição](assets/overlay-node-path.png)

1. Atualize o navegador. O nó de sobreposição `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` está selecionada.
1. No **[!UICONTROL Propriedades]** , insira o valor apropriado em bytes para aumentar o limite de tamanho para o tamanho desejado. Por exemplo, para aumentar o limite de tamanho para 30 GB, insira `32212254720` valor.

1. Na barra de ferramentas, clique em **[!UICONTROL Salvar tudo]**.
1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. No [!DNL Adobe Experience Manager] [!UICONTROL Pacotes do Console da Web] na coluna Nome da tabela, localize e clique em **[!UICONTROL Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite]**.
1. No [!UICONTROL Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite] , defina os segundos para ambos **[!UICONTROL Tempo limite padrão]** e **[!UICONTROL Tempo limite máximo]** campos para `18000` (cinco horas). Clique em **[!UICONTROL Salvar]**.
1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos de fluxo de trabalho , selecione **[!UICONTROL Codificar vídeo no Dynamic Media]**, depois clique em **[!UICONTROL Editar]**.
1. Na página do fluxo de trabalho , clique duas vezes no botão **[!UICONTROL Processo de serviço de vídeo do Dynamic Media]** componente.
1. Na caixa de diálogo [!UICONTROL Propriedades da etapa], na guia **[!UICONTROL Comum]**, expanda **Configurações avançadas**.
1. No **[!UICONTROL Tempo limite]** , especifique um valor de `18000`, depois clique em **[!UICONTROL OK]** para retornar ao **[!UICONTROL Codificar vídeo no Dynamic Media]** página do fluxo de trabalho.
1. Próximo à parte superior da página, abaixo do [!UICONTROL Codificar vídeo no Dynamic Media] título da página, clique em **[!UICONTROL Salvar]**.

## Publicar ativos de vídeo {#publish-video-assets}

Após a publicação, é possível incluir os ativos de vídeo em uma página da Web como um URL ou incorporar diretamente os ativos. Para obter detalhes, consulte [publicar ativos do Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md).

## Anotar ativos de vídeo {#annotate-video-assets}

1. No [!DNL Assets] , selecione **[!UICONTROL Editar]** no cartão de ativos para exibir a página de detalhes do ativo.
1. Para reproduzir o vídeo, clique em **[!UICONTROL Visualizar]**.
1. Para anotar o vídeo, clique em **[!UICONTROL Anotar]**. Uma anotação é adicionada no horário específico (quadro) do vídeo. Ao fazer anotações, você pode desenhar na tela e incluir um comentário com o desenho. Os comentários são salvos automaticamente. Para sair do assistente de anotação, clique em **[!UICONTROL Fechar]**.

   ![Desenhar e anotar em um quadro de vídeo](assets/annotate-video.png)

1. Procure um ponto específico no vídeo, especifique o tempo em segundos no campo de **texto** e clique em **Pular**. Por exemplo, para pular os primeiros 20 segundos de vídeo, digite 20 no campo de texto.

   ![Procure um horário em um vídeo para ignorar em segundos específicos](assets/seek-in-video.png)

1. Para exibi-la na linha do tempo, clique em uma anotação. Para excluir a anotação da linha do tempo, clique em **[!UICONTROL Excluir]**.

   ![Exibir anotações e detalhes na linha do tempo](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Gerenciar ativos digitais no Experience Manager Assets](/help/assets/manage-assets.md)
>* [Gerenciar coleções no Experience Manager Assets](/help/assets/manage-collections.md)
>* [Documentação de vídeo do Dynamic Media](/help/assets/video.md).


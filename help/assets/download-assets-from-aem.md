---
title: Baixar ativos
description: Saiba como baixar ativos [!DNL Adobe Experience Manager] e ativar ou desativar a funcionalidade de download.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 3%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Você pode baixar ativos, incluindo representações estáticas e dinâmicas. Como alternativa, você pode enviar emails com links para ativos diretamente de [!DNL Adobe Experience Manager Assets]. Os ativos baixados são agrupados em um arquivo ZIP. O arquivo ZIP compactado tem um tamanho máximo de 1 GB para o trabalho de exportação. São permitidos no máximo 500 ativos por trabalho de exportação.

>[!NOTE]
>
>Recipient de e-mails devem ser membros do `dam-users` grupo para acessar o link de download ZIP na mensagem de e-mail. Para poder baixar os ativos, os membros devem ter permissões para iniciar workflows que acionam o download de ativos.

Os tipos de ativos Conjuntos de imagens, Conjuntos de rotação, Conjuntos de mídia mista e Conjuntos de carrossel não podem ser baixados.

Para baixar ativos, siga estas etapas:

1. No canto superior esquerdo, clique no logotipo. In the left rail, click **[!UICONTROL Navigation]**.
1. Na página [!UICONTROL Navegação] , clique em **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos.]**
1. Navegue até uma pasta que contenha ativos que você deseja baixar.
1. Selecione a pasta ou selecione um ou mais ativos na pasta.
1. Na barra de ferramentas, clique em **[!UICONTROL Download.]**

   ![Opções disponíveis ao baixar ativos dos ativos Experience Manager](/help/assets/assets/asset-download1.png)

   *Figura: Opções disponíveis na caixa de diálogo de download.*

1. Na caixa de diálogo Download, selecione as opções de download desejadas.

   | Opção Exportar ou baixar | Descrição |
   |---|---|
   | **[!UICONTROL Criar uma pasta separada para cada ativo]** | Selecione essa opção para incluir cada ativo que você baixar, incluindo ativos em pastas filhas aninhadas sob a pasta pai do ativo, em uma pasta no computador local. Quando essa opção não é selecionada, por padrão, a hierarquia de pastas é ignorada e todos os ativos são baixados em uma pasta no computador local. |
   | **[!UICONTROL E-mail]** | Uma notificação por email é enviada ao usuário. Os modelos padrão de e-mails estão disponíveis nos seguintes locais:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Os modelos que você personaliza durante a implantação estão disponíveis nos seguintes locais: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Você pode armazenar modelos personalizados específicos do locatário nos seguintes locais:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ativo(s)]** | Selecione essa opção para baixar o ativo em seu formulário original sem execuções.<br>A opção de subativos estará disponível se o ativo original tiver subativos. |
   | **[!UICONTROL Representações]** | Uma representação é uma representação binária de um ativo. Os ativos têm uma representação principal - a do arquivo carregado. Podem ter qualquer número de representações. <br> Com essa opção, você pode selecionar as representações que deseja baixar. As representações disponíveis dependem do ativo selecionado. A opção estará disponível se o ativo tiver representações. |
   | **[!UICONTROL Cortes inteligentes]** | Selecione essa opção para baixar todas as representações de recorte inteligente do ativo selecionado no AEM. Um arquivo zip com as execuções de Recorte inteligente é criado e baixado no computador local. |
   | **[!UICONTROL Execução(ões) dinâmica(s)]** | Selecione essa opção para gerar uma série de representações alternativas em tempo real. Ao selecionar essa opção, você também seleciona as representações que deseja criar dinamicamente selecionando na lista [Predefinição](image-presets.md) de imagem. <br>Além disso, é possível selecionar o tamanho e a unidade de medida, o formato, o espaço de cor, a resolução e qualquer modificador de imagem opcional, como inverter a imagem. A opção só estará disponível se você tiver [!DNL Dynamic Media] ativado. |

1. Na caixa de diálogo, clique em **[!UICONTROL Download.]**.

Quando você seleciona uma pasta para download, a hierarquia completa de ativos na pasta é baixada. Para incluir cada ativo baixado (incluindo ativos em pastas filhas aninhadas sob a pasta pai) em uma pasta individual, selecione **[!UICONTROL Criar pasta separada para cada ativo]**.

## Ativar servlet de download de ativos {#enable-asset-download-servlet}

O servlet padrão [!DNL Experience Manager] permite que os usuários autenticados emitam solicitações de download simultâneas e arbitrariamente grandes para criar arquivos ZIP de ativos visíveis a eles que podem sobrecarregar o servidor e a rede. Para atenuar os possíveis riscos de DoS causados por esse recurso, o componente `AssetDownloadServlet` OSGi é desabilitado por padrão para instâncias de publicação.

Para permitir o download de ativos do DAM, digamos ao usar algo como o Asset Share Commons ou outra implementação semelhante ao portal, ative manualmente o servlet por meio de uma configuração OSGi. O Adobe recomenda que o tamanho de download permitido seja o mais baixo possível, sem afetar os requisitos diários de download. Um valor alto pode afetar o desempenho.

1. Crie uma pasta com uma convenção de nomenclatura que público alvo o modo de execução de publicação (`config.publish`): `/apps/<your-app-name>/config.publish`. Para definir as propriedades de configuração para um modo de execução, consulte Modos [de execução](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. Na pasta de configuração, crie um arquivo do tipo `nt:file` chamado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Preencha `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` com o seguinte. Define um tamanho máximo (em bytes) para o download como valor de `asset.download.prezip.maxcontentsize`. A amostra abaixo configura o tamanho máximo do download ZIP para não exceder 100 kB.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Desativar o servlet de download de ativos {#disable-asset-download-servlet}

O `Asset Download Servlet` pode ser desativado em instâncias de [!DNL Experience Manager] Publicação atualizando a configuração do dispatcher para bloquear quaisquer solicitações de download de ativos. O servlet também pode ser desabilitado manualmente por meio do console OSGi diretamente.

1. Para bloquear as solicitações de download de ativos por meio de uma configuração de despachante, edite a `dispatcher.any` configuração e adicione uma regra à seção [de](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)filtro. `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Para desativar o componente OSGi em uma instância de publicação, acesse o console OSGi em `http://[aem_server]:[port]/system/console/components`. Localize `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` e clique em **[!UICONTROL Desativar]**.

>[!MORELIKETHIS]
>
>* [Baixar ativos usando o Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [Baixe ativos](drm.md)protegidos por DRM.
>* [Baixe ativos usando o aplicativo de desktop Experience Manager no desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#download-assets)Win ou Mac.
>* [Baixe ativos usando o Link de ativos Adobe nos aplicativos](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html)Adobe Creative Cloud suportados.


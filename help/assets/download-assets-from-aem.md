---
title: Baixe ativos digitais [!DNL Adobe Experience Manager].
description: Saiba como baixar ativos [!DNL Adobe Experience Manager] e ativar ou desativar a funcionalidade de download.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 3%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Você pode baixar ativos, incluindo representações estáticas e dinâmicas. Como alternativa, você pode enviar emails com links para ativos diretamente de [!DNL Adobe Experience Manager Assets]. Os ativos baixados são agrupados em um arquivo ZIP. O arquivo ZIP compactado tem um tamanho máximo de 1 GB para o trabalho de exportação. São permitidos no máximo 500 ativos por trabalho de exportação.

>[!NOTE]
>
>Recipient de e-mails devem ser membros do `dam-users` grupo para acessar o link de download ZIP na mensagem de e-mail. Para poder baixar os ativos, os membros devem ter permissões para iniciar workflows que acionam o download de ativos.

Os tipos de ativos Conjuntos de imagens, Conjuntos de rotação, Conjuntos de mídia mista e Conjuntos de carrossel não podem ser baixados.

**Para baixar ativos,**

1. No canto superior esquerdo do AEM, toque no logotipo do AEM e, no painel esquerdo, toque em **[!UICONTROL Navegação]**.
1. Na página Navegação, toque em **[!UICONTROL Ativos > Arquivos.]**
1. Navegue até uma pasta que contenha ativos que você deseja baixar.
1. Selecione a pasta ou selecione um ou mais ativos na pasta.
1. Na barra de ferramentas, toque em **[!UICONTROL Download.]**

   ![Opções disponíveis ao baixar ativos dos ativos Experience Manager](/help/assets/assets/asset-download1.png)

   *Opções da caixa de diálogo de download.*

1. Na caixa de diálogo Download, selecione as opções de download desejadas.

   | Opção de download | Descrição |
   |---|---|
   | **[!UICONTROL Criar uma pasta separada para cada ativo]** | Selecione essa opção para incluir cada ativo que você baixar, incluindo ativos em pastas filhas aninhadas sob a pasta pai do ativo, em uma pasta no computador local. Quando essa opção *não* é selecionada, por padrão, a hierarquia de pastas é ignorada e todos os ativos são baixados em uma pasta no computador local. |
   | **[!UICONTROL E-mail]** | Selecione essa opção para que uma notificação por email seja enviada ao recipient. Os modelos padrão de e-mails estão disponíveis nos seguintes locais:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Os modelos que você personaliza durante a implantação estão disponíveis nos seguintes locais: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Você pode armazenar modelos personalizados específicos do locatário nos seguintes locais:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ativo(s)]** | Selecione essa opção para baixar o ativo em seu formulário original sem execuções.<br>A opção de subativos estará disponível se o ativo original tiver subativos. |
   | **[!UICONTROL Representações]** | Uma representação é uma representação binária de um ativo. Os ativos têm uma representação principal - a do arquivo carregado. Podem ter qualquer número de representações. <br> Com essa opção, você pode selecionar as representações que deseja baixar. As representações disponíveis dependem do ativo selecionado. |
   | **[!UICONTROL Cortes inteligentes]** | Selecione essa opção para baixar todas as representações de recorte inteligente do ativo selecionado no AEM. Um arquivo zip com as execuções de Recorte inteligente é criado e baixado no computador local. |
   | **[!UICONTROL Execução(ões) dinâmica(s)]** | Selecione essa opção para gerar uma série de representações alternativas em tempo real. Ao selecionar essa opção, você também seleciona as representações que deseja criar dinamicamente selecionando na lista [Predefinição](image-presets.md) de imagem. <br>Além disso, é possível selecionar o tamanho e a unidade de medida, o formato, o espaço de cor, a resolução e qualquer modificador de imagem opcional, como inverter a imagem. A opção só estará disponível se você tiver [!DNL Dynamic Media] ativado. |

1. Na caixa de diálogo, toque em **[!UICONTROL Download.]**.

## Ativar servlet de download de ativos {#enable-asset-download-servlet}

O servlet padrão [!DNL Experience Manager] permite que os usuários autenticados emitam solicitações de download simultâneas e arbitrariamente grandes para criar arquivos ZIP de ativos visíveis a eles que podem sobrecarregar o servidor e a rede. Para atenuar os possíveis riscos de DoS causados por esse recurso, o componente `AssetDownloadServlet` OSGi é desabilitado por padrão para instâncias de publicação.

Para permitir o download de ativos do DAM, digamos ao usar algo como o Asset Share Commons ou outra implementação semelhante ao portal, ative manualmente o servlet por meio de uma configuração OSGi. A Adobe recomenda definir o tamanho de download permitido o mais baixo possível sem afetar os requisitos diários de download. Um valor alto pode afetar o desempenho.

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

1. Desative o componente OSGi em uma instância de Publicação navegando até o console OSGi em `http://[aem_server]:[port]/system/console/components`. Localize `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` e clique em **[!UICONTROL Desativar]**.

>[!MORELIKETHIS]
>
>* [Baixe ativos](drm.md)protegidos por DRM.
>* [Baixe ativos usando o aplicativo de desktop Experience Manager no desktop](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)Win ou Mac.
>* [Baixe ativos usando o Adobe Assets Link dos aplicativos](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html)da Adobe Creative Cloud compatíveis.


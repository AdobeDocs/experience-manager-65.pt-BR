---
title: Baixar ativos
description: Saiba como baixar ativos do  [!DNL Adobe Experience Manager]  e habilitar ou desabilitar a funcionalidade de download.
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 2%

---

# Baixar ativos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | Este artigo |

É possível baixar ativos, incluindo representações estáticas e dinâmicas. Como alternativa, você pode enviar emails com links para ativos diretamente do [!DNL Adobe Experience Manager Assets]. Os ativos baixados são incluídos em um arquivo ZIP. O arquivo ZIP compactado tem um tamanho máximo de arquivo de 1 GB para o trabalho de exportação. Um máximo de 500 ativos totais por trabalho de exportação são permitidos.

>[!NOTE]
>
>Qualquer usuário com permissões de leitura no local `/var/dam/share` pode acessar o link de download compartilhado na mensagem de email.
>
>Qualquer usuário com permissões de leitura para o local `/var/dam/jobs/download` pode baixar ativos.
>
>Os tipos de ativos - Conjuntos de imagens, Conjuntos de rotação, Conjuntos de mídia mista e Conjuntos de carrossel não podem ser baixados.

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**Para baixar os ativos, siga estas etapas:**

1. No canto superior esquerdo, clique no logotipo. No painel à esquerda, clique em **[!UICONTROL Navegação]**.
1. Na página [!UICONTROL Navegação], clique em **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Navegue até uma pasta que contenha os ativos que você deseja baixar.
1. Selecione a pasta ou selecione um ou mais ativos na pasta.
1. Na barra de ferramentas, clique em **[!UICONTROL Baixar]**.
1. Na caixa de diálogo Download, selecione as opções de download desejadas.

   | Opção de exportação ou download | Descrição |
   |---|---|
   | **[!UICONTROL Criar uma pasta separada para cada ativo]** | Selecione essa opção para incluir cada ativo baixado, inclusive ativos em pastas secundárias aninhadas na pasta principal do ativo, em uma pasta no computador local. Quando essa opção não está selecionada, por padrão, a hierarquia de pastas é ignorada e todos os ativos são baixados para uma pasta no computador local. |
   | **[!UICONTROL Email]** | Uma notificação por email é enviada ao usuário. Os modelos padrão de email estão disponíveis nos seguintes locais:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Os modelos que você personaliza durante a implantação estão disponíveis nos seguintes locais: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Você pode armazenar modelos personalizados específicos do locatário nos seguintes locais:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ativo(s)]** | Selecione essa opção para baixar o ativo em sua forma original sem representações.<br>A opção de subativos estará disponível se o ativo original tiver subativos. |
   | **[!UICONTROL Representação(ões)]** | Uma representação é a representação binária de um ativo. O Assets tem uma representação principal - a do arquivo carregado. Eles podem ter qualquer número de representações. <br> Com essa opção, você pode selecionar as representações que deseja baixar. As representações disponíveis dependem do ativo selecionado. A opção estará disponível se o ativo tiver representações. |
   | **[!UICONTROL Recortes inteligentes]** | Selecione essa opção para baixar todas as representações de corte inteligente do ativo selecionado no AEM. Um arquivo zip com as representações de Recorte inteligente é criado e baixado no computador local. |
   | **[!UICONTROL Representação(ões) Dinâmica(s)]** | Selecione essa opção para gerar uma série de representações alternativas em tempo real. Ao selecionar essa opção, você também seleciona as representações que deseja criar dinamicamente, selecionando na lista [Predefinição de imagem](image-presets.md). <br>Além disso, você pode selecionar o tamanho e a unidade de medida, o formato, o espaço de cores, a resolução e qualquer modificador de imagem opcional, como a inversão da imagem. A opção só estará disponível se você tiver o [!DNL Dynamic Media] habilitado. |

1. Na caixa de diálogo, clique em **[!UICONTROL Baixar]**.

Ao selecionar uma pasta para download, a hierarquia completa de ativos na pasta é baixada. Para incluir cada ativo baixado (incluindo ativos em pastas derivadas aninhadas na pasta pai) em uma pasta individual, selecione **[!UICONTROL Criar pasta separada para cada ativo]**.

## Ativar o servlet de download de ativos {#enable-asset-download-servlet}

O servlet padrão no [!DNL Experience Manager] permite que usuários autenticados emitam arbitrariamente grandes solicitações de download simultâneas para criar arquivos ZIP de ativos visíveis a eles que podem sobrecarregar o servidor e a rede. Para mitigar possíveis riscos de DoS causados por esse recurso, o componente OSGi `AssetDownloadServlet` é desabilitado por padrão para instâncias de publicação.

Para permitir o download de ativos do seu DAM, ao usar algo como o Asset Share Commons ou outra implementação semelhante a um portal, ative manualmente o servlet por meio de uma configuração OSGi. A Adobe recomenda definir o tamanho permitido do download o mais baixo possível, sem afetar os requisitos diários de download. Um valor alto pode afetar o desempenho.

1. Crie uma pasta com uma convenção de nomenclatura que direcione ao modo de execução de publicação (`config.publish`): `/apps/<your-app-name>/config.publish`. Para definir propriedades de configuração para um modo de execução, consulte [Modos de Execução](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. Na pasta de configuração, crie um arquivo do tipo `nt:file` chamado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Preencha `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` com o seguinte. Define um tamanho máximo (em bytes) para o download como o valor de `asset.download.prezip.maxcontentsize`. O exemplo abaixo configura o tamanho máximo do download do ZIP para não exceder 100 kb.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

Por padrão, para `GET` solicitações de download de arquivos, [!DNL Experience Manager] impõe um limite de 50 MB no tamanho de download do arquivo ZIP. Downloads iniciados por solicitações `POST` ou pela interface do usuário não são afetados por esse limite.

## Desativar o servlet de download de ativos {#disable-asset-download-servlet}

O `Asset Download Servlet` pode ser desativado em uma instância do Publish [!DNL Experience Manager] ao atualizar a configuração do Dispatcher para bloquear qualquer solicitação de download de ativo. O servlet também pode ser desativado manualmente por meio do console OSGi diretamente.

1. Para bloquear solicitações de download de ativos por meio de uma configuração de Dispatcher, edite a configuração `dispatcher.any` e adicione uma regra à [seção de filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Para desativar o componente OSGi em uma instância do Publish, acesse o Console OSGi em `http://[aem_server]:[port]/system/console/components`. Localize `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` e clique em **[!UICONTROL Desabilitar]**.

>[!MORELIKETHIS]
>
>* [Baixar ativos usando o Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [Baixar ativos protegidos por DRM](drm.md).
>* [Baixe ativos usando o aplicativo de desktop Experience Manager no Win ou no Mac desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [Baixe ativos usando o Adobe Assets Link nos aplicativos Adobe Creative Cloud compatíveis](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html).

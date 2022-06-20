---
title: Baixar ativos
description: Saiba como baixar ativos no [!DNL Adobe Experience Manager] e ative ou desative a funcionalidade de download.
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 5%

---

# Baixar ativos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/download-assets-from-aem.html?lang=en) |

Você pode baixar ativos, incluindo representações estáticas e dinâmicas. Como alternativa, você pode enviar emails com links para ativos diretamente do [!DNL Adobe Experience Manager Assets]. Os ativos baixados são agrupados em um arquivo ZIP. O arquivo ZIP compactado tem um tamanho máximo de arquivo de 1 GB para o trabalho de exportação. É permitido um máximo de 500 ativos totais por trabalho de exportação.

>[!NOTE]
>
>Qualquer usuário com permissões de leitura em `/var/dam/share` O local pode acessar o link de download compartilhado na mensagem de email.
>
>Qualquer usuário com permissões de leitura para `/var/dam/jobs/download` O local pode baixar ativos.
>
>Os tipos de ativos - Conjuntos de imagens, Conjuntos de rotação, Conjuntos de mídia mista e Conjuntos de carrossel não podem ser baixados.

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**Para baixar ativos, siga estas etapas:**

1. No canto superior esquerdo, clique no logotipo . No painel à esquerda, clique em **[!UICONTROL Navegação]**.
1. No [!UICONTROL Navegação] página, clique em **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Navegue até uma pasta que contenha ativos que você deseja baixar.
1. Selecione a pasta ou selecione um ou mais ativos na pasta.
1. Na barra de ferramentas, clique em **[!UICONTROL Baixar]**.
1. Na caixa de diálogo Download, selecione as opções de download desejadas.

   | Opção de exportação ou download | Descrição |
   |---|---|
   | **[!UICONTROL Criar uma pasta separada para cada ativo]** | Selecione essa opção para incluir cada ativo que você baixar, incluindo ativos em pastas filhas aninhadas na pasta principal do ativo, em uma pasta no computador local. Quando essa opção não é selecionada, por padrão, a hierarquia de pastas é ignorada e todos os ativos são baixados em uma pasta no computador local. |
   | **[!UICONTROL Email]** | Uma notificação por email é enviada ao usuário. Os modelos padrão de emails estão disponíveis nos seguintes locais:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Os modelos personalizados durante a implantação estão disponíveis nos seguintes locais: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Você pode armazenar modelos personalizados específicos do locatário nos seguintes locais:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ativo(s)]** | Selecione essa opção para baixar o ativo em seu formulário original sem nenhuma representação.<br>A opção por ativos secundários estará disponível se o ativo original tiver ativos secundários. |
   | **[!UICONTROL Representações]** | Uma representação é uma representação binária de um ativo. Os ativos têm uma representação principal: a do arquivo carregado. Eles podem ter qualquer número de representações. <br> Com essa opção, você pode selecionar as representações que deseja baixar. As representações disponíveis dependem do ativo selecionado. A opção estará disponível se o ativo tiver renderizações. |
   | **[!UICONTROL Cortes inteligentes]** | Selecione esta opção para baixar todas as representações de recorte inteligente do ativo selecionado no AEM. Um arquivo zip com as representações de Recorte inteligente é criado e baixado no computador local. |
   | **[!UICONTROL Representação(ões) dinâmica(s)]** | Selecione essa opção para gerar uma série de representações alternativas em tempo real. Ao selecionar essa opção, você também seleciona as representações que deseja criar dinamicamente, selecionando no [Predefinição de imagem](image-presets.md) lista. <br>Além disso, é possível selecionar o tamanho e a unidade de medida, o formato, o espaço de cores, a resolução e qualquer modificador de imagem opcional, como inverter a imagem. A opção só estará disponível se você tiver [!DNL Dynamic Media] habilitado. |

1. Na caixa de diálogo, clique em **[!UICONTROL Baixar]**.

Ao selecionar uma pasta para baixar, a hierarquia completa do ativo na pasta é baixada. Para incluir cada ativo baixado (incluindo ativos em pastas filhas aninhadas na pasta principal) em uma pasta individual, selecione **[!UICONTROL Criar uma pasta separada para cada ativo]**.

## Habilitar servlet de download de ativos {#enable-asset-download-servlet}

O servlet padrão em [!DNL Experience Manager] O permite que usuários autenticados emitam solicitações de download arbitrariamente grandes e simultâneas para criar arquivos ZIP de ativos visíveis a eles que podem sobrecarregar o servidor e a rede. Para reduzir possíveis riscos de DoS causados por esse recurso, `AssetDownloadServlet` O componente OSGi é desabilitado por padrão para instâncias de publicação.

Para permitir o download de ativos do DAM, digamos ao usar algo como o Asset Share Commons ou outra implementação semelhante a portal, ative manualmente o servlet por meio de uma configuração OSGi. A Adobe recomenda definir o tamanho de download permitido o mais baixo possível sem afetar os requisitos diários de download. Um alto valor pode afetar o desempenho.

1. Crie uma pasta com uma convenção de nomenclatura que seja direcionada ao modo de execução de publicação (`config.publish`): `/apps/<your-app-name>/config.publish`. Para definir as propriedades de configuração para um modo de execução, consulte [Modos de Execução](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. Na pasta de configuração, crie um arquivo do tipo `nt:file` nomeado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Preencher `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` com o seguinte. Define um tamanho máximo (em bytes) para download como valor de `asset.download.prezip.maxcontentsize`. A amostra abaixo configura o tamanho máximo do download ZIP para não exceder 100 kB.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

Por padrão, para `GET` solicitações para baixar arquivos, [!DNL Experience Manager] impõe um limite de 50 MB no tamanho de download do arquivo ZIP. Downloads iniciados via `POST` As solicitações ou a interface do usuário não são afetadas por esse limite.

## Desativar o servlet de download de ativos {#disable-asset-download-servlet}

O `Asset Download Servlet` pode ser desativado em um [!DNL Experience Manager] Publique instâncias atualizando a configuração do dispatcher para bloquear qualquer solicitação de download de ativo. O servlet também pode ser desabilitado manualmente por meio do console OSGi diretamente.

1. Para bloquear solicitações de download de ativos por meio de uma configuração de dispatcher, edite a variável `dispatcher.any` e adicionar uma regra ao [seção de filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Para desativar o componente OSGi em uma instância de publicação, acesse o console OSGi em `http://[aem_server]:[port]/system/console/components`. Localizar `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` e clique em **[!UICONTROL Desativar]**.

>[!MORELIKETHIS]
>
>* [Baixar ativos usando o Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [Baixar ativos protegidos por DRM](drm.md).
>* [Baixe ativos usando o aplicativo de desktop do Experience Manager no desktop Win ou Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [Baixar ativos usando o Link de ativos do Adobe nos aplicativos Adobe Creative Cloud compatíveis](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html).


---
title: Como editar ou adicionar metadados
description: Saiba mais sobre metadados de ativos no [!DNL Adobe Experience Manager Assets] e sobre várias maneiras pelas quais você pode editar metadados de ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Como editar ou adicionar metadados {#how-to-edit-or-add-metadata}

Metadados são informações adicionais sobre o ativo que pode ser pesquisado. Ele é extraído automaticamente quando você carrega uma imagem. Você pode editar os metadados existentes ou adicionar novas propriedades de metadados a campos existentes (por exemplo, quando um campo de metadados estiver em branco).

Como as organizações precisam de vocabulários de metadados controlados e confiáveis, [!DNL Experience Manager Assets] não permite a adição ad-hoc de novas propriedades de metadados. Embora os autores não possam adicionar novos campos de metadados para ativos, os desenvolvedores podem. Consulte [criar nova propriedade de metadados para ativos](meta-edit.md#editing-metadata-schema).

## Editar metadados para um ativo {#editing-metadata-for-an-asset}

Para editar metadados:

1. Faça uma das seguintes opções:

   * Na [!DNL Assets] interface, selecione o ativo e clique em Propriedades **[!UICONTROL da]** Visualização na barra de ferramentas.
   * Na miniatura do ativo, selecione a ação rápida Propriedades **[!UICONTROL da]** Visualização.
   * Na página de ativos, clique em Propriedades **[!UICONTROL da]** Visualização ![chlimage_1-168](assets/chlimage_1-168.png) na barra de ferramentas.
   A página do ativo exibe todos os metadados do ativo. Os metadados são extraídos quando o ativo é carregado (assimilado) no Experience Manager.

   ![selecione Propriedades do ativo para visualização de metadados](assets/asset-metadata.png)

   *Figura: Edite ou adicione metadados na página Propriedades do ativo.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the Assets web interface.

   >[!NOTE]
   >
   >Se um campo de texto estiver vazio, não há metadados definidos. Você pode inserir um valor no campo e salvá-lo para adicionar essa propriedade de metadados.

Quaisquer alterações nos metadados de um ativo são gravadas de volta no binário original como parte de seus dados XMP. Isso é feito por meio do fluxo de trabalho de gravação de metadados do Experience Manager. As alterações feitas nas propriedades existentes (como `dc:title`) são substituídas e as propriedades recém-criadas (incluindo propriedades personalizadas como `cq:tags`) são adicionadas ao schema.

A gravação XMP é suportada e ativada para as plataformas e formatos de arquivo descritos nos requisitos [técnicos.](/help/sites-deploying/technical-requirements.md)

## Editar schema de metadados {#editing-metadata-schema}

Para obter detalhes sobre como editar schemas de metadados, consulte [Editar formulários](metadata-schemas.md#edit-metadata-schema-forms)de schema de metadados.

## Registrar uma namespace personalizada no Experience Manager {#registering-a-custom-namespace-within-aem}

Você pode adicionar suas próprias namespaces no Experience Manager. Assim como há namespaces predefinidas, como cq, jcr e sling, você pode ter uma namespace para os metadados do repositório e o processamento xml.

1. Vá para a página de administração do tipo de nó `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Clique em **[!UICONTROL Namespace]** na parte superior da página. A página de administração da namespace é exibida em uma janela.

1. Para adicionar uma namespace, clique em **[!UICONTROL Novo]** na parte inferior.
1. Especifique uma namespace personalizada na convenção de namespace XML (especifique a ID no formato de um URI e um prefixo associado para a ID) e clique em **[!UICONTROL Salvar]**.

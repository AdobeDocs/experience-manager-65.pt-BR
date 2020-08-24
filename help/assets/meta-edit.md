---
title: Como editar ou adicionar metadados
description: Saiba mais sobre os metadados do ativo [!DNL Adobe Experience Manager Assets] de várias maneiras pelas quais você pode editar os metadados do ativo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: fc14ccc834c9a41b67eb8cf17dd8b34f5dff2406
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---


# Como editar ou adicionar metadados {#how-to-edit-or-add-metadata}

Metadados são informações adicionais sobre o ativo que pode ser pesquisado. Ele é extraído automaticamente quando você carrega uma imagem. Você pode editar os metadados existentes ou adicionar novas propriedades de metadados ao campo existente, por exemplo, quando um campo de metadados estiver em branco.

As organizações precisam de vocabulários de metadados controlados e confiáveis. Portanto, não [!DNL Experience Manager Assets] permite a adição sob demanda de novas propriedades de metadados. Os desenvolvedores e não os autores podem adicionar novos campos de metadados para ativos. Consulte [criar propriedade de metadados para ativos](meta-edit.md#editing-metadata-schema).

## Editar metadados para um ativo {#editing-metadata-for-an-asset}

Para editar metadados, siga estas etapas:

1. Faça uma das seguintes opções:

   * Na [!DNL Assets] interface, selecione o ativo e clique em Propriedades **[!UICONTROL da]** Visualização na barra de ferramentas.
   * Na miniatura do ativo, selecione a ação rápida Propriedades **[!UICONTROL da]** Visualização.
   * Na página do ativo, clique no ícone **[!UICONTROL de informações Propriedades]** da ![Visualização](assets/do-not-localize/info-circle-icon.png) Ativos na barra de ferramentas.

   A página do ativo exibe todos os metadados do ativo. Os metadados são extraídos quando o ativo é carregado (assimilado) no [!DNL Experience Manager].

   ![Selecione Propriedades de um ativo para visualização de seus metadados](assets/asset-metadata.png)

   *Figura: Edite ou adicione metadados na página[!UICONTROL Propriedades]do ativo.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >Se um campo de texto estiver vazio, não há metadados definidos. Você pode inserir um valor no campo e salvá-lo para adicionar essa propriedade de metadados.

Quaisquer alterações nos metadados de um ativo são gravadas de volta no binário original como parte de seus dados XMP. O fluxo de trabalho de gravação de metadados adiciona os metadados ao binário original. As alterações feitas nas propriedades existentes (como `dc:title`) são substituídas e novas propriedades (incluindo propriedades personalizadas como `cq:tags`) são adicionadas ao schema.

XMP gravação é suportada e ativada para plataformas e formatos de arquivos descritos nos requisitos [técnicos.](/help/sites-deploying/technical-requirements.md)

## Editar schema de metadados {#editing-metadata-schema}

Para obter detalhes, consulte [editar formulários](metadata-schemas.md#edit-metadata-schema-forms)de schema de metadados.

## Registrar uma namespace personalizada em [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Você pode adicionar suas próprias namespaces dentro [!DNL Experience Manager]. Assim como há namespaces predefinidas, como `cq`, `jcr`e `sling`, você pode ter uma namespace para os metadados do repositório e o processamento XML.

1. Acesse a página de administração do tipo de nó `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acessar a página de administração de namespaces, clique em **[!UICONTROL Namespaces]** na parte superior da página.
1. Para adicionar uma namespace, clique em **[!UICONTROL Novo]** na parte inferior da página.
1. Especifique uma namespace personalizada na convenção de namespace XML. Especifique a ID na forma de um URI e um prefixo associado para a ID. Clique em **[!UICONTROL Salvar]**.

## Dicas e limitações {#best-practices-limitations}

* Os metadados são atualizados por interface de usuário sensível ao toque e alteram as propriedades dos metadados na `dc` namespace. Qualquer atualização feita por meio da API HTTP altera as propriedades de metadados na `jcr` namespace. Consulte [como atualizar metadados usando a API](/help/assets/mac-api-assets.md#update-asset-metadata)HTTP.

>[!MORELIKETHIS]
>
>* [Sobre metadados e suas necessidades em ativos](metadata.md)
>* [Metadados XMP](xmp.md)
>* [Referência dos esquemas de metadados](meta-ref.md)


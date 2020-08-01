---
title: Write-back de XMP a execuções
description: Saiba como o recurso XMP write-back propaga as alterações de metadados de um ativo para todas as execuções ou representações específicas do ativo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 5%

---


# Write-back de XMP a execuções {#xmp-writeback-to-renditions}

O recurso de write-back XMP em [!DNL Adobe Experience Manager Assets] replica as alterações nos metadados do ativo nas representações do ativo. Quando você altera os metadados de um ativo de dentro [!DNL Experience Manager Assets] ou durante o upload do ativo, as alterações são armazenadas inicialmente no nó do ativo no CRXDe. O recurso de write-back XMP propaga as alterações nos metadados para todas as execuções ou para as execuções específicas do ativo.

Considere um cenário em que você modifica a propriedade [!UICONTROL Título] do ativo com título `Classic Leather` para `Nylon`.

![metadata](assets/metadata.png)

Nesse caso, o [!DNL Experience Manager Assets] salva as alterações na propriedade **[!UICONTROL Title]** no `dc:title` parâmetro para os metadados do ativo armazenados na hierarquia do ativo.

![metadata_storage](assets/metadata_stored.png)

No entanto, [!DNL Experience Manager Assets] não propaga automaticamente quaisquer alterações de metadados nas representações de um ativo.

O recurso XMP Writeback permite que você propague as alterações de metadados para todas as execuções ou representações específicas do ativo. No entanto, as alterações não são armazenadas no nó de metadados na hierarquia do ativo. Em vez disso, esse recurso incorpora as alterações nos arquivos binários das execuções.

## Habilitar XMP write-back {#enabling-xmp-writeback}

Para permitir que as alterações de metadados sejam propagadas para as representações do ativo ao carregá-lo, modifique a configuração do **[!UICONTROL Adobe CQ DAM Rendition Maker]** no Configuration Manager.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração do **[!UICONTROL Adobe CQ DAM Rendition Maker]** .
1. Selecione a opção **[!UICONTROL Propagate XMP[!UICONTROL ** e salve as alterações.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Habilitar XMP write-back para execuções específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que o recurso XMP Writeback propague alterações de metadados para selecionar execuções, especifique essas execuções para a etapa de fluxo de trabalho XMP Processo de gravação do fluxo de trabalho WriteBack [!UICONTROL de metadados de] DAM. Por padrão, essa etapa é configurada com a representação original.

Para que o recurso XMP Writeback propague metadados para as miniaturas de execução 140.100.png e 319.319.png, execute estas etapas.

1. Na interface do Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos, abra o modelo de fluxo de trabalho Writeback **[!UICONTROL de metadados]** DAM.
1. Na página de propriedades **[!UICONTROL DAM Metadata Writeback]**, abra a etapa **[!UICONTROL Processo de Writeback XMP]**.
1. In the [!UICONTROL Step Properties] dialog box, click the **[!UICONTROL Process]** tab.
1. Na caixa **Argumentos** , adicione `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`e clique em **OK**.

   ![step_properties](assets/step_properties.png)

1. Salve as alterações.
1. To regenerate the pyramid TIFF renditions for [!DNL Dynamic Media] images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the [!UICONTROL DAM Metadata Writeback] workflow.

   As representações PTIFF são criadas e armazenadas apenas localmente em uma implementação híbrida do Dynamic Media.

1. Salve o fluxo de trabalho.

As alterações de metadados são propagadas para as representações representações thumbnail.140.100.png e thumbnail.319.319.png do ativo, e não para as outras.

>[!NOTE]
>
>Para XMP problemas de gravação no Linux de 64 bits, consulte [Como ativar XMP write-back no RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)de 64 bits.
>
>Para as plataformas compatíveis, consulte [XMP pré-requisitos](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)de gravação de metadados.

## Filtrar metadados XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] suporta a filtragem de lista de bloqueios e lista de permissões de propriedades/nós para metadados XMP que são lidos de binários de ativos e armazenados no JCR quando os ativos são ingeridos.

Filtrar usando uma lista de bloqueios permite importar todas as propriedades de metadados XMP, exceto as propriedades especificadas para exclusão. No entanto, para tipos de ativos, como arquivos INDD que têm uma grande quantidade de metadados XMP (por exemplo, 1000 nós com 10.000 propriedades), os nomes dos nós a serem filtrados nem sempre são conhecidos antecipadamente. Se a filtragem usando uma lista de bloqueios permitir a importação de um grande número de ativos com diversos metadados XMP, a [!DNL Experience Manager] implantação poderá enfrentar problemas de estabilidade, por exemplo, filas de observação obstruídas.

A filtragem de metadados de XMP por lista de permissões resolve esse problema ao permitir que você defina as propriedades de XMP a serem importadas. Dessa forma, qualquer outra propriedade XMP ou desconhecida é ignorada. Para compatibilidade com versões anteriores, você pode adicionar algumas dessas propriedades ao filtro que usa uma lista de bloqueios.

>[!NOTE]
>
>A filtragem funciona somente para as propriedades derivadas de fontes XMP em binários de ativos. Para as propriedades derivadas de fontes não XMP, como formatos EXIF e IPTC, a filtragem não funciona. Por exemplo, a data de criação do ativo é armazenada em uma propriedade chamada `CreateDate` em EXIF TIFF. O Experience Manager armazena esse valor em um campo de metadados chamado `exif:DateTimeOriginal`. Como a fonte é uma fonte não XMP, a filtragem não funciona nessa propriedade.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração **[!UICONTROL Adobe CQ DAM XmpFilter]** .
1. To apply filtering via an allowed list, select **[!UICONTROL Apply Allowlist to XMP Properties]**, and specify the properties to be imported in the **[!UICONTROL Allowed XML Names for XMP filtering]** box.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar XMP propriedades bloqueadas após a aplicação da filtragem por lista de permissões, especifique as propriedades na caixa Nomes XML **[!UICONTROL bloqueados para XMP filtragem]** .

   >[!NOTE]
   >
   >A opção **[!UICONTROL Aplicar Lista de bloqueios a XMP propriedades]** está selecionada por padrão. Em outras palavras, a filtragem usando uma lista de bloqueios é ativada por padrão. Para desativar essa filtragem, desmarque a opção **[!UICONTROL Aplicar Lista de bloqueios a XMP propriedades]** .

1. Salve as alterações.

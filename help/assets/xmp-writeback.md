---
title: Write-back de XMP a execuções
description: Saiba como o recurso de gravação XMP propaga as alterações de metadados de um ativo para todas as execuções ou representações específicas do ativo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 11%

---


# Write-back de XMP a execuções {#xmp-writeback-to-renditions}

O recurso de gravação XMP em [!DNL Adobe Experience Manager Assets] replica as alterações nos metadados do ativo nas representações do ativo. Quando você altera os metadados de um ativo de dentro [!DNL Experience Manager Assets] ou durante o upload do ativo, as alterações são armazenadas inicialmente no nó do ativo no CRXDe. O recurso de write-back XMP propaga as alterações de metadados para todas as execuções ou representações específicas do ativo.

Considere um cenário em que você modifica a propriedade [!UICONTROL Título] do ativo com título `Classic Leather` para `Nylon`.

![metadata](assets/metadata.png)

Nesse caso, o [!DNL Experience Manager Assets] salva as alterações na propriedade **[!UICONTROL Title]** no `dc:title` parâmetro para os metadados do ativo armazenados na hierarquia do ativo.

![metadata_storage](assets/metadata_stored.png)

No entanto, [!DNL Experience Manager Assets] não propaga automaticamente quaisquer alterações de metadados nas representações de um ativo.

O recurso de Writeback XMP permite que você propague as alterações de metadados para todas as representações ou representações específicas do ativo. No entanto, as alterações não são armazenadas no nó de metadados na hierarquia do ativo. Em vez disso, esse recurso incorpora as alterações nos arquivos binários das execuções.

## Habilitando o write-back XMP {#enabling-xmp-writeback}

Para permitir que as alterações de metadados sejam propagadas para as representações do ativo ao carregá-lo, modifique a configuração do **[!UICONTROL Adobe CQ DAM Rendition Maker]** no Configuration Manager.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração do **[!UICONTROL Adobe CQ DAM Rendition Maker]** .
1. Selecione a opção **[!UICONTROL Propagate XMP[!UICONTROL ** e salve as alterações.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Habilitar o write-back XMP para execuções específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que o recurso de Gravação XMP propague alterações de metadados para selecionar execuções, especifique essas execuções para a etapa de fluxo de trabalho do Processo de Gravação XMP do fluxo de trabalho WriteBack [!UICONTROL de Metadados] DAM. Por padrão, essa etapa é configurada com a representação original.

Para o recurso de Writeback XMP propagar metadados para as miniaturas de execução 140.100.png e 319.319.png, execute estas etapas.

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
>Para problemas de gravação em XMP no Linux de 64 bits, consulte [Como ativar a gravação em XMP no RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)de 64 bits.
>
>Para obter mais informações sobre plataformas compatíveis, consulte Pré-requisitos [de gravação de metadados](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)XMP.

## Filtrar metadados XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] suporta a filtragem de listas negras e de listas brancas de propriedades/nós para metadados XMP que são lidos de binários de ativos e armazenados no JCR quando os ativos são ingeridos.

A filtragem da lista negra permite importar todas as propriedades de metadados XMP, exceto as propriedades especificadas para exclusão. No entanto, para tipos de ativos, como arquivos INDD que têm quantidades enormes de metadados XMP (por exemplo, 1000 nós com 10.000 propriedades), os nomes dos nós a serem filtrados nem sempre são conhecidos antecipadamente. Se a filtragem da lista negra permitir a importação de um grande número de ativos com diversos metadados XMP, a implantação do Experience Manager poderá enfrentar problemas de estabilidade, por exemplo, filas de observação obstruídas.

A filtragem da lista de permissões dos metadados XMP resolve esse problema ao permitir que você defina as propriedades XMP a serem importadas. Dessa forma, outras propriedades XMP/desconhecidas são ignoradas. Você pode adicionar algumas dessas propriedades ao filtro da lista negra para compatibilidade com versões anteriores.

>[!NOTE]
>
>A filtragem funciona somente para as propriedades derivadas de fontes XMP em binários de ativos. Para as propriedades derivadas de fontes não XMP, como formatos EXIF e IPTC, a filtragem não funciona. Por exemplo, a data de criação do ativo é armazenada em uma propriedade chamada `CreateDate` em EXIF TIFF. O Experience Manager armazena esse valor em um campo de metadados chamado `exif:DateTimeOriginal`. Como a fonte é uma fonte não XMP, a filtragem não funciona nessa propriedade.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração **[!UICONTROL Adobe CQ DAM XmpFilter]** .
1. Para aplicar a filtragem de lista de permissões, selecione **[!UICONTROL Aplicar lista de permissões às propriedades XMP]** e especifique as propriedades que serão importadas na caixa **[!UICONTROL Nomes XML na lista de permissões para filtragem XMP]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar as propriedades XMP proibidas após aplicar a filtragem de lista de permissões, especifique-as na caixa **[!UICONTROL Nomes XML não permitidos para filtragem XMP]**.

   >[!NOTE]
   >
   >A opção **[!UICONTROL Aplicar lista negra a propriedades]** XMP está selecionada por padrão. Em outras palavras, a filtragem da lista negra é ativada por padrão. Para desativar a filtragem da lista negra, desmarque a opção **[!UICONTROL Aplicar lista negra às propriedades]** XMP.

1. Salve as alterações.

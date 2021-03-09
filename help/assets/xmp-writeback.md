---
title: Write-back de XMP a execuções
description: Saiba como o recurso de write-back XMP propaga as alterações de metadados de um ativo para todas ou representações específicas do ativo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: cf86d0c38e326766b35318e78a94a3f32e166e01
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 5%

---


# Write-back de XMP a execuções {#xmp-writeback-to-renditions}

O recurso de write-back XMP em [!DNL Adobe Experience Manager Assets] replica as alterações nos metadados do ativo nas representações do ativo. Quando você altera os metadados de um ativo de [!DNL Experience Manager Assets] ou durante o upload do ativo, as alterações são armazenadas inicialmente no nó do ativo no CRXDe. O recurso de gravação XMP propaga as alterações de metadados para todas as representações ou representações específicas do ativo.

Considere um cenário em que você modifica a propriedade [!UICONTROL Title] do ativo intitulado `Classic Leather` para `Nylon`.

![metadados](assets/metadata.png)

Nesse caso, o [!DNL Experience Manager Assets] salva as alterações na propriedade **[!UICONTROL Title]** no parâmetro `dc:title` para os metadados de ativos armazenados na hierarquia de ativos.

![metadata_stored](assets/metadata_stored.png)

No entanto, [!DNL Experience Manager Assets] não propaga automaticamente quaisquer alterações de metadados nas representações de um ativo.

O recurso de Writeback XMP permite propagar as alterações de metadados para todas as representações ou representações específicas do ativo. No entanto, as alterações não são armazenadas no nó de metadados na hierarquia de ativos. Em vez disso, esse recurso incorpora as alterações nos arquivos binários das representações.

## Ativando o write-back XMP {#enabling-xmp-writeback}

Para permitir que as alterações de metadados sejam propagadas para as representações do ativo ao carregá-lo, modifique a configuração **[!UICONTROL Adobe CQ DAM Rendition Maker]** no Configuration Manager.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração do **[!UICONTROL Adobe CQ DAM Rendition Maker]**.
1. Selecione a opção **[!UICONTROL Propagar XMP]** e salve as alterações.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Ativando o write-back de XMP para representações específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que o recurso de Writeback XMP propague alterações de metadados para selecionar representações, especifique essas representações para a etapa de fluxo de trabalho do Processo de Writeback XMP do fluxo de trabalho [!UICONTROL WriteBack de Metadados DAM] . Por padrão, essa etapa é configurada com a representação original.

Para o recurso de gravação XMP propagar metadados para as miniaturas de representação 140.100.png e 319.319.png, execute estas etapas.

1. Na interface do Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos , abra o modelo de fluxo de trabalho **[!UICONTROL DAM Metadata Writeback]** .
1. Na página de propriedades **[!UICONTROL DAM Metadata Writeback]**, abra a etapa **[!UICONTROL Processo de Writeback XMP]**.
1. Na caixa de diálogo [!UICONTROL Propriedades da etapa], clique na guia **[!UICONTROL Processo]**.
1. Na caixa **Argumentos**, adicione `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png` e clique em **OK**.

   ![step_properties](assets/step_properties.png)

1. Salve as alterações.
1. Para regenerar as representações de pirâmide TIFF de [!DNL Dynamic Media] imagens com os novos atributos, adicione a etapa **[!UICONTROL Ativos de imagem do processo do Dynamic Media]** ao fluxo de trabalho [!UICONTROL Writeback de metadados do DAM].

   As representações PTIFF são criadas e armazenadas apenas localmente em uma implementação híbrida do Dynamic Media.

1. Salve o workflow.

As alterações de metadados são propagadas para a miniatura de representações.140.100.png e thumbnail.319.319.png do ativo, e não para os outros.

>[!NOTE]
>
>Para problemas de write-back de XMP no Linux de 64 bits, consulte [Como ativar o write-back de XMP no RedHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Para as plataformas compatíveis, consulte [Pré-requisitos de gravação de metadados XMP](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrar metadados XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] O suporta a filtragem de lista bloqueada e de lista permitida de propriedades/nós para metadados XMP que são lidos de binários de ativos e armazenados no JCR quando os ativos são assimilados.

Filtrar usando uma lista bloqueada permite importar todas as propriedades de metadados XMP, exceto as propriedades especificadas para exclusão. No entanto, para tipos de ativos como arquivos INDD que têm grandes quantidades de metadados XMP (por exemplo, 1000 nós com 10.000 propriedades), os nomes de nós a serem filtrados nem sempre são conhecidos antecipadamente. Se a filtragem usando uma lista bloqueada permitir que um grande número de ativos com vários metadados XMP seja importado, a implantação [!DNL Experience Manager] poderá encontrar problemas de estabilidade, por exemplo, filas de observação obstruídas.

A filtragem de metadados XMP por meio da lista de permissões resolve esse problema permitindo definir as propriedades XMP a serem importadas. Dessa forma, qualquer outra propriedade XMP ou desconhecida é ignorada. Para compatibilidade com versões anteriores, você pode adicionar algumas dessas propriedades ao filtro que usa uma lista bloqueada.

>[!NOTE]
>
>A filtragem funciona somente para as propriedades derivadas de fontes XMP em binários de ativos. Para as propriedades derivadas de fontes não XMP, como formatos EXIF e IPTC, a filtragem não funciona. Por exemplo, a data de criação do ativo é armazenada na propriedade chamada `CreateDate` em EXIF TIFF. O Experience Manager armazena esse valor em um campo de metadados chamado `exif:DateTimeOriginal`. Como a fonte é uma fonte não-XMP, a filtragem não funciona nessa propriedade.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração **[!UICONTROL Adobe CQ DAM XmpFilter]**.
1. Para aplicar a filtragem por meio de uma lista permitida, selecione **[!UICONTROL Aplicar lista de permissões às propriedades XMP]** e especifique as propriedades a serem importadas na caixa **[!UICONTROL Nomes XML permitidos para filtragem XMP]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar as propriedades XMP bloqueadas depois de aplicar a filtragem por meio da lista permitida, especifique aquelas na caixa **[!UICONTROL Nomes XML bloqueados para filtragem XMP]**.

   >[!NOTE]
   >
   >A opção **[!UICONTROL Aplicar Lista de Bloqueios às Propriedades XMP]** é selecionada por padrão. Em outras palavras, filtrar usando uma lista bloqueada é ativado por padrão. Para desativar essa filtragem, cancele a seleção da opção **[!UICONTROL Aplicar Lista de Bloqueios às Propriedades XMP]**.

1. Salve as alterações.

---
title: Write-back de XMP a execuções
description: Saiba como o recurso de write-back de XMP propaga as alterações de metadados de um ativo para todas as representações ou representações específicas do ativo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7faa6638eff422599450946a257e53970d25189c
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 5%

---


# Write-back de XMP a execuções {#xmp-writeback-to-renditions}

Esse recurso de write-back de XMP em [!DNL Adobe Experience Manager Assets] replica as alterações de metadados nas representações do ativo original. Ao alterar os metadados de um ativo de dentro do Assets ou ao fazer upload do ativo, as alterações são armazenadas inicialmente no nó de metadados na hierarquia de ativos.

O recurso de write-back de XMP permite propagar as alterações de metadados para todas as representações ou representações específicas do ativo. O recurso grava somente as propriedades de metadados que usam `jcr` namespace, ou seja, uma propriedade chamada `dc:title` é gravada novamente, mas uma propriedade chamada `mytitle` não é.

Considere um cenário em que você modifica a propriedade [!UICONTROL Title] do ativo intitulado `Classic Leather` para `Nylon`.

![metadados](assets/metadata.png)

Nesse caso, o [!DNL Experience Manager Assets] salva as alterações na propriedade **[!UICONTROL Title]** no parâmetro `dc:title` para os metadados de ativos armazenados na hierarquia de ativos.

![metadata_stored](assets/metadata_stored.png)

No entanto, [!DNL Experience Manager Assets] não propaga automaticamente quaisquer alterações de metadados nas representações de um ativo. Consulte [como ativar XMP write-back](#enable-xmp-writeback).

## Habilitar XMP write-back {#enable-xmp-writeback}

Para permitir que as alterações de metadados sejam propagadas para as representações do ativo ao carregá-lo, modifique a configuração **[!UICONTROL Adobe CQ DAM Rendition Maker]** no Configuration Manager.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração **[!UICONTROL Adobe CQ DAM Rendition Maker]**.
1. Selecione a opção **[!UICONTROL Propagar XMP]** e salve as alterações.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Ativando XMP write-back para representações específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que o recurso Writeback XMP propague alterações de metadados para selecionar representações, especifique essas representações na etapa XMP do fluxo de trabalho Processo de Writeback do fluxo de trabalho [!UICONTROL DAM Metadata WriteBack] . Por padrão, essa etapa é configurada com a representação original.

Para que o recurso Writeback de XMP propague metadados para as miniaturas de representação 140.100.png e 319.319.png, execute estas etapas.

1. Na interface do Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos , abra o modelo de fluxo de trabalho **[!UICONTROL DAM Metadata Writeback]** .
1. Na página de propriedades **[!UICONTROL DAM Metadata Writeback]**, abra a etapa **[!UICONTROL Processo de Writeback XMP]**.
1. Na caixa de diálogo [!UICONTROL Propriedades da etapa], clique na guia **[!UICONTROL Processo]**.
1. Na caixa **Argumentos**, adicione `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png` e clique em **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Salve as alterações.
1. Para regenerar as representações de pirâmide TIFF de [!DNL Dynamic Media] imagens com os novos atributos, adicione a etapa **[!UICONTROL Ativos de imagem de processo do Dynamic Media]** ao fluxo de trabalho [!UICONTROL Writeback de metadados do DAM].

   As representações PTIFF são criadas e armazenadas apenas localmente em uma implementação híbrida do Dynamic Media.

1. Salve o workflow.

As alterações de metadados são propagadas para a miniatura de representações.140.100.png e thumbnail.319.319.png do ativo, e não para os outros.

>[!NOTE]
>
>Para XMP problemas de write-back no Linux de 64 bits, consulte [Como ativar XMP write-back no RedHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Para as plataformas compatíveis, consulte [XMP pré-requisitos de gravação de metadados](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrar metadados de XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] O suporta a filtragem de lista de bloqueios e lista de permissões de propriedades/nós para metadados de XMP que são lidos de binários de ativos e armazenados no JCR quando os ativos são assimilados.

Filtrar usando uma lista de bloqueios permite importar todas as propriedades de metadados XMP, exceto as propriedades especificadas para exclusão. No entanto, para tipos de ativos como arquivos INDD que têm grandes quantidades de metadados de XMP (por exemplo, 1000 nós com 10.000 propriedades), os nomes de nós a serem filtrados nem sempre são conhecidos antecipadamente. Se a filtragem que usa uma lista de bloqueios permitir que um grande número de ativos com vários metadados de XMP seja importado, a implantação [!DNL Experience Manager] poderá encontrar problemas de estabilidade, por exemplo, filas de observação obstruídas.

A filtragem de metadados de XMP por meio do lista de permissões resolve esse problema permitindo definir as propriedades de XMP a serem importadas. Dessa forma, quaisquer propriedades de XMP outras ou desconhecidas são ignoradas. Para ter compatibilidade com versões anteriores, você pode adicionar algumas dessas propriedades ao filtro que usa uma lista de bloqueios.

>[!NOTE]
>
>A filtragem funciona somente nas propriedades derivadas de fontes de XMP em binários de ativos. Para as propriedades derivadas de fontes não XMP, como formatos EXIF e IPTC, a filtragem não funciona. Por exemplo, a data de criação do ativo é armazenada na propriedade chamada `CreateDate` em EXIF TIFF. O Experience Manager armazena esse valor em um campo de metadados chamado `exif:DateTimeOriginal`. Como a fonte é uma fonte não XMP, a filtragem não funciona nessa propriedade.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração **[!UICONTROL Adobe CQ DAM XmpFilter]**.
1. Para aplicar a filtragem por meio de uma lista de permissões, selecione **[!UICONTROL Aplicar Lista de permissões a XMP Propriedades]** e especifique as propriedades a serem importadas na caixa **[!UICONTROL Nomes XML permitidos para XMP filtragem]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar XMP propriedades bloqueadas após aplicar a filtragem via lista de permissões, especifique aquelas na caixa **[!UICONTROL Nomes XML bloqueados para XMP filtragem]**.

   >[!NOTE]
   >
   >A opção **[!UICONTROL Aplicar Lista de bloqueios a XMP Propriedades]** é selecionada por padrão. Em outras palavras, a filtragem usando uma lista de bloqueios é ativada por padrão. Para desativar essa filtragem, cancele a seleção da opção **[!UICONTROL Aplicar Lista de bloqueios a XMP Propriedades]**.

1. Salve as alterações.
